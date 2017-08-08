(B) Cryptography
================

The secure messaging cryptography community now expects a great deal
of features in a text-based messenger. Some of these are:

* Confidentiality
* Authenticity (of origin and message)
* Forward secrecy
* Session freshness
* (Limited) plausible deniability
* Chat room and transcript consistency
* ...

An implementation of the full set of these features is time consuming
and cannot be expected to be available for the time line of this
development plan.  A simpler cryptographic solution -- which is still
cryptographically sound -- is going to be used.  The sole focus lies
on the cryptographic requirements of message transport/storage
confidentiality and authentication of participants and their messages.

The transport encryption is going to be built by using elliptic curve
(EC) public-key cryptography from the existing TweetNaCl library
[TweetNaCl-paper]_ [TweetNaCl-homepage]_ [TweetNaCl.js]_ library.  It
has been chosen for its high quality (lots of peer review and
integrity tests) and efficiency (towards computational as well as
storage overhead of cipher texts).  Tests (our own in modern browsers)
have also shown it to only cause a small performance impact that is
perfectly tolerable.

This simple encryption scheme does not require a key agreement
protocol, making it ideal to be also used for simplicity in offline
messages and concurrent multi-device capability for a single user.

Messages are going to be encrypted using a symmetric cipher scheme
using XSalsa20.  Every message is authenticated using an Ed25519 EdDSA
signature (therefore not needing a Poly1305 authentication code).
Messages containing new per-user symmetric sending keys are using
Curve25519 to derive a public key encryption key for that individual
message.

For this to work, a "chat key" encryption key pair (Curve25519) needs
to be added to a user's attributes analogously to the already existing
Ed25519 key pair, with the public key portion signed for verification
of authenticity.


..
    Local Variables:
    mode: rst
    ispell-local-dictionary: "en_GB-ise"
    mode: flyspell
    End:
