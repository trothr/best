# PGP - Pretty Good Privacy

When we talk about PGP, most people think first about email.
That's reasonable because PGP was first used as a means of securing
email communication and contemporary solutions using the same
cryptographic technology are primary focused on communication.

But there's more to this than just email and other communication,
and we're seeing increased use of asymmetric cryptography in things like
crypto-currencies, code signing, and NFTs. It's all about trust.

The PGP "web of trust" may be the strongest cryptographic trust anchor
available to the human race.

PGP first appeared in popular computing in the late 1980s.
Phil Zimmerman with his "Phil's Pretty Good Software" combined traditional
symmetric encryption with then-new asymmetric encryption, specifically
the RSA algorithm, and offered "strong encryption for the masses".

There is an intriguing story about Phil Zimmerman and PGP from the
1990s which is beyond the scope of this document. But look for it,
if only for the entertainment value, or perhaps as a cautionary tale.

## Rivest, Shamir, Adleman

In the late 1970s, Ron Rivest, Adi Shamir, and Leonard Adleman then at
the Massachusetts Institute of Technology (MIT) sought come up with
a function that was hard to invert. They were inspired by the work of
Whitfield Diffie and Martin Hellman who had suggested the idea in 1976
of an asymmetric public/private key cryptosystem.

The heart of the system is that a "message" encrypted with the public key
can only be decrypted with the private key (the secret key). Further, one
cannot easily determine one key from the other. The public and private
keys are mathematical counterparts, created at the same time, but not
easily guessed from each other.

In the early 1970s, several years ahead of Rivest, Shamir, and Adleman,
Clifford Cocks and others then at UK GCHQ derived a similar cryptosystem.
Later, Cocks also developed Identity-Based Encryption (IBE).

Today there are several asymmetric crypto algorithms, but RSA remains
in heavy use.

## Asymmetric Crypto

With symmetric cryptography, as with traditional keys and locks,
as well as such things as passwords, there is a serious distribution
challenge. How do you get the key to the person who needs it?
There is also the problem of copying. The same key which locks the
message or file can unlock it. The file can be decrypted, modified,
and then re-encrypted, and no-one would be the wiser.

With asymmetric cryptography, there is still the need to distribute,
but distribution becomes dramatically less risky. Your public key can
and should be distributed widely. There is little harm in a hostile
party having your public key. Once you have established a line of trust,
additional public keys can be sent, both symmetric and asymmetric.

## Combined Crypto

Asymmetric cryptographic algorithms are heavy, slow to execute.
They use longer key lengths than their symmetric cousins. The latter
run faster. The former ensures authenticity of the recipient and often
(in best practice) of the sender too.

Whether purely common sense or a spark of genius, Zimmerman combined
symmetric crypto with asymmetric. The bulk of the message (or file)
in PGP is protected by a symmetric "session key". The session key is
protected with tye asymmetric key. This minimizes the load on the
slower algorithm to decrypting only a small body, the session key,
which is typically less than 100 bytes.

The combination also allows that the session key can be economically
encrypted with more than one asymmetric public key, allowing multiple
recipients in PGP and similar applications.

The concept of a "session key" is most clearly demonstrated in
services like SSH and SSL (TLS, for HTTPS and other things) where
there is an actual "session" in the usual sense.

Similarly, the "signing" of objects with asymmetric keys is done by
encrypting a hash of the object to be signed with the private key
of the signer. People posessing the signer's public key can then
decrypt the signature. If the decrypted signature matches, it is
understood to be authentic. The hash can cover a very large object
but is itself consistently very small and suitable for encryption
using asymmetric algorithms.

## Authenticating Both Ways

When a message is encrypted with the recipient's PGP public key
the recipient is confirmed (is authenticated). Since only the recipient
has the private half of his key pair, only the recipient can read
the message.

Asymmetric cryptography allows that you can send content
without worry that it might fall into the wrong hands.

