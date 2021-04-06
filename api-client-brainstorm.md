## Client API Draft

This intention of this initial draft is to create a loose outline of the API requirements for the client app. Many aspects are subject to change and haven't been fully discussed or decided. All ammendments welcome.

&nbsp;
> All references to 'Tags' have been replaced with 'Topics' - just testing the less-social-media-y waters! 

&nbsp;
___
### Screens
&nbsp;
1. [Main Screen](#1-main-screen)  
2. [Question Screen](#2-question-screen)  
3. [Ask Screen](#3-ask-screen)  
4. [Account Screen](#4-account-screen)  
4. [Settings Screen](#5-settings-screen)  
4. [Registration Screen](#6-registration-screen)  
&nbsp;
___


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
>* Topics 
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
>* Topics 
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
    * filterable by electorate, topics, MP or committee directed at, answer status 
* A Question in the list can be clicked on for a detailed view, where Answers and Links are visible. See `Question Screen`.
* A Topic assigned to a Question can be clicked on to filter Questions on the `Main Screen` by that Topic. (VT: Good idea.)
* A Topic or set of Topics used to filter the `Main Screen` by can be followed and available via one's own `Account Screen`.
* An MP or Committee a Question is directed at can be clicked on to see the `Account Screen` of the MP or Committee.

&nbsp;

[To Top](#screens)
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
3. PATCH /api/{question}
``` 
An MP that has been identified as the recipient of a question may not believe they are the most appropriate person to be selected.  

An MP is able to remove themselves from being tagged by the Question.
```
{
    target: ""
}
```

An MP is able to select another MP for which the Question is more relevant.
```
{
    target: "AnotherMP"
}
```
* *Question: Could we offer a drop-down to allow the MP to explain the removal/reassignment? Perhaps this is easier than requesting a text-explanation. Eg. 'Not relevent to my portfolio', 'Question is not from my electorate'*
* *Question: Perhaps on reassignment, subject to question-asker approval, the Question will be removed from the MP's `Account Screen` and appear on the newly-tagged MP's `Account Screen`. Perhaps too complicated - what happens if the question-asker does not approve?*

&nbsp;
___

```
Local Operations
```
* The User who posted a Question or Answer can be clicked on and their `Account Screen` displayed

&nbsp;

[To Top](#screens)
___
## 3. Ask Screen
The `Ask Screen` is used to create a Question. It can be accessed via a navigation menu.  

*Question: We would like to encourage users to view Questions in a category before posting a question. Could we ask for the question topics and MP/committee in an initial screen, and provide an option for them to (for example) swipe up on a drawer at the bottom of the screen to 'See 10 questions about Covid' (like swiping up on an Instagram story to follow a link). When the MP is added, then it can update to 'See 5 questions about Covid for Scott Morrison'. The drawer can be swiped down and Question drafting resumed if nothing similar exists.*

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
    topics: ["One", "Two", "Three", "Four"...],
    target: "UserMP",
    user: "User", 
    signature: // TODO - for BB
}
```

> * The server will generate a `dateCreated` and `lastModified` timestamp for the Question on insertion into the db. An ID will be generated, `H(Q)`, and `upvotes` and `downvotes` set to `0`.  
> * The Question object is returned and inserted into the local db.

> * The server also returns an immediate acknowledgement (TODO) that the data will be included on the BB, without information that is subject to change (topics, target, background, backgroundLink)

> * The User is forwarded to `Question Screen` where their new Question is displayed.

* *Question: Are there a maximum number of topics allowed for a Question?*

* *Question: Should we have a 'Reason for Selection' dropdown for the MP who is targetted? Similar to the options provided for an MP to reject a question. Eg, 'X is my MP', 'X has a relevent portfolio'. It may make users be more thoughtful in their selection*


&nbsp;

[To Top](#screens)
___
## 4. Account Screen

The `Account Screen` displays User-provided information they have elected to share. A list of Questions asked by the User is also displayed. 
In the case of MPs, a list of Questions they have provided Answers to is also displayed.

___
```
Local Operations
``` 
* See list of followed Users, MPs, Committees
* See list of Topics followed
* Click on a User, MP or Committee and see their `Account Screen`
* Click on a Topic and be directed to the `Main Screen` filtered by the selected Topic
* Add a User, MP or Committee to your following list via their `Account Screen`

&nbsp;

[To Top](#screens)
___
## 5. Settings Screen

* *Question: Can electorates be modified after registration?*

```
1. POST /api/user/verify
```
An MP can provide their government email address (`@aph.gov.au`, `@parliament.vic.gov.au`...), which will be sent an email with a token they can use to verify their identity.

* *Question: Does the email send a token that is to be entered into the app for verification, or is it simply a link in their email inbox they have to click on which communicates with our server?*

```
{
    user: "UserMP",
    email: "usermp@parliament.vic.gov.au",
    signature: // TODO - for BB
}
```


&nbsp;
___
```
2. POST /api/user/delete
```
Any user can delete their account.
* *Question: When an account is deleted, do the questions remain? Is the username still assigned to those questions?*

```
{
    user: "User",
    signature: // TODO - for BB
}
```
> The User is redirected to the `Main Screen` and can view the app like an unregistered User.

&nbsp;

[To Top](#screens)
___
## 6. Registration Screen

After browsing the app in a limited capacity, the User is requested to register and create an account. 
* *Todo: Establish extent to which an unregistered User can browse and the points where they will be requested to register*

```
1. POST /api/user
``` 
Anyone can register to create an account.
> Postcode is not mandatory for registration


```
{
    username: "Username",
    postcode: "1234",
    publicKey: "5k8Yab",
    signature: // TODO - for BB
}
```

* *Question: We discussed with Nick how postcodes sometimes cross electorate boundaries - perhaps we could ask for postcodes at registration, then if they fall across multiple electorates create a notification on their* `Settings Screen` *that their electorate could not be established? We could also provide the option here to ask them to share location so we can determine electorate for them, if electorates can be modified after registration.* 

&nbsp;

[To Top](#screens)
___