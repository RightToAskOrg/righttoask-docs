## Table of contents
* [Index](https://righttoaskorg.github.io/righttoask-docs/index)
* [Features](https://righttoaskorg.github.io/righttoask-docs/Features)
* [Screens and Usage](https://righttoaskorg.github.io/righttoask-docs/ScreensAndUsage)
* [Security and privacy](https://righttoaskorg.github.io/righttoask-docs/SecurityAndPrivacy)
* [Direct messaging](https://righttoaskorg.github.io/righttoask-docs/DMs)
* [Discussion and further questions](https://righttoaskorg.github.io/righttoask-docs/DiscussionAndFurtherQuestions)
* [Prototype](https://righttoaskorg.github.io/righttoask-docs/Prototype)
* [API](https://righttoaskorg.github.io/righttoask-docs/API)

# General questions and discussion

## Which questions are good questions?

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

## Fairness among MPs

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

## Other possibly-useful features

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

## Desktop version

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

## Directing to journalists

Several interviewees suggested that journalists might actually find as
much value in these questions as MPs. Are there any changes we need to
make to encourage this? One obvious answer is for it to be less tightly
focused on parliamentary business.

### Ideas we considered but rejected

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

|:----------------|---------------:|
|[Back: Direct Messages](https://righttoaskorg.github.io/righttoask-docs/DMs) | | [Next: Prototype](https://righttoaskorg.github.io/righttoask-docs/Prototype)|



