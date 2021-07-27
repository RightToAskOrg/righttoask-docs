---
title: FAQ 
---

<a href="https://hackmd.io/peCERzhcRm-2HUtOGlgvRQ">
<div style="display: flex; align-items: flex-end; width=100%; background-color: #bb9cdb; justify-content: space-between">
    <img style="margin-left: 20px; height:80px" src="https://i.imgur.com/zbzGAzJ.png" />
    <p style="font: normal small-caps 900 16px sans-serif; color: white">
    Influence without Surveillance
    </p>
    <div style="clear:both;"></div>
</div>
</a>

## Question about the features

**Q:** How often should citizens be shown questions they haven't searched or asked for, or on topics they didn't select? It's important to count the people who were *not* interested in a question, and flicked it away without upvoting it. But showing people too many uninteresting questions may cause frustration. 
**A:** Actually it's probably fine to show people questions only in their field(s) of interest. There is still plenty of opportunity for them to express a lack of support for the particular question. Could also simply show how many people had viewed the question.

**Q:** Should non-MPs be able to comment on or answer others' questions? 
**A:** I think not, because the purpose is to connect MPs with constituents, not to encourage the constituents to argue amongst each other like they can on Twitter.

**Q:** Should citizens be directed to search through other questions with the same keywords before they pose a question? 
**A:** I think yes, so that they are encouraged not to duplicate a question already present. But not so much it irritates them.

**Q:** What is the right metric for popularity? Should it be what has the largest total votes, what has the largest fraction of upvotes per view, what has the most activity recently, or should these options all be available?

**Q:** Should MPs be able to contact citizens directly? 
**A:** I think yes. But perhaps only if the citizen is in their electorate, follows them, or directs a question at them. A: This is a fine default, but it should be user-configurable.

**Q:** Under what circumstances should citizens be able to message MPs? 
**A:** Technically, this is identical to MP-to-citizen DMs, but possibly needs to be restricted lest it become a source of un-aggregated info.

**Q:** Should the people who upvoted a question be notified when someone answers it, or only the person who asked it?
**A:** I think this should be configurable by the user. The question-asker should probably also be notified if lots of people upvote it.

**Q:** How exactly should the reject/disavow/re-tag functionality work? We don't want MPs to be unfairly embarrassed by questions that are not relevant to their responsibilities, but we also don't want to make it too easy to hide a valid and popular question.
**A:** Maybe direct it to someone else? Maybe just let it expire? Maybe write a short message explaining why you're not answering?

**Q:** How should the helpful re-tagging by other citizens work?
**A:** When you write a question, you decide whether it is available for open re-tagging or not.  If yes, others can add tags (maybe up to some predermined limit); if 'ask me' then others can suggest but the original question-asker has to approve them; if no, then no further tags can be added.  Examples: you may wish to direct a question to one entity only, not wanting to accept answers from others. Alternatively, you may welcome direction and not be certain where the question should go.  This may also help distinguish local from general issues, e.g. if multiple people ask their MP the same question - when is it a repeat of a national/state issue vs when is it separate local issues with similar text.

#### Onboarding and education questions

**Q:** People may decline to give their postcode for privacy reasons, but may not appreciate that most MPs are a lot more likely to respond to communication from constituents. What's the best way to explain the tradeoffs?*

**Q:** What would incentivise MPs to use the system?

**Q:** Which gamification options are likely to be effective for citizens without being too distracting from the main purpose?

