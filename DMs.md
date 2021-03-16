# Possible extra feature: Direct Messages {#sec:DMs}

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