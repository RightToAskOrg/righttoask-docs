# Server API sketch

This file sketches the main ideas for a REST API for client-server interaction.  The key idea is to separate the data upload step from the inclusion-verification step.

We envisage a bulletin board (BB) which is rebuilt on a relatively slow schedule - think of an epoch as an hour or perhaps a day.  At the end of each epoch, the BB produces a new root hash, and is able to produce:

- a proof of inclusion of any data posted in the previous epoch, and
- a history proof (subtree proof) of inclusion of the prior epoch's root hash.

See these resources for [a good pictorial introduction to Merkle Trees and inclusion proofs](https://sites.google.com/site/certificatetransparency/log-proofs-work),  and [Crosby and Wallach's paper describing the original ideas](https://www.usenix.org/legacy/event/sec09/tech/full_papers/crosby.pdf).  

We will implement a Bulletin Board using the [rust Merkle Tree implementation by Andrew Conway](https:https://github.com/RightToAskOrg/bulletin-board-demo/). The server communicates directly with this BB, and offers a public interface for some of its operations.

The BB completes a tree and builds a **Published root** of a Merkle tree when requested by the server.  This ends an epoch (and starts a new one).

The BB has two classes of data, both represented by their hash values:

- **included values** are incorporated into a **published root**
- **pending values** are not yet included, but are promised to be in the next published root.

The BB can produce:

- the set of (hashes of) **pending values**
- the current **published root**
- a proof of inclusion, for any **included value**, wrt the **published root** (even if the value was included several iterations in the past)
- a history proof, for any prior **published root**, of its inclusion in the current **published root**

(VT Note/TODO: get precise BB API for inclusion and history proofs, in the style of these ones defined by Eleanor McMurtry [here](https://eleanorve.net/google-merkle-rs/google_merkle/struct.MerkleTree.html).  

For now, call them inclusionProof and historyProof.  These proofs work only on hashes of data, not on the posted data directly.

The main functionality of the rightToAsk client-server interaction is to post questions (and links, tags, or answers) or encrypted votes, and read others' questions and the decrypted tallies. A secondary function is to post and read public keys, for signing and verification of the uploaded data.  (At a later time, we may add public encryption keys for direct messages.) We also add verification of the BB state. 

(VT Note/TODO: Be consistent about whether a question or other data item is referred to by the hash of its data or the hash of its (data || sig).  (1) Consistency with Election Guard would be good, but (2) ease-of-use of BB would be good, which favours hashing (item+sig).  OTOH, if there are some items without sigs it might be annoying/complicated.)

## Main Data structures

**Questions: So far this completely omits data structures for key generation - TBA.  **

### Election Transcript
The election transcript consists of everything worth verifying:

- **Questions** including answers, directions, etc.
- **Ballots** which contain encrypted votes on questions
- **Tallies** i.e. decrypted aggregated votes on questions
- **Registrations** including a public key and name  

An **Entity** is either a department/ministerial portfolio (preloaded), a public authority (also preloaded, prob from RightToKnow), or a system user (an MP, registered citizen, or registered org rep). 

<a id="question_def"/>
### Question 

The contest-id=H(Q) will become the database index for that question, to which the rest of the database record is attached.

So a database record for a question will be:

- H(Q): index/hash
- Q: Question
- Question_Suggester: ID
- .... [Insert other data here: date, links, expl, tags, etc...]
- Signature (see above).

H(Q) is inserted into the Merkle tree / BB.

Validity: 

Compulsory fields: Question_Text, question-suggester, sig. Others, including lists, may be blank.

The permission and validity rules for each field are:

- Question_Text: string
    * Validity: character length
    * Permission: must be from the question-suggester
- Question_Suggester: Entity
    * Validity: must be a system user.
    * Permission: n/a 
- Background: string
    * Validity: character length
    * Permission: must be from the question-suggester
- Question_Askers: List(Entity)
    * Validity: must be MPs.  
    * Permission: n/a
- Question_Answerers: List(Entity)
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
- Topics: List(Topics)
    * Validity: short list of pre-loaded topics
    * Permission: n/a
- Signature: Sig
    * Must be a valid sig on all uploaded data with Question_Suggester's key.

Not clear whether we need keywords or topics.

(**VT: I would like a nice way to express the simple idea that you can change the 'answer accepted' bool from false to true, but not vice versa, and that this is an append-only-style operation, i.e. an 'or only' operation. Not sure of the most elegant way to express this.)

Also the neccessity to write a valid sig on your message is universal.  In this case the person uploading is supposed to put their name to a specific part of the data structure, so that requirement (which is usually ephemeral) imposes this permanent notion of validity on the database.


### Ballot

We will use the same ballot data structure as ElectionGuard.  (VT: Note, these have changed - get updates.) Something like this: @"{""ballot_style"":""ballot-style-1"",""contests"":[{""ballot_selections"":[{""object_id"":""contest-1-yes-selection-id"",""vote"":1},{""object_id"":""contest-1-no-selection-id"",""vote"":0}],""object_id"":""contest-1-id""},{""ballot_selections"":[{""object_id"":""contest-2-selection-1-id"",""vote"":1},{""object_id"":""contest-2-selection-2-id"",""vote"":0}],""object_id"":""contest-2-id""}],""object_id"":""ballot-id-123""}"; ;


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

- A username,
- a public key,
- boolean: Is_MP,
- boolean: Is_Org,
- (optionally) state or federal electorate(s),
- (optionally) email domain (e.g. parliament.vic.gov.au or acf.org.au)

Again, this is hashed, stored in the database, and posted on the BB.

(VT: Consider what should happen when someone wants to register several different keys from different devices, or different people who represent the same MP.)

## Post functions

Each upload is divided into two parts: data to be uploaded to the BB, and other optional metadata.  The BB data also needs the client's signature.  So a typical post, e.g. for registration, question-posting, or voting, has this structure:

**Post**

- D = data
- CSig = signature<sub>Client</sub>(data)
- M = metadata

This receives an immediate acknowledgement from the server, of the form:

**Ack**

- SSig = signature<sub>server</sub>(h(D, CSig))

where h indicates a cryptographic hash function (e.g. SHA256), for use in the BB proofs.  This is a promise from the server that D, CSig  (or, more precisely, h(D,CSig)) will be included on the BB.

The role of the metadata M is to allow the client to upload extraneous info to the server without that info being posted on the BB.

At this point, the data should appear in BB.get_pending_hash_values.

(VT: not 100% clear what the data format should be.  Ideally it should allow for easy verification later, when the items are included in a published root.)

The exact requirements for the data obviously depend on the specific kind of message. For registration, data would include a name, public key and (optionally) electorate.  For voting, data would include vote ciphertexts with sufficient extra data to identify which questions they were answering.  For question-asking, the data is quite complex and would include the text of the question, the ID of the person asking, any tags or links, etc.  We will also add some more functionality for answering questions, marking them as answered, re-tagging them for other MPs, etc...

### Specific POST functions

**New Question**

- D =  Question - see above.
- M =  List(Enc(address, MP public key))

Responses: 

- Ack (with sig, as above), 
- Validity failure (details), 
- Permission failure (details). 
- Duplicate failure (h).

The server applies question's [validity and permission rules](#question_def) (which should also be checked by the client). 

(VT: Consider exactly how perfectly equal a duplicate should need to be in order to be automatically excluded.  I think the same Question_Text except whitespace, and the same other data. In particular, even an identical question with different background should probably be allowed.)

M is empty if the user has not opted in to sharing their address with their MP, or if they have not tagged their MP as either a Question_Asker or Question_Answerer. Otherwise, M contains a list of ciphertexts containing the person's address, encrypted with the public encryption keys of each tagged MP.

(VT: TODO: resolve inconsistencies with registration data structures - atm we don't have public encryption keys, just digital sig keys, but we'll need them for this feature. Need to think/ask about multiple public keys for staffers associated with one MP.)

**Edit Question**

D includes:

- h: the hash used to identify the question, 
- Edits: a list of (field, value) pairs, where the field is an element of the [question data structure](**link) and the value is an update to be appended to the existing value. 

Responses: 

- Success (hash of D + server sig), 
- Auth Failure (you're not permitted to do this update, which may be either because you don't have permission to update that field, or there are already too many answers of that kind), 
- Merge failure (you need to manually resolve X - for example, if two people have simultaneously updated a field that can only have one element).

The server applies question's [validity and permission rules](#question_def) (which should also be checked by the client). 

(VT: Remember censorship when considering what conflicts with what - in some circumstances a moderator should be able to remove stuff. Definitely questions.  Possibly answers from MPs.)

Simultaneous update rules:

The merge rules for each field are:
- Question_Text, Question_Suggester, Signature: Reject updates.
- Background: Reject updates unless currently blank.
- Question_Askers, Question_Answerers: Eliminate duplicates (including with values already present). If the total number of values doesn't exceed the limit, accept. If the limit has already been exceeded, reject. If it hasn't, but would if this update was accepted, send a merge request back to the client (pick at most m out of the n you tried to submit...).  Note that this might cause cascading merges that need to be manually resolved, but that's less trouble than allowing locks.
- Answer: If there are simultaneous valid \& permitted updates, accept both (append), regardless of whether the MP is the person who was tagged.
- Answer_accepted: May be changed from false to true.
- Hansard link, Keywords, Topics: Same as Question_Askers, Question_Answerers.

**New Registration**

D includes:

- Name
- PK: public key
- (optional) electorate
- (optional) email domain

M includes:

- (optional) email name

**Edit Registration**

## Query functions

Query functions ask for current updates, since the last sync. The answers do not include proofs of proper inclusion, but do include enough information that, in future, the client will be able to verify that the replies are included in a published hash.  Some already have been; others are pending and will be published in the next one.

(VT: There should be some fairly standard ways to do this in an automatic way, which we could adopt. I've threaded (server) timestamps through it on the basis that that's probably a good way for the server to know what the client needs, but there may be better ways to do it.)  

The simplest query simply asks for everthing since the last query.

**Query update**

Input: prior_timestamp (of the last synch)

The server returns:

- current_timestamp
- Q = list of questions uploaded
- Q_Edits = list of edits (e.g. answers, links, new tags) to existing questions
- T = list of new tallies (which may be increments on previous tallies)
- Reg = list of new registrations    

since prior_timestamp. Plus:

- PR - most recent published root
- Pending - An indication of which of the returned values are still pending (i.e. not incorporated into PR)

Also SSig = signature<sub>server</sub>(h(Q | Q_Edits | T | Reg | PR | Pending))


**Query key**
Client sends:

- ID

Server returns:

- ID
- PK<sub>ID</sub> = the public key associated with that ID
- PR - most recent published root
- Pending (bool) - An indication of whether this value is still pending (i.e. not incorporated into PR)
- Ssig = signature<sub>server</sub>(h(ID,PK<sub>ID</sub>))

(**Question: Think about exactly what verification info we want with the PK - do we need the current root? Do we need the server to sign it? Should you get back either a sig or a BB inclusion proof depending on whether it has already been included?**)

(**Question: Earlier verisons had separate queries for questions/question_edits and for tallies.  I'm not sure this is useful, so I've deleted them. We could, however, consider various kinds of search-based updates, e.g. all the questions posted by one user, or for answers or tallies for the questions that you asked. This would be easy - the question is whether you would ever _not_ want everything else as well.**)

(**Question: Need to make it obvious/easy to check that something you were told is subsequently included. Need to think about the data structure a little.  It probably works out fine if we simply make a Merkle leaf out of each batch decryption - clients can then verify inclusion later, though they obviously can't verify if something was withheld.**)

(**Question: should a query answer include only the updates since the last epoch?  Or should it include the state as at the last BB update too?  If the latter, should it include an inclusion proof?  Should an explicit commitment to current state be part of each epoch's BB data? If so the answer to a query would be a proven state - as at the last epoch - plus an unproven current update.  Actually perhaps decoupling these is good - we say you can request a proven tally of the prior epoch (below), but separately (here) you can query without verification, including updates that aren't yet on the BB.**)

(**Question: we want a way to query earlier questions, e.g. for previous epochs, if the client has been offline for a while. We could implement this as either (1) amending the above query to include a root hash R, i.e. interpret this as a query for the questions since R, or (2) change the verification f'ns below so that rather than asking for something specific, you're simply asking for inclusion-proven list of all questions (or keys) between two updates.  (2) seems better. Which then means we need to consider completeness proofs, i.e. is it possible, without seeing the whole tree, to verify that you've seen _all_ the questions or all the decrypted tallies?  I assume we can do this simply with a counter, but it's not obvious.**)

(VT: TODO: When the querier is an MP, the server should also return the list of encrypted addresses for any questions tagged for that MP.)

## Verification
There are four different things a client may wish to verify (though the first two are very similar):

- that certain previously-posted data is included on the BB,
- that the root hash of a previous epoch is properly included in the current root hash,
- that a previously-given answer to a query is included on the BB (e.g., tallies, questions). 
- that the root hash is properly constructed from all posted data.

Let H = h(D) be some data previously posted to the BB. This could be something posted by a user (as h(D,CSig)), by the server (as a tally update) or by the trustees (e.g. decryption proof). The requester may know about it because they submitted it, or because they received it in response to a query (above).

### Verification data structures

**(See Eleanor's Rustdocs and equivalent for Andrew's BB)**

An inclusion proof is a list of hashes (and some metadata). The verifier checks that re-doing the tree construction using those hashes and its input, produces the expected root hash.  

**(VT: add history)**

### BB verification

The verification that the tallies are a valid decryption of the votes on the BB should be exactly the same as ElectionGuard.  **(Probably significant detail to go through carefully.)**


**Verify-inclusion**

The client's verify-inclusion query is to send H to the server.  The server responds with an 

- I = inclusionProof(H,R)

where R is the current root hash.

(**VT: Note: if I understand rightly, the BB abstracts for us whether your H is included directly in the current PR or indirectly in a PR from a few epochs ago.**)

(**VT: Note: We probably want a nice bulk way to verify the inclusion of everything you were told was pending.  Though of course it's completely fine if you can't do this until the whole new epoch's transcript is published, so the most efficient way to do it may simply be to download all the data for the just-finished epoch, check its proper formation, and then (plainly) check that it matches what you were told. VT(2) Actually this is possibly the most important thing, and is quite easy given that a query gives you the current root.  So there's an obvious local verification function in response to a query, which is to check that the complete included data in PR is (a) properly included in PR and (b) matches any 'pending' information you were given in response to earlier queries.**)

**Verify-history**

A client can request proof that earlier root hashes are properly-included subtrees of the current one. The client sends:

- R1, R2: two root hashes from different epochs

and the server returns

- Hist = historyProof(R1,R2)

or an error if R1, R2 are not valid root hashes, or R1 is not a subtree of R2.

If R2 is omitted, the server returns historyProof(R1,R) where R is the current root hash.

(**VT: More details here.  It occurs to me that the Root hash data probably needs some metadata, e.g. a sequence number, so you can tell which roots are supposed to be subtrees of which others.  Check what the BB does here.**)

**Verify-BB**

This function is intended to allow a complete download of the BB's contents, expecting that the client will want to verify all the vote aggregation and decryption as well.  Here we describe only the verification that the root hash is properly constructed.  Unlike all the other query functions, this function outputs data, not just the hashes.  The client sends:

- R1, R2: two root hashes from different epochs

and the server returns

- the complete BB contents between R1 and R2.

If R1 is omitted, the entire history since inception until R2 is returned.  If R2 is omitted, the current root hash is used.

There is no need for a history proof because the client can compute this themselves.

### Election Verification
(VT: TODO)

This will, as much as possible, match ElectionGuard's election verification, consisting of checking all the decryption proofs, vote aggregations, etc.

**Verify-crypto**
TODO


## Details and other questions
I'm not quite sure what M would be, but it seems a useful placeholder.  It is also possible that we should have a similar placeholder for the server's response.  e.g. it could tell you which epoch your data will appear in, to avoid ambiguity in the case where your upload occurred close to the boundary.

I've also generally left out data that didn't need to be there, such as the vote data already known to the client.  It's possible that it would be simpler to include this sometimes, rather than only the hash.

I have also omitted many of the details that need to be added for general good API design, such as a version number, to allow for later updates.