**Q:** What feedback is useful to MPs? "Things can slip through the cracks".
**A:** The system could easily produce weekly counts of popular questions, both those that had been responded to and the rest; it could give notifications for those that are likely to expire, etc. Interesting to know how many followed a certain category / tag; how many questions were asked in each of those. How many different users. (i.e. distinguish one user asking lots of q'ns from broader participation). Some of these are easily computed from public information; others need aggregate decryption.


### Sorting, searching and following questions

**Q:** What should it mean to follow an MP? e.g. should you see all their answers?

**Q:** Should you be able to follow a committee or inquiry of interest? This may not be useful separately from the filtering feature.

**Q:** Should questions be allowed or obliged to have an expiry date? This could be very useful for those directed to specific hearings or inquiries.

**Q:** What kind of branding options are important for an MP's presence on the system?


# General questions and discussion

## Which questions are good questions?

Some tradeoffs, limitations, and imperfections are inherent to
democracy. These also apply to RightToAsk. What is the difference between what is popular and what is good? How do we distinguish a real expert from an opinionated amateur? If a political organisation works hard to get thousands of members to express a particular view, do we call that positive engagement or distortion? There are no complete answers, but some approaches are discussed here. 

Section [4](#sec:securityAndPrivacy){reference-type="ref"
reference="sec:securityAndPrivacy"} addresses the separate question of manipulation that is clearly intended to deceive, such as by registering thousands of bots, cracking in to the server to manipulate the tally, etc.

One way to identify a good question is to assess the person who posed it. RightToAsk lets people build a profile explaining their background and linking to other sites (such as a LinkedIn page or university web page). This may be relevant both for expertise (in the sense of research knowledge, relevant training *etc.*) or personal knowledge (*i.e.* direct experience of the matter in question). Of course, we cannot verify this information (though we can verify their email like we do for MPs, and use the same technique as Google Scholar to state, "Verified email at anu.edu" *etc.*).

#### Questions

-   *Question: Some sites, such as StackOverflow, leverage the reputation of the writer when assessing the value of a question. Should questions that come from citizens whose questions tend to be popular be more likely to appear in a citizen's feed? This may disadvantage people with specific expertise on a narrow topic, or important lived experience that is not widely shared. So there is an important requirement not to use the reputation system (if there is one) to reinforce existing biases about whose questions get heard.*

-   *Question: Should citizens be able to follow other citizens (or MPs), or search for questions asked by them?*

## Fairness among MPs

Should it be just for MPs, or also for candidates? My feeling is that candidates should be allowed to read and search (everyone is) but perhaps not answer. Ditto journalists.

Different MPs have very different resources and technical savvy---it is important for the system to be fair, and perceived as such, so that those with fewer staff are not unfairly disadvantaged. Perhaps it is better to emphasise an individual's responsiveness rather than a contest between them. 

It is also important that a few questions with no response do not
dominate a person's profile. The purpose is to focus attention on
important questions while (somewhat deliberately) leaving unimportant ones. An MP who receives and responds appropriately to many questions should not be embarrassed disproportionately by a few they have missed.

*Question: Should questions be filtered by time of asking? Should they disappear when they expire? (This might shift the incentive to strongly in favour of ignoring them.))*

## Other possibly-useful features

It can be easy for things to slip through the cracks, so it would be good if it produced weekly or fortnightly reports: "This many outstanding questions, tagged for you and/or your committee \..."

It would be useful to report on how many people followed a certain tag or person, or how many questions were asked in each of those. Also it would help to distinguish one person asking lots of questions from numerous contributors.

**Q:** which of the above could be harmlessly derived from public information and which require information upload, presumably aggregated for decryption?

## Desktop version

It is straightforward to make a read-only desktop version, incorporating searching, sorting, filtering by tags, etc.

However, allowing for secure decryption and signatures through the desktop environment is challenging. Desktop machines can send information (via QR code) to phones relatively easily, while the reverse transmission is difficult.

**Q:** Is it acceptable to users to have to hold their phone up to the screen and read a QR code when they want to read DMs or respond to questions? We could implement a batched signature, but batched decryption is harder. Or maybe we could make the ciphertext display as a QR code that was read by the phone.

## Directing to journalists

Several interviewees suggested that journalists might actually find as much value in these questions as MPs. Are there any changes we need to make to encourage this? One obvious answer is for it to be less tightly focused on parliamentary business.

### Ideas we considered but rejected

We considered an online *Leaderboard* in which the MPs who have answered the most questions, or picked up the most suggested questions, are displayed. However, this may be counterproductive---it is not entirely clear what the relevant statistic should be, given that different MPs will be asked different numbers of questions. Furthermore, it is difficult to make it fair in the context of very different levels of
staff---some MPs have numerous staff members constantly answering questions, while others are much more resource-constrained. Anyway it does not seem to be contributing directly to the core goals, which were to connect MPs with their constitutents, not to compare MPs against one another.

We also considered allowing people to register as interested in certain issues, but this may actually be unhelpful in understanding what they want. (For example, everyone says they are interested in the economy, but this is not very informative for understanding what policies they support or questions they want to ask.)

**Q:** should clicking on a tag associated with a committee or inquiry take you to that committee/inquiry homepage? Probably. Perhaps within the app so you can easily go back.

