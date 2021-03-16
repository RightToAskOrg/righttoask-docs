---
author:
- |
    Vanessa Teague[^1]\
    [vanessa\@thinkingcybersecurity.com](vanessa@thinkingcybersecurity.com)
    
title: |
    Right To Ask\
    Influence without Surveillance
---

Right To Ask Overview
=====================

Parliament is meant to represent the people, but it does not always work
as well as it should. Citizens want more input into the functions of
government between elections; parliamentarians, conversely, often
struggle to understand what their constituents want and how to represent
them.

*RightToAsk* lets citizens[^2] suggest and vote on questions, which
could be:

-   *directed to* an MP to ask for an answer, or

-   *suggested for* an MP to ask someone else.

*RightToAsk* shows parliamentarians which questions are popular and
relevant to their role. It is *informative*, making suggestions they may
not have thought of, and raising priorities they may not have been aware
so many people cared about.

These questions are meant to be asked in formal scenarios such as
Parliamentary committee hearings and question time, or answered in
written form in-app. We aim to open a channel of communication between
parliamentarians and citizens so that Parliament can be more directly
and immediately responsive to input from citizens. It is intended to
give citizens a way of putting things they care about on the agenda. It
is also a way of aggregating expertise, allowing large clusters of
citizens to amplify and support those whose insights are regarded as
valuable.

*RightToAsk* aims to improve efficiency in terms of time spent at both
ends: citizens can flick through a diverse list of questions and quickly
express their opinion by upvoting questions they want answered. If they
cannot find an existing question that reflects their priorities, they
can suggest a new one. MPs, too, can easily search for questions
directed at them or topics of interest and see a short, aggregated list
of relevant and popular questions.

*RightToAsk* does not attempt to hide who suggested which
questions---this is partly to disincentivise aggressive or threatening
ones.

The risk of profiling and manipulation is both a vulnerability in our
democracy and a disincentive for participation. RightToAsk uses
additive-homomorphic encryption to add votes without revealing how
individuals voted. It thus defeats political profiling and tracking,
rather like an electronic equivalent of putting everyone's vote into a
ballot box and counting them only when their link with the voter has
been broken.

Example scenarios
-----------------

Parliamentary Committee Members

:   can use *RightToAsk* to get expert suggestions for good questions.
    Suppose Senate Estimates wants to examine the effectiveness of a
    recently-built government app, but doesn't understand the app or its
    likely failures well enough to formulate effective questions.
    Knowledgeable technical people who have been examining the app can
    suggest important questions for the committee members to pose, and
    other citizens can vote them up so they receive attention.

MPs

:   can assess the importance of questions to their electorate. For
    example, if someone raises a question about an issue that matters to
    them, but nobody else upvotes it, then the MP can filter questions
    for their electorate alone and see that most of their constituents
    have flicked past it. Conversely, a new question that had received
    100% upvotes might deserve attention even if the total number of
    votes was small. The MP may answer the question directly or raise it
    in Parliament.[^3]

Journalists

:   and anyone else can adopt the questions for use in press conferences
    or any other setting.

We step away from the notion of 'voting on decisions' towards raising
awareness and asking questions about issues that seemed important to
lots of people. In particular, we do not work hard to distinguish
something with 51% support from something with 49% support - instead, we
try to raise up several issues, in the form of questions, that a large
number of people care about.

Each MP's contribution and responses will be public, both the number of
questions they have asked in parliament (as suggested by the platform)
and the number they have answered. The idea is to incentivise
participation by rewarding active participants with a public show of how
well they are doing their job of responding to the wishes of the
electorate.

Of course, MPs are also welcome to suggest questions to the electorate
for feedback.

Goals
-----

The primary goal is *meaningful information flow* from citizens to MPs.
This should be valuable and efficient at both ends.

The aim is to give MPs a succinct, clear list of most-popular questions,
rather than a deluge of thousands of emails which may be individually
considered or copy-pasted, and take time to assess.

We avoid AI and the consequent risks of algorithmic bias. Citizens do
the work of aggregating opinions and assessing others' suggestions, thus
providing a more trustworthy way of directing the most important
questions to MPs. (Although, of course, people can be biased too.)

RightToAsk also conveys what fraction of people saw the question and
*did not* upvote it, thus informing the MP if many people were *not*
interested.

Citizens are incentivised to participate by the satisfaction of having
their voices heard.

