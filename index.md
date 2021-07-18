## Table of contents
* [Index](https://righttoaskorg.github.io/righttoask-docs/index)
* [Features](https://righttoaskorg.github.io/righttoask-docs/Features)
* [Screens and Usage](https://righttoaskorg.github.io/righttoask-docs/ScreensAndUsage)
* [Security and privacy](https://righttoaskorg.github.io/righttoask-docs/SecurityAndPrivacy)
* [Direct messaging](https://righttoaskorg.github.io/righttoask-docs/DMs)
* [Discussion and further questions](https://righttoaskorg.github.io/righttoask-docs/DiscussionAndFurtherQuestions)
* [Prototype](https://righttoaskorg.github.io/righttoask-docs/Prototype)
* [API](https://righttoaskorg.github.io/righttoask-docs/API)

# Right To Ask

Parliament is meant to represent the people, but it does not always work
as well as it should. Citizens want more input into the functions of
government between elections; parliamentarians, conversely, often
struggle with a deluge of messages that do not give a clear picture of 
what their constituents want or how to represent them.

*RightToAsk* lets citizens[^1] suggest and vote on questions, which
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

## Example scenarios

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
    in Parliament.[^2]

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

## Goals

The primary goal is *meaningful information flow* from citizens to MPs.
This should be valuable and efficient at both ends.

The aim is to give MPs a succinct, clear list of most-popular questions,
rather than a deluge of thousands of emails which may be individually
considered or copy-pasted, and take time to assess.

We avoid AI and the consequent risks of algorithmic bias. Citizens do
the work of aggregating opinions and assessing others' suggestions, thus
providing a more trustworthy way of directing the most important
questions to MPs (although, of course, people can be biased too).

RightToAsk also conveys what fraction of people saw the question and
*did not* upvote it, thus informing the MP if many people were *not*
interested.

Citizens are incentivised to participate by the satisfaction of having
their voices heard.


<div style="text-align: right"> <a href="https://righttoaskorg.github.io/righttoask-docs/Features">Next: Features</a> </div>

*****

[^1]: The term "citizen" is used here to emphasise the active
    participation in a democratic process, though users may of course be
    permanent residents, under-18s or other non-Australian-citizens. The
    term "MP" includes senators and members of state legislative bodies.

[^2]: The Victorian Parliament has recently introduced a special session
    for constituent questions:
    <https://www.parliament.vic.gov.au/about/news/2458-constituency-questions-introduced>

