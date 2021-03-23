# Server API sketch

This file sketches the main ideas for a REST API for client-server interaction.  The key idea is to separate the data upload step from the inclusion-verification step.

We envisage a bulletin board (BB) which is rebuilt on a relatively slow schedule - think of an epoch as an hour or perhaps a day.  At the end of each epoch, the BB produces a new root hash, and is able to produce:

- a proof of inclusion of any data posted in the previous epoch, and
- a history proof (subtree proof) of inclusion of the prior epoch's root hash.

See these resources for [a good pictorial introduction to Merkle Trees and inclusion proofs](), [Google's Trillian implementation](https://github.com/google/trillian) and [Crosby and Wallach's paper describing the original ideas](https://www.usenix.org/legacy/event/sec09/tech/full_papers/crosby.pdf).  

We assume the interfaces for inclusion and history proofs defined by Eleanor McMurtry [here](https://eleanorve.net/google-merkle-rs/google_merkle/struct.MerkleTree.html).  For now, call them inclusionProof and historyProof.  These proofs work only on hashes of data, not on the posted data directly.

## Main post functions

The main functionality of the rightToAsk client-server interaction is very similar to that of the prototype, except that we also add verification of the BB state.  This means that each upload is divided into two parts: data to be uploaded to the BB, and other optional metadata.  The BB data also needs the client's signature.  So a typical post, e.g. for registration, question-posting, or voting, has this structure:

**Post**

- D = data
- CSig = signature<sub>Client</sub>(data)
- M = metadata

This receives an immediate acknowledgement from the server, of the form:

**Ack**

- SSig = signature<sub>server</sub>(h(D, CSig))

where h indicates a cryptographic hash function (e.g. SHA256), for use in the BB proofs.  This is a promise from the server that H(D), CSig will be included on the BB.

The role of the metadata M is to allow the client to upload extraneous info to the server without that info being posted on the BB.

The exact requirements for the data obviously depend on the specific kind of message. For registration, data would include a name, public key and (optionally) electorate.  For voting, data would include vote ciphertexts with sufficient extra data to identify which questions they were answering.  For question-asking, the data is quite complex and would include the text of the question, the ID of the person asking, any tags or links, etc.  We will also add some more functionality for answering quesions, marking them as answered, re-tagging them for other MPs, etc...

## Verification functions
There are three different things a client may wish to verify (though the first two are very similar):

- that certain previously-posted data is included on the BB,
- that the root hash of a previous epoch is properly included in the current root hash,
- that the root hash is properly constructed from all posted data.

Let H = h(D,CSig) be some data previously posted to the BB.

**Verify-inclusion**

The client's verify-inclusion query is to send H to the server.  The server responds with an 

- I = inclusionProof(H,R)

where R is the current root hash.

(**VT: I need to think about this  a little more, because it's not 100% clear what should happen if you ask for an inclusion proof from a few epochs ago.  I think the right answer is that you should get an inclusion proof for the root hash of that epoch (RPast), plus a history proof linking that root to the present epoch's root, i.e. historyProof(RPast,RPresent).  I'll check what Trillian does here.**)

**Verify-history**

A client can request proof that earlier root hashes are properly-included subtrees of the current one. The client sends:

- R1, R2: two root hashes from different epochs

and the server returns

- Hist = historyProof(R1,R2)

or an error if R1, R2 are not valid root hashes, or R1 is not a subtree of R2.

If R2 is omitted, the server returns historyProof(R1,R) where R is the current root hash.

(**VT: More details here.  It occurs to me that the Root hash data probably needs some metadata, e.g. a sequence number, so you can tell which roots are supposed to be subtrees of which others.  I assume Trillian already does this - will check.  Also, just as for the inclusion proofs, we can think about whether a history proof for two roots separated by several epochs is a direct subtree proof, or a list of immediate-subtree proofs, one for each epoch.  I suspect the latter is better - will check what Trillian does.**)

**Verify-BB**

This function is intended to allow a complete download of the BB's contents, expecting that the client will want to verify all the vote aggregation and decryption as well.  Here we describe only the verification that the root hash is properly constructed.  Unlike all the other query functions, this function outputs data, not just the hashes.  The client sends:

- R1, R2: two root hashes from different epochs

and the server returns

- the complete BB contents between R1 and R2.

If R1 is omitted, the entire history since inception until R2 is returned.  If R2 is omitted, the current root hash is used.

There is no need for a history proof because the client can compute this themselves.







### Details and other questions
I'm not quite sure what M would be, but it seems a useful placeholder.  It is also possible that we should have a similar placeholder for the server's response.  e.g. it could tell you which epoch your data will appear in, to avoid ambiguity in the case where your upload occurred close to the boundary.

I've also generally left out data that didn't need to be there, such as the data.  It's possible that it would be simpler to include this sometimes, rather than only the hash.

I have also omitted many of the details that need to be added for general good API design, such as a version number, to allow for later updates.

