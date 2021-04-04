## Client API Draft
&nbsp;

### 1. Main Screen
The `Main Screen` is the first page that appears when the app is opened and contains a scrollable list of questions with options for sorting. On load or refresh, a batch of data will be synced to the phone.

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
1. An exact number of questions and their associated answers, or
2. A set of questions and answers within a specified date range
    * Using a date range risks displaying inconsistent numbers of questions

* *Question: The user is able to interact with the app in ways that may require data from periods that don't exist on the device. For example, clicking on a user's profile should display a list of all questions they have posted on the app. For the unregistered user, we may need to prevent their access to viewing users' accounts to avoid this issue, or display a message 'Register to view all questions posted by X'*
&nbsp;
> The local database is updated with a subset of,  
>* Questions
>* The selected questions' Answers
>* Users who have posted the selected Questions and their associated Answers

>If the user is able to draft a question before being prompted to register, the local database is also updated with the full set of,
>* Tags 
>* MPs & committees 

&nbsp;
___
```
3. POST /api/vote/{ballot}
```
Registered users can upvote or downvote questions in the list.

**TBC**
```
{

}
```

* *Question: Can a user change their vote?*
* *Question: Do we need to (optionally be able to) incorporate the user's electorate into their vote? Can an MP sufficiently say 'My electorate cares about this' if we only know the person who posted the question is in the electorate, but the votes are anonymous?*

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
* A Tag on a Question can be clicked on to filter Questions on the `Main Screen` by that Tag.
* An MP or Committee a Question is directed at can be clicked on to see the `Account Screen` of the MP or Committee.

&nbsp;
___
### 2. Question Screen

The `Question Screen` provides a detailed view of a Question where Answers and Question background are visible.

&nbsp;
___

```
1. POST /api/vote/{ballot}
``` 
A registered user can vote on a question. See `Main Screen [3]`

&nbsp;
___
```
2. POST /api/answer
```

An MP can type a response to a Question.  
```
{
    question: H(Q),
    answer: "Answer",
    user: "UserMP", 
    signature: sig(question, answer, user)
}
```


All users can add a Hansard link to a Question, indicating the Question was answered during Question Time

```
{
    question: H(Q),
    hansard: "www.link.com.au",
    user: "User",
    signature: sig(question, hansard, user)
}
```
> * The server will generate a `dateCreated` and `lastModified` timestamp for the Answer, and update  Question `H(Q)`'s `lastModifed` timestamp with the same value.

> * Inclusion on BB? **TBC**

> * The server returns the stored Answer object which is inserted into the local database and displayed in the `Question Screen` for Question `H(Q)`.

&nbsp;
___

```
Local Operations
```
* The User who posted a Question or Answer can be clicked on and their `Account Screen` displayed
