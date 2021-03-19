# Security and privacy {#sec:securityAndPrivacy}

RightToAsk incorporates the [ElectionGuard end-to-end verifiability
library](https://github.com/microsoft/electionguard) to aggregate votes before the total is decrypted, and to prove
that even the system administrators cannot artificially inflate or
deflate the popularity of questions.

Citizens can also verify proper
inclusion of their votes, and anyone can verify proper tallying of those
questions they are interested in.

## What we ask people to share

Optionally, people may state the electorate they live in.[^1] This
allows MPs (and everyone else) to filter based on their own electorate.

I see no reason to ask for demographic information, except possibly to
understand who is under 18.

-   *Question: What is the minimum group size to allow for aggregation,
    in order to be fairly confident of not violating individual privacy?
    This is complicated by aggregation in other dimensions, such as time
    and electorate.*

-   *Question: Are there extra privacy rules for participants under 18?
    Certainly in the EU there are - not sure about Aus.*

-   *Question: How important is participation privacy as well as the privacy of up or down
votes? That is, it should not be possible to detect which users have
rated which questions.*

## Identity and account verification {#subsec:identityAndAccountVerif}

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
    aspects, e.g. some for committee questions and others for
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

*Question: Should you be allowed to use a pseudonym? My feeling is yes, but know
that you're easily re-identified.*

### Key management

*Question: Could we implement a signal-like way to check your friend's key? And/or
integrate with other systems such as Signal, Apple, Keybase, etc?*

*Question: We could optionally allow people to secret-share their private key with
friends (or authorities?) for recovery. Is that a helpful feature or too hard to do in a
 usable way?*

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


|:----------------|---------------:|
| [Back: Screens and Usage](https://righttoaskorg.github.io/righttoask-docs/ScreensAndUsage)| |[Next: Direct Messages](https://righttoaskorg.github.io/righttoask-docs/DMs)


[^1]: In Victoria, all state electorates are subsets of federal
    electorates, but in other Australian states this is not guaranteed.
    This matters for privacy because there may be only a few people in
    the intersection of two (state and federal) electorates, so tallying
    of those subsets may reveal individual votes.
