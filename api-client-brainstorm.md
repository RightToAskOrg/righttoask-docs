## Client API Draft
&nbsp;

## 1. Main Screen
The `Main Screen` is the first page that appears when the app is opened and contains a scrollable list of questions with options for sorting and filtering. On load or refresh, a batch of data will be synced to the phone.

> Locally stored variables used:
>* `RightToAsk-Username` 
>* `RightToAsk-LastSync` 

&nbsp;
___
```
1. GET /api/sync/{lastSync}
```
If the user already has an account (`RightToAsk-Username`) a timestamp (`RightToAsk-LastSync`) will be used to determine the download period. 

The server responds with all entities that have a `lastModified` stamp between 
`RightToAsk-LastSync` and `now`.

> The local database is updated with new or modified entities,  
>* Questions
>* Answers
>* Users who have posted Questions or Answers
>* Tags 
>* MPs & Committees 

&nbsp;
* *Question: Should the older, locally stored data be cleared after time period passes or storage amount is reached?*
* *Question: If the data since lastSync is greater than a determined size, should we restrict the returned data to be from currentDate -> moreRecentPeriod? For now perhaps assume we take everything, otherwise the client will have to handle knowing which periods data exists for & which other periods a remote fetch will need to be made.*

&nbsp;
___
```
2. GET /api/sync
```

If the user does not have an account, a subset of recent questions are synced which the user can browse and view the details of before being asked to register.

The server responds with,
1. An exact number of questions and their associated answers and current tallies, or
2. A set of questions, answers and tallies within a specified date range
    * Using a date range risks displaying inconsistent numbers of questions

* *Question: The user is able to interact with the app in ways that may require data from periods that don't exist on the device. For example, clicking on a user's profile should display a list of all questions they have posted on the app. For the unregistered user, we may need to prevent their access to viewing users' accounts to avoid this issue, or display a message 'Register to view all questions posted by X'  
VT: I think it's OK to read state from before you joined the system, though I certainly agree that we don't want massive initial downloads of the complete history of everything.  Also note there may be updated answers or tallies from questions that were asked quite a long time ago, but are still being actively upvoted and/or answered. So possibly we want a notion of questions being still active or expired (should they have expiry dates?) and also perhaps we want the option to download some history (e.g. a specific person's questions) from before you joined.  
HN: I think you're right, this probably isn't such a big issue due to the fact that we don't allow regular users to comment on each other's questions. This somewhat restricts how deeply we would need to follow/expand users to ensure all possible paths from a Question -> user's Question list -> another Question have been accounted for.*
&nbsp;
> The local database is updated with a subset of,  
>* Questions
>* The selected questions' Answers and current tallies
>* Users who have posted the selected Questions and their associated Answers

> The local database is also updated with the full set of,
>* Tags 
>* MPs & committees 
whether or not the user has registered.

&nbsp;
___
```
3. POST /api/vote
```
Registered users can upvote or downvote questions in the list.

**TODO**
```
{

}
```

* *Question: Can a user change their vote?  
VT: No, that goes into the too-hard box, probably forever.  
HN: We should probably make an effort to ensure the upvote/downvote buttons aren't too close to each other and also aren't in places where people normally place fingers to scroll :)*
* *Question: Do we need to (optionally be able to) incorporate the user's electorate into their vote? Can an MP sufficiently say 'My electorate cares about this' if we only know the person who posted the question is in the electorate, but the votes are anonymous? VT: I think yes - a person should optionally be able to state their electorate when they register, which then becomes part of their public profile (along with their public key).  Then, when we aggregate and tally, we can do sub-tallies by electorate.  Of course, we need to be extra careful about privacy if the sets are small.*

&nbsp;
___
```
Local Operations
```
* The list of questions on the `Main Screen` is,
    * able to be sorted by certain parameters, eg. recently posted, trending, popularity,
    * searchable by key words via a text box,
    * filterable by electorate, topic tag, MP or committee directed at, answer status 
* A Question in the list can be clicked on for a detailed view, where Answers and Links are visible. See `Question Screen`.
* A Tag on a Question can be clicked on to filter Questions on the `Main Screen` by that Tag. (VT: Good idea.)
* An MP or Committee a Question is directed at can be clicked on to see the `Account Screen` of the MP or Committee.

&nbsp;
___
## 2. Question Screen

The `Question Screen` provides a detailed view of a Question where Votes, Answers and provided background are visible.

&nbsp;
___

```
1. POST /api/vote
``` 
A registered user can vote on a question. See `Main Screen [3]`

&nbsp;
___
```
2. POST /api/answer
```
> `H(Q)` is the index of question Q  

An MP can type a response to a Question.  

```
{
    question: H(Q),
    answer: "Answer",
    user: "UserMP", 
    signature: // TODO - for BB
}
```


All users can add a Hansard link to a Question, indicating the Question was answered during Question Time or in a Committee.

```
{
    question: H(Q),
    hansard: "link.aph.gov.au",
    user: "User",
    signature: // TODO - for BB
}
```
> * The server will generate a `dateCreated` and `lastModified` timestamp for the Answer on insertion into the db and update  Question `H(Q)`'s `lastModifed` timestamp with the same value.  

> * The server returns an immediate acknowledgement (TODO) that the data will be included on the BB.

> * The server returns the stored Answer object which is inserted into the local database and displayed in the `Question Screen` for Question `H(Q)`.

&nbsp;
___

```
Local Operations
```
* The User who posted a Question or Answer can be clicked on and their `Account Screen` displayed

&nbsp;
___
## 3. Ask Screen
The `Ask Screen` is used to create a Question. It can be accessed via a navigation menu.  

*Question: We would like to encourage users to view Questions in a category before posting a question. Could we ask for the topic tags and MP/committee in an initial screen, and provide an option for them to (for example) swipe up on a drawer at the bottom of the screen to 'See 10 questions about Covid' (like swiping up on an Instagram story to follow a link). When the MP is added, then it can update to 'See 5 questions about Covid for Scott Morrison'. The drawer can be swiped down and Question drafting resumed if nothing similar exists.*
&nbsp;
___

```
1. POST /api/question
``` 
A registered user can ask a question.

```
{
    question: "Question",
    background: "Context",
    backgroundLink: "www.context.com",
    tags: ["One", "Two", "Three", "Four"...],
    target: "UserMP",
    author: "User", 
    signature: // TODO - for BB
}
```

> * The server will generate a `dateCreated` and `lastModified` timestamp for the Question on insertion into the db. An ID will be generated, `H(Q)`, and `upvotes` and `downvotes` set to `0`.  
> * The Question object is returned and inserted into the local db.

> * The server also returns an immediate acknowledgement (TODO) that the data will be included on the BB, without information that is subject to change (tags, target, background, backgroundLink)

> * The User is forwarded to `Question Screen` where their new Question is displayed.

* *Question: Are there a maximum number of tags allowed on a Question?*
