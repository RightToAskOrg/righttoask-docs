---
title: Security and Privacy
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

## Security and privacy

RightToAsk incorporates the [ElectionGuard end-to-end verifiability library](https://github.com/microsoft/electionguard) to aggregate votes before the total is decrypted, and to prove that even the system administrators cannot artificially inflate or deflate the popularity of questions. 

The decryption keys are secret-shared among four decryption servers.
This means that individual votes remain private, even from RightToAsk's administrators, unless three of the four decryptors collude.

Citizens can also verify proper inclusion of their votes, and anyone can verify proper tallying of those questions they are interested in.

Questions are public, and have the writer's name (or pseudonym) attached. The similarity search necessary for finding similar questions is performed on the server, so the server learns, but does not retain, information about drafted questions, even if they were not posted.

## What we ask people to share

Optionally, people may state the electorate they live in.[^1] This allows MPs (and everyone else) to filter based on their own electorate.

I see no reason to ask for demographic information, except possibly to understand who is under 18.

:::spoiler Discussion
:::warning
**Q:** What is the minimum group size to allow for aggregation, in order to be fairly confident of not violating individual privacy? 
**A:** This is complicated by aggregation in other dimensions, such as time and electorate.

---
**Q:** Are there extra privacy rules for participants under 18? 
**A:** Certainly in the EU there are - not sure about Aus.

---
**Q:** How important is participation privacy as well as the privacy of up or down votes? 
**A:** That is, does it matter whether it is possible to detect which users have rated which questions?
:::

## Identity and account verification 

### MPs

MPs are relatively easy to verify using their parliamentary email. We can do the traditional/standard sending of some secret code to that email address, and use it at registration time. This proves that the person registering has access to the official email account.

:::warning
**Q**: How are these answered in practice? Is there one account or device on which they're read, or are there multiple people with access?

---
**Q**: How should RightToAsk account access be organised for staffers? Do different staff take responsibility for different aspects, e.g. some for committee questions and others for constituent matters?
:::

### Citizens

Detecting completely fake accounts, and distinguishing them from a signup drive from a legitimate source, is really important but very hard. Perhaps new accounts should have a 'new user' badge (because that might be a nice person to engage with, but it might also be grounds for suspicion because not actually a real person).

How do we check whether the person really does live in the electorate? My suggestion is that by default we don't, though I think it would be good to add a feature where a person who has visited their MP (at a public meeting or whatever) could be certified as living there.

:::warning
**Q:** Could we possibly use mailouts, e.g. by MPs to constituents or from electoral Commissions, with unique random numbers? 
**A:** The assumption would be that if you can pick up that person's mail then you must be that person. Not perfect, but a decent deterrence of widespread fake registration. Perhaps when people sign up they could apply for such a thing if their MP joins in? This would cost a postage stamp of course.

---
**Q:** Should you be allowed to use a pseudonym? 
**A:** My feeling is yes, but know that you're easily re-identified.
:::


### Organisations

It would be valuable to be able to identify key stakeholders, e.g. that the person who claims to be writing on behalf of an organisation really does speak for it. So for example domain names could be required to match email addresses for orgs. So perhaps we have a profile screen where an org can state their website, and then we verify that their email address has the same domain (the same way we verify MPs' emails, but with the domain they claimed). It's not perfect, and it doesn't stop you registering "mydodgyfakeoftheaustralianconservationfoundation.com" but at least it gives other users a chance to check their website.

## Key management

:::warning
**Q:** Could we implement a signal-like way to check your friend's key? And/or integrate with other systems such as Signal, Apple, Keybase, etc?

---
**Q**: We could optionally allow people to secret-share their private key with friends (or authorities?) for recovery. Is that a helpful feature or too hard to do in a usable way?
:::

## Direct Messages

Direct messages are end-to-end encrypted but do not attempt to hide metadata (e.g. who communicated with whom, when, how frequently, and how long the messages were). We are considering the best ways of delivering message notifications - see the [Discussion in the technical docs](https://github.com/RightToAskOrg/technical-docs/discussions/3).

[^1]: In Victoria, all state electorates are subsets of federal electorates, but in other Australian states this is not guaranteed. This matters for privacy because there may be only a few people in the intersection of two (state and federal) electorates, so tallying of those subsets may reveal individual votes.