Messages can also be signed by the sender.
Signing a message confirms that it really came from the one
who supposedly wrote it. We've all gotten "spam" where a message
supposedly came from one sender but was faked. When you have a
public key for the supposed sender, and the message is signed,
you can verify authenticity.

Asymmetric cryptography allows that you can confirm that content
which you receive is the genuine article, the real thing.

## PGP Renaissance

In the early days of PGP, the tool was necessarily used manually.
These days it is well integrated, but the perception of manual steps
persists. You may occasionally read "PGP must die!" and similar cries.
But understand such complaints are about unintegrated operation,
not about the tool itself and certainly not about the technology.
Key management is *hard* and manual operation is annoying.

Again, the PGP web-of-trust is likely the strongest cryptographic
trust anchor that we have. We must have anchors, but all others
are more vulnerable to rogue disruption or misrepresentation.

Around 2020, Thunderbird Email gained PGP functionality
as the developers incorporated the OpenPGP library into the client.
Other email clients already integrate PGP. As a result, any consumer
can use strong encryption with their email *without* having to perform
confusing techie operations with mysterious complicated incantations.
It's easy!

The stand-alone tools are still there and work well for traditional
operations. Code signing, for example, can be integrated with
software management, but can also be effected by discrete utilities.

Increasingly, software and other content available via the public
internet is cryptographically signed. When you then have the
public key of the signer (and when you have assurance of that key's
validity) then you can trust that the content is legitimate.

Attestation isn't encryption, but it's all under the same umbrella.

## It's All About Trust

In the PGP world, public keys must be exchanged in person for proper
assurance of ownership. The cryptography is no different than we use
in PKI (SSL/TLS), SSH, but PGP started as a hobbyist effort. Strictly
speaking, PGP keys do not have to be exchanged in person (same chaining
works for PGP as works for PKI) but PGP keys are traditionally added
manually. Manual effort doesn't scale.

"Crypto is easy. Key management is hard."

Enterprise and commercial, as well as military and government,
trust anchors are established by agencies. When you use systems
and services controlled by these agencies, you intrinsically place trust
in the anchors established by the agencies. It works. Think about things
like an Active Directory Domain Controller. Your work PC "trusts"
the AD controller and vice versa.

Mechanized trust scales better. It is not perfect.
I advocate PGP as a means of supplementing the more scalable
business model with the human touch.

## Reflections on Trusting Trust

In 1983, Ken Thompson famously gave his "Reflections on Trusting Trust"
speech in acceptance that year of the Turing Award (jointly received
with the late Dennis Ritchie). The gist of the speech is that machines
can hide what men have done. Everything Ken said in 1983 remains true today.

Think about how well you trust any given third party. <br/>
Your web browser verifies HTTPS connections to most internet sites
because the maker of your browser has pre-loaded root certificates
into the browser. These root certificates come from companies like
Apple, Microsoft, Verizon, Symantec, as well as from lesser-known
companies like DigiCert, Entrust, Thawte, Comodo, StartCom. Some of
these are no longer in business and some of them have been breached.

On the web, the trust model is PKI, Public Key Infrastructure.
It scales better for managed trust, but notice that the "trust"
(technical) is something you're probably unaware of. With the PGP model,
you're aware. You can actually "trust" (functionally) the PGP web
better because of your awareness and the human factors involved.

The PKI model means there is a third party. You might actually have
end-to-end encryption, but there are *three* parties, not just two,
and possibly more, that you have to rely on.

We would do well to see the best of both worlds,
to use PKI certificate chains which carry added trust logic
which has been confirmed by people we know. This remains rare.

The PKI model is much easier for consumers, but
it is more risky. There's at least 50% more opportunity for failure/leakage.

## references

https://en.wikipedia.org/wiki/RSA_(cryptosystem)

https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange

https://en.wikipedia.org/wiki/Clifford_Cocks

https://www.cs.cmu.edu/~rdriley/487/papers/Thompson_1984_ReflectionsonTrustingTrust.pdf


