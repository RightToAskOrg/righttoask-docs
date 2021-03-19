# Features

## Features for citizens

Ordinary users can:

Ask a question

:   

Direct a question to a particular MP or committee

:   

Tag a question with a topic or keyword

:   

Add an explanation or background link

:   e.g. to a bill[^4]

Upvote or downvote/flick a question

:   

Attach a link to Hansard

:   where a question was asked or answered

Search questions

:   by tag, committee, or MP

Sort questions

:   by popularity

Filter questions

:   by electorate, answer status[^5]

Follow another citizen

:   who may or may not be an MP.

## Features for MPs

MPs can do everything that other citizens can do, and also respond to
questions, whether those directed to them or to other MPs. There are
several ways to respond to a question:

use the question

:   by posing it to someone in a commmittee or other hearing, thus
    allowing a link to Hansard or the online recording to be added;

comment on a question

:   or on an answer or comment from another MP;

answer a question publicly via RightToAsk,

:   which generates a notification to the person who asked it;

ask it in a confidential parliamentary setting

:   and make a (public) response to say that the matter was raised in a
    confidential context and will be considered in the committee's final
    report;

answer it privately by DM

:   generally for private questions only of interest to the individual
    who asked (see [Direct Messages](https://righttoaskorg.github.io/righttoask-docs/DMs);

Reject / disavow / re-tag the question

:   if the question should be asked elsewhere.

MPs generally told us that they would value---and respond to---questions
only if they

-   came from their electorate, or

-   related to their portfolios (in the case of ministers) and came from
    the relevant state (in the case of State MPs), or

-   related to their committee responsibilities.

The aim is to streamline this at both ends, both making it easy for MPs
to identify relevant questions with high support (including high support
within their constituency if relevant) and also easy for citizens to
understand how to direct their questions in a way that makes them more
likely to have influence.

#### Functionality questions - citizens and MPs

-   *Question: How often should citizens be shown questions they haven't
    searched or asked for, or on topics they didn't select? It's
    important to count the people who were *not* interested in a
    question, and flicked it away without upvoting it. But showing
    people too many uninteresting questions may cause frustration. A:
    Actually it's probably fine to show people questions only in their
    field(s) of interest. There is still plenty of opportunity for them
    to express a lack of support for the particular question. Could also
    simply show how many people had viewed the question.*

-   *Question: Should non-MPs be able to comment on or answer others'
    questions? I think not, because the purpose is to connect MPs with
    constituents, not to encourage the constituents to argue amongst
    each other like they can on Twitter.*

-   *Question: Should citizens be directed to search through other
    questions with the same keywords before they pose a question? I
    think yes, so that they are encouraged not to duplicate a question
    already present. But not so much it irritates them.*

-   *Question: What is the right metric for popularity? Should it be
    what has the largest total votes, what has the largest fraction of
    upvotes per view, what has the most activity recently, or should
    these options all be available?*

-   *Question: Should MPs be able to contact citizens directly? I think
    yes---see Section [5](#sec:DMs){reference-type="ref"
    reference="sec:DMs"} on direct messages (DMs). But perhaps only if
    the citizen is in their electorate, follows them, or directs a
    question at them. A: This is a fine default, but it should be
    user-configurable.*

-   *Question: Under what circumstances should citizens be able to
    message MPs? Technically, this is identical to MP-to-citizen DMs,
    but possibly needs to be restricted lest it become a source of
    un-aggregated info.*

-   *Question: Should the people who upvoted a question be notified when
    someone answers it, or only the person who asked it? A: I think this
    should be configurable by the user. The question-asker should
    probably also be notified if lots of people upvote it.*

-   *Question: How exactly should the reject/disavow/re-tag
    functionality work? We don't want MPs to be unfairly embarrassed by
    questions that are not relevant to their responsibilities, but we
    also don't want to make it too easy to hide a valid and popular
    question. Maybe direct it to someone else? Maybe just let it expire?
    Maybe write a short message explaining why you're not answering?*

## Accounts and roles

Organisations may also have accounts. These have the privileges of
citizens---they can pose and vote on questions, but not answer them.
However, the details of their account structure are more like an MPs, in
the sense that we seek some evidence that they actually represent their
claimed organisation, and allow multiple individuals to speak on their
behalf. See [Security and Privacy](https://righttoaskorg.github.io/righttoask-docs/SecurityAndPrivacy) for more details.

## Sorting, searching and following features

You can *search* the contents of questions, *follow* a person (who may
be an MP, organisation or other citizen) or *filter* by question
metadata such as tags and answer status. Every MP, committee and inquiry
has standardised tags. MPs and citizens may also generate their own
tags.

Questions can be **sorted**

-   by *popularity*, i.e. the total number of upvotes;

-   by *proportional popularity*, i.e. the total fraction of upvotes per
    citizen who viewed it;

-   by *recent popularity*, i.e. the number or fraction of upvotes in
    the last day or hour;

-   or by a weighted combinaton of the above.

Subject to privacy requirements (that there is a minimum number of
respondents from the electorate), both of these sorts can run within a
certain constituency, allowing MPs (and anyone else) to assess the
popularity of a question to their own constituents.

-   *Question: What kind of branding options are important for an MP's
    presence on the system?*

#### Sorting, searching and following questions

-   *Question: What should it mean to follow an MP? e.g. should you see
    all their answers?*

-   *Question: Should you be able to follow a committee or inquiry of
    interest? This may not be useful separately from the filtering
    feature.*

-   *Question: Should questions be allowed or obliged to have an expiry
    date? This could be very useful for those directed to specific
    hearings or inquiries.*

## Feedback features

The best and most positive kind of feedback will be to have suggested
(or voted on) a question that is subsequently asked in a committee or
meaningfully answered by the MP. This can be emphasised in several ways.

-   A notification if a question you asked is answered or asked in
    Parliament.

-   The same, when you upvoted it. (Note however that this would require
    local storage of which questions you voted on.)

There are also a number of ways we could offer rewards to those who
suggested popular questions.

-   Electronic rewards or prizes for asking your first question, getting
    at least 50 votes on a question, etc.

-   Notifications when other people upvote your questions.

-   Leaderboards for people who have cast the most votes?

#### Feedback questions

-   *Question: What would incentivise MPs to use the system?*

-   *Question: Which gamification options are likely to be effective for
    citizens without being too distracting from the main purpose?*

-   *Question: What feedback is useful to MPs? "Things can slip through
    the cracks." The system could easily produce weekly counts of
    popular questions, both those that had been responded to and the
    rest; it could give notifications for those that are likely to
    expire, etc. Interesting to know how many followed a certain
    category / tag; how many questions were asked in each of those. How
    many different users. (i.e. distinguish one user asking lots of q'ns
    from broader participation). Some of these are easily computed from
    public information; others need aggregate decryption.*

## Civics and education features

State and federal electoral commissions and parliaments have online
features for helping citizens find their electorate and representatives.
However, these can be challenging to navigate for people who are not
already familiar with how Australia's political systems work.

RightToAsk provides an accessible way for citizens to look up their
representatives, at the time they register. They are asked (optionally)
for a postcode, which is then used to assess who their representatives
are. They are then asked if they would like to follow their state and
federal representatives.

#### Onboarding and education questions

-   *Question: People may decline to give their postcode for privacy
    reasons, but may not appreciate that most MPs are a lot more likely
    to respond to communication from constituents. What's the best way
    to explain the tradeoffs?*

|:----------------|---------------:|
|[Back: Overview](https://righttoaskorg.github.io/righttoask-docs/) | [Next: Screens and Usage](https://righttoaskorg.github.io/righttoask-docs/ScreensAndUsage)|
