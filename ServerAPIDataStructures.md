## Table of contentss
* [Index](https://righttoaskorg.github.io/righttoask-docs/index)
* [Features](https://righttoaskorg.github.io/righttoask-docs/Features)
* [Screens and Usage](https://righttoaskorg.github.io/righttoask-docs/ScreensAndUsage)
* [Security and privacy](https://righttoaskorg.github.io/righttoask-docs/SecurityAndPrivacy)
* [Direct messaging](https://righttoaskorg.github.io/righttoask-docs/DMs)
* [Discussion and further questions](https://righttoaskorg.github.io/righttoask-docs/DiscussionAndFurtherQuestions)
* [Prototype](https://righttoaskorg.github.io/righttoask-docs/Prototype)
* [API](https://righttoaskorg.github.io/righttoask-docs/API)

# Server API Data Structures



<a id="data_structures_overview"/>
## Main Data structures

The server's internal data structures correspond closely to the data structures posted on the Bulletin Board.  However, since many public structures such as questions, tallies and public keys can be updated, the server needs to keep track of when multiple different bulletin board entries correspond to the same data item, for example updates or tallies for a question.  

Each data structure therefore has specific immutable fields which define it - for example, an entity is defined by its name. The hash of the defining data is returned when the data is first posted on the Bulletin Board, then used as an index for subsequent updates.

**TODO: so far this completely omits data structures for key generation - TBA.  **

<a id="transcript_def"/>
### Election Transcript
The election transcript consists of everything worth verifying:

- **Questions** including answers, directions, etc.
- **Ballots** which contain encrypted votes on questions
- **Tallies** i.e. decrypted aggregated votes on questions
- **Entities** which have a name and (possilby zero or multiple) public key(s)  

An **Entity** is either a department/ministerial portfolio (preloaded), a public authority (also preloaded, prob from RightToKnow), or a system user (an MP, citizen, or registered org rep). 

We assume data structures are transferred as JSON serialisations, and use || to indicate this.

<a id="question_def"/>
### Question 

Defining fields:

- Question_Text: string
    * Validity: character length
    * Permission: must be from the question-suggester
    * compulsory
- Question_Writer: Entity
    * Validity: must be a system user.
    * Permission: n/a 
    * compulsory
- Expiry_Date: Date
    - Validity: must be later than present
    - Permission: n/a
    - compulsory

Other fields:
- Question-Id = H(Question_Text, Question_Writer, Sig)

(** TODO: Check that this definition of question-id is consistent with ElectionGuard's contest-id, which is a hash of some election data.) 

- Background: string
    * Validity: character length
    * Permission: must be from the question-suggester
- MP_Who_Should_Ask_The_Questions: List(Entity)
    * Validity: must be MPs.  
    * Permission: n/a
- Entity_Who_Should_Answer_The_Question: List(Entity)
    * Validity: must be MPs, depts/portfolios, or public authorities
    * Permission: n/a
- Answer: List(string, answerer)
    * Validity: character length; answerer must match the sig.
    * Permission: must be from an MP 
- Answer_accepted: bool (default false)
    * Validity: n/a
    * Permission: must be from the question-suggester
- Hansard link: List(url)
    * Validity: domain must be aph.gov.au, parliament.vic.gov.au, etc. (preloaded permit-list - note that url sanitation is nontrivial).
    * Permissions: n/a
- Keywords: List(String)
    * Validity: short list of short words
    * Permission: n/a
- Category: List(Topics)
    * Validity: short list of pre-loaded topics
    * Permission: n/a
- Last_Update: BB_Index


The idea is that the BB_Index provides a link to the most recent update on the BB, which includes a signature and also a link to the prior most recent update. Thus anyone who wants to verify can iteratively retrieve all the updates on this question, at each step verifying the relevant signature, and then check that the composition of the updates matches the current announced state.


TODO: Think about whether signatures are a function of the underlying data structure, or of a particular update. Should a sig by the question-writer be a defining field of the initial question upload? Answer: a signature is a part of a BB upload, not an (explicit) part of the question.

TODO: Not clear whether we need keywords or topics.

(**VT: I would like a nice way to express the simple idea that you can change the 'answer accepted' bool from false to true, but not vice versa, and that this is an append-only-style operation, i.e. an 'or only' operation. Not sure of the most elegant way to express this.)

Also the neccessity to write a valid sig on your message is universal.  In this case the person uploading is supposed to put their name to a specific part of the data structure, so that requirement (which is usually ephemeral) imposes this permanent notion of validity on the database.


### Ballot

We will use the same ballot data structure as ElectionGuard.  (VT: Note, these have changed - get updates.) Something like this:

```javascript
ballot = {
    ballot_style: "ballot-style-1", 
    contests:
        [
            {
                object_id: "contest-1-id"
                ballot_selections:
                    [
                        {
                            object_id: "contest-1-yes-selection-id",
                            vote: 1
                        },
                        {
                            object_id: "contest-1-no-selection-id",
                            vote:0
                        }
                    ],
            }
        ]
}
```

**VT: the following are very negotiable, with the clear intention of making sure EG compatibility is easy, esp including John Caron's verifier**

The **contest-id** should be a hash of the question - H(Q).  We will only ever have two selections: up and down.  The selection IDs can therefore be very simply encoded using only one more bit (or perhaps an 'up' or 'down' string if that seems helpful). The hash should (perhaps) include the date, but should _not_ include other data such as links and tags, because these can change after the question is posted.

We won't need an explicit 'abstain' option - we'll be able to tally the upvotes and the downvotes (regardless of whether they are an explicit downvote or a swipe-aside).  Then it will be immediately evident how many votes there were with two zeros, since the overall total votes will be obvious.

**Question / thing to check: Can EG and/or JC's verifier aggregate some, but not necessarily all, contests on a ballot? And can it aggregate some, but not all, of the votes already received?** I assume the answer must be yes, because many US jurisdictions give slightly different ballots to different voters according to different addresses, but we may have an extreme version because each participant might vote on a completely different subset of questions. I think this effectively means each participant makes up their own "ballot-style."

We'll want to be able to take a _contest_ and choose to aggregate and decrypt 
its votes, which may be spread across a lot of different positions on a lot of different ballots.

Every submitted ballot is signed.  The hash of the ballot and its signature, H(B | Sig) is inserted in the Merkle Tree / BB.



### Tallies

A tally is:

- A claimed total,
- Decryption proofs from each trustee,
- A clear statement of which votes were aggregated.  (**Check how EG does this - or does it assume that you always want to decrypt everything?)

Again, this is hashed, stored in the database, and posted on the BB.

### Registration

A registration record is:

TODO: define the data structure for state (state, state electorate, federal electorate)

- A username,
- a public key,
- enumeration: Is_MP, Is_Org, Is_Public,
- (optionally) state or federal electorate(s),
- (Org or MP only) email domain (e.g. parliament.vic.gov.au or acf.org.au)

Again, this is hashed, stored in the database, and posted on the BB. Everything is public.

(VT: Consider what should happen when someone wants to register several different keys from different devices, or different people who represent the same MP.)