Features
========

Features for citizens
---------------------

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

Features for MPs
----------------

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
    who asked (see Section [5](#sec:DMs){reference-type="ref"
    reference="sec:DMs"});

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
    Maybe write a short message explaining why you're not answering?
    Perhaps the implementation of this is the same as (3).*

Accounts and roles
------------------

Organisations may also have accounts. These have the privileges of
citizens---they can pose and vote on questions, but not answer them.
However, the details of their account structure are more like an MPs, in
the sense that we seek some evidence that they actually represent their
claimed organisation, and allow multiple individuals to speak on their
behalf. See
Section [4.2](#subsec:identityAndAccountVerif){reference-type="ref"
reference="subsec:identityAndAccountVerif"} for more details.

Sorting, searching and following features
-----------------------------------------

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

Feedback features
-----------------

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

Civics and education features
-----------------------------

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

Screens and usage {#sec:screensUsage}
=================

The Registration screen

:   invites a user to choose a name and (optionally) state their
    postcode. This also generates a cryptographic key pair.

The Main screen

:   shows the list of current questions and allows search, filter, sort,
    *etc.* Voters are invited to up-vote or flick past (or possibly
    explicitly downvote) questions. Voting is immediate, while asking a
    question requires clicking on a specific icon. It is also possible
    to report a question as abusive.

    Clicking on the person takes you to their account screen. Clicking
    on a question takes the user to:

the Question screen

:   which allows for the addition of extra background information, links
    to Hansard, tag viewing, *etc.* Both questions and background
    information are character-limited.

The Account settings and verification screen

:   allows an MP to verify a parliamentary email address---the domains
    of Australian state and federal parliaments are hardcoded. For other
    organisations, it allows a person to verify that they can access
    email at a domain that matches the claimed website.

    This screen also allows settings for the externally-visible account
    screen, including aesthetic settings (photo uploads, colour schemes)
    and privacy settings (whether the account accepts DMS from nobody,
    from those they've followed or DM'd, from MPs, or from nobody).

    Some corporate or MP accounts (or possibly even some individual
    accounts with multiple devices) may register multiple public
    keys---this means that multiple people may speak for the group.

The Account screen

:   shows the information about the account that that entity (MP,
    citizen, organisation) has chosen to display, along with a list of
    their questions.

*Question: Should clicking on a tag associated with a committee or
inquiry take you to that committee/inquiry homepage? Probably. Perhaps
within the app so you can easily go back.*

Format and function details are described in the spec.

Security and privacy {#sec:securityAndPrivacy}
====================

RightToAsk incorporates the ElectionGuard end-to-end verifiability
library to aggregate votes before the total is decrypted, and to prove
that even the system administrators cannot artificially inflate or
deflate the popularity of questions.

We aim for *participation privacy* as well as the privacy of up or down
votes. That is, it should not be possible to detect which users have
rated which questions. We also want people to be able to verify proper
inclusion of their votes, and to verify proper tallying of those
questions they are interested in.

What we ask people to share
---------------------------

Optionally, people may state the electorate they live in. [^6] This
allows MPs (and everyone else) to filter based on their own electorate.

I see no reason to ask for demographic information, except possibly to
understand who is $<18$ and who isn't.

-   *Question: What is the minimum group size to allow for aggregation,
    in order to be fairly confident of not violating individual privacy?
    This is complicated by aggregation in other dimensions, such as time
    and electorate.*

-   *Question: Are there extra privacy rules for participants under 18?
    Certainly in the EU there are - not sure about Aus.*

Identity and account verification {#subsec:identityAndAccountVerif}
---------------------------------

### MPs

MPs are relatively easy to verify using their parliamentary email. We
can do the traditional/standard sending of some secret code to that
email address, and use it at registration time. This proves that the
person registering has access to the official email account.

-   *Question: How are these answered in practice? Is there one account
    or device on which they're read, or are there multiple people with
    access?*

-   *Question: How should RightToAsk account access be organised for
    staffers? Do different staff take responsibility for different
    aspects,*e.g.* some for committee questions and others for
    constituent matters?*

### Citizens

Detecting completely fake accounts, and distinguishing them from a
signup drive from a legitimate source, is really important but very
hard. Maybe have a new user badge (because that might be a nice person
to engage with, but it might also be grounds for suspicion because not
actually a real person).

How do we check whether the person really does live in the electorate?
My suggestion is that by default we don't, though I think it would be
good to add a feature where a person who has visited their MP (at a
public meeting or whatever) could be certified as living there.

*Detail: Could we possibly use mailouts, e.g. by MPs to constituents or
from electoral Commissions, with unique random num's? The assumption
would be that if you can pick up that person's mail then you must be
that person. Not perfect, but a decent deterrence of widespread fake
registration. Perhaps when people sign up they could apply for such a
thing if their MP joins in? This would cost a postage stamp of course.*

*Question: Can you be endorsed by an MP who doesn't represent you, i.e.
in an electorate that isn't yours? My feeling is no, but maybe if you
move you should be allowed to change electorates without needing to be
re-endorsed.*

Should you be allowed to use a pseudonym? My feeling is yes, but know
that you're easily re-identified.

Should you be allowed to write a nice profile/summary of yourself? My
feeling is yes, probably more than Twitter allows, and links to
professional/scholarly/other websites. But note we will not verify this
information.

Perhaps implement a signal-like way to check your friend's key? And/or
integrate with other systems such as Signal, Apple, Keybase,*etc.*

We could optionally allow people to secret-share their private key with
friends (or authorities?) for recovery.

### Organisations

It would be valuable to be able to identify key stakeholders, e.g. that
the person who claims to be writing on behalf of an organisation really
does speak for it. So for example domain names could be required to
match email addresses for orgs. So perhaps we have, say, a profile
screen where an org can state their website, and then we verify that
their email address has the same domain (the same way we verify MPs'
emails, but with the domain they claimed). It's not perfect, and it
doesn't stop you registering
"mydodgyfakeoftheaustralianconservationfoundation.com" but at least it
gives other users a chance to check their website.

Detecting completely fake accounts, and distinguishing them from a
signup drive from a legitimate source, is really important but very
hard. Maybe have a new user badge (because that might be a nice person
to engage with, but it might also be a sign of being not actually a real
person).

Possible extra feature: Direct Messages {#sec:DMs}
=======================================

The system will use its PKI for end-to-end encrypted Direct messages
(DMs).

Default behaviour: an MP can reply (by DM) to any message tagged for
them; a citizen can reply (by DM) to any DM. Of course, these defaults
can be edited to allow more or less receptive DM behaviour.

*Question: Do we have to do anything as complicated as Signal-style
ratcheting, or can we simply use noninteractive DH like COVIDSafe? i.e.
is one PK operation per DM tolerable or not? Admittedly it doesn't have
forward secrecy if the receiver's key is compromised. Or is there a
forward-secure version like TOR in which you use your signing key to
send the $g^a$ and $g^b$ msgs? But then maybe everyone needs to be
online? But then maybe everyone is always online now. Needs more
thought. I'm inclined to go for vanilla authenticated key exchange
(which only has to be authenticated one way) using persistent keys to
authenticate ephemeral keys, generated freshly for each exchange (e.g.
after you've paused for a few mins, or maybe after you turn off the app?
Investigate non-permanent secure storage).*

*Question: Maybe MPs should only accept DMs from verified accounts?*

*Question: Perhaps we should just use PGP mail?*

General questions and discussion
================================

Which questions are good questions?
-----------------------------------

Some tradeoffs, limitations, and imperfections are inherent to
democracy. These also apply to RightToAsk. What is the difference
between what is popular and what is good? How do we distinguish a real
expert from an opinionated amateur? If a political organisation works
hard to get thousands of members to express a particular view, do we
call that positive engagement or distortion? There are no complete
answers, but some approaches are discussed here.

Section [4](#sec:securityAndPrivacy){reference-type="ref"
reference="sec:securityAndPrivacy"} addresses the separate question of
manipulation that is clearly intended to deceive, such as by registering
thousands of bots, cracking in to the server to manipulate the tally,
etc.

One way to identify a good question is to assess the person who posed
it. RightToAsk lets people build a profile explaining their background
and linking to other sites (such as a LinkedIn page or university web
page). This may be relevant both for expertise (in the sense of research
knowledge, relevant training *etc.*) or personal knowledge (*i.e.*
direct experience of the matter in question). Of course, we cannot
verify this information (though we can verify their email like we do for
MPs, and use the same technique as Google Scholar to state, "Verified
email at anu.edu" *etc.*).

#### Questions

-   *Question: Some sites, such as StackOverflow, leverage the
    reputation of the writer when assessing the value of a question.
    Should questions that come from citizens whose questions tend to be
    popular be more likely to appear in a citizen's feed? This may
    disadvantage people with specific expertise on a narrow topic, or
    important lived experience that is not widely shared. So there is an
    important requirement not to use the reputation system (if there is
    one) to reinforce existing biases about whose questions get heard.*

-   *Question: Should citizens be able to follow other citizens (or
    MPs), or search for questions asked by them?*

Fairness among MPs
------------------

Should it be just for MPs, or also for candidates? My feeling is that
candidates should be allowed to read and search (everyone is) but
perhaps not answer. Ditto journalists.

Different MPs have very different resources and technical savvy---it is
important for the system to be fair, and perceived as such, so that
those with fewer staff are not unfairly disadvantaged. Perhaps it is
better to emphasise an individual's responsiveness rather than a contest
between them.

It is also important that a few questions with no response do not
dominate a person's profile. The purpose is to focus attention on
important questions while (somewhat deliberately) leaving unimportant
ones. An MP who receives and responds appropriately to many questions
should not be embarrassed disproportionately by a few they have missed.

*Question: Should questions be filtered by time of asking? Should they
disappear when they expire? (This might shift the incentive to strongly
in favour of ignoring them.))*

Other possibly-useful features
------------------------------

It can be easy for things to slip through the cracks, so it would be
good if it produced weekly or fortnightly reports: "This many
outstanding questions, tagged for you and/or your committee \..."

It would be useful to report on how many people followed a certain tag
or person, or how many questions were asked in each of those. Also it
would help to distinguish one person asking lots of questions from
numerous contributors.

*Question: Which of the above could be harmlessly derived from public
information and which require information upload, presumably aggregated
for decryption?*

Desktop version
---------------

It is straightforward to make a read-only desktop version, incorporating
searching, sorting, filtering by tags, etc.

However, allowing for secure decryption and signatures through the
desktop environment is challenging. Desktop machines can send
information (via QR code) to phones relatively easily, while the reverse
transmission is difficult.

-   *Question: Is it acceptable to users to have to hold their phone up
    to the screen and read a QR code when they want to read DMs or
    respond to questions? We could implement a batched signature, but
    batched decryption is harder. Or maybe we could make the ciphertext
    display as a QR code that was read by the phone.*

Directing to journalists
------------------------

Several interviewees suggested that journalists might actually find as
much value in these questions as MPs. Are there any changes we need to
make to encourage this? One obvious answer is for it to be less tightly
focused on parliamentary business.

Ideas we considered but rejected
================================

We considered an online *Leaderboard* in which the MPs who have answered
the most questions, or picked up the most suggested questions, are
displayed. However, this may be counterproductive---it is not entirely
clear what the relevant statistic should be, given that different MPs
will be asked different numbers of questions. Furthermore, it is
difficult to make it fair in the context of very different levels of
staff---some MPs have numerous staff members constantly answering
questions, while others are much more resource-constrained. Anyway it
does not seem to be contributing directly to the core goals, which were
to connect MPs with their constitutents, not to compare MPs against one
another.

We also considered allowing people to register as interested in certain
issues, but this may actually be unhelpful in understanding what they
want. (For example, everyone says they are interested in the economy,
but this is not very informative for understanding what policies they
support or questions they want to ask.)

[^1]: Many students also contributed to this design, including: Ishan
    Goyal, Chuanyuan Liu, Lilli McCann, Eleanor McMurtry, Hanna Navissi
    and Miguel Wood

[^2]: The term "citizen" is used here to emphasise the active
    participation in a democratic process, though users may of course be
    permanent residents, under-18s or other non-Australian-citizens. The
    term "MP" includes senators and members of state legislative bodies.

[^3]: The Victorian Parliament has recently introduced a special session
    for constituent questions:
    <https://www.parliament.vic.gov.au/about/news/2458-constituency-questions-introduced>

[^4]: Perhaps restricted to .gov.au sites?

[^5]: Filter is not functionally different from search

[^6]: In Victoria, all state electorates are subsets of federal
    electorates, but in other Australian states this is not guaranteed.
    This matters for privacy because there may be only a few people in
    the intersection of two (state and federal) electorates, so tallying
    of those subsets may reveal individual votes.
