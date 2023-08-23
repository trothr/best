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

## Rivest, Shamir, Adleman, and Cocks

In the late 1970s, Ron Rivest, Adi Shamir, and Leonard Adleman (the R,
S, and A of RSA) then at the Massachusetts Institute of Technology (MIT)
sought come up with a function that was hard to invert. They were inspired
by the work of Whitfield Diffie and Martin Hellman who had suggested the
idea in 1976 of an asymmetric public/private key cryptosystem.

Prior to the development of asymmetric cryptography, all ciphers were
symmetric, meaning that the "key" which locked a message was the same
"key" as unlocked it. The heart of the new system was that a "message"
encrypted with the *public* key could only be decrypted with the
*private* key (the secret key). Further, one cannot easily determine
one key from the other. The public and private keys are mathematical
counterparts, created at the same time, but not easily guessed
from each other.

In the early 1970s, several years ahead of Rivest, Shamir, and Adleman,
Clifford Cocks and others then at UK GCHQ derived a similar cryptosystem.
Later, Cocks also developed Identity-Based Encryption (IBE).

Today there are several asymmetric crypto algorithms,
but RSA remains in broad use.

## Asymmetric Crypto

With symmetric cryptography, as with traditional keys and locks,
as well as such things as passwords, there is a serious challenge
regarding distribution. How do you get the key to the right person?
How do you ensure that the key is not intercepted or copied?
Symmetrically, the same key which locks the message or file can unlock,
just like a password on a ZIP file. The file can be decrypted, modified,
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

## Command-Line Operations

The following sections discuss using Gnu Privacy Guard (GPG), one of the
more popular PGP work-alike utilities. When using PGP with an integrated
application such as Thunderbird, it's best to use the interface within
the application. But for operations which need to work on discrete files
or where there is no formal integration, use command-line tools like GPG.

GPG (like most PGP implementations) has the concept of a "key ring" and
maintains two files: one for public keys and one (smaller) for private keys.

## Generate a Key Pair

    gpg --gen-key

Enter the command and respond to the prompts:

    1 - RSA and RSA (default)
    4096 bits
    0 - Key does not expire at all

RSA remains the most common asymmetric algorithm.

Be sure and use the largest key size possible, 4096 bits in this case.

Key expiration can be counter productive.
It's better to create a key revokation file.

    Real name: human readable
    Email address: reachable mailbox or identity
    (you can leave the comment field blank)

    Enter passphrase:

Your name and email address are vital if this key will be used for email.
Even if this key will only be used for files and/or signing, it should
have an identity associated with it.

For some keys, you can use a non-working email address or can use
a string in the email field which is not an email address at all.
But the key should be readily identifyable.

## Importing and Exporting Keys

Use the following commands to import and export keys.

    gpg --armor --export [keyid] > [keyfile]
    gpg --send-keys [keyid]                     export keys to a key server
    gpg --import [keyfile]                      import (and merge) keys
    gpg --recv-keys [keyid]                     import keys from a key server
    gpg --list-keys [keyid]                     show public keys
    gpg --list-sec                              show your secret keys (your private keys)

The `--armor` option applies "ASCII armor" to otherwise binary content.
For the export command, it results in an exported key file which can be
passed around as plain text (copy-n-pasted, embedded in email, etc).

There are a number of PGP key servers available publicly.
You can upload keys to and download keys from these servers.
Export is to "send" as import is to "recv".

## Encrypting and Decrypting

Once you have (at least) a public key, you can encrypt.
For any public key used to encrypt a file, you'll need the private
(secret) half to decrypt that file.

    gpg --decrypt [file]
    gpg --encrypt [file]

When decrypting, you'll be prompted for the pass phrase of the
appropriate secret key. If you have a GPG Agent running then you can
enter your pass phrase less frequently, sometimes only once per session.

## Signing and Verifying Files

Use the following commands to sign a file,
confirming its authenticity to others who have your public key.

    gpg --sign [file]                           make a signature
    gpg --detach-sign [file]                    make a signature in a separate file
    gpg --verify [signedfile]                   verify a signature on a signed file

It is common to have the signature in a separate file.
That's the purpose of `--detach-sign`.

When verifying a file with a detached signature, name the signature file
(typically `.sig` or `.asc`) not the signed file, and `gpg` will find
the signed file by removing the filename extension of the signature file.

## Signing Keys

You can sign keys on your public key ring.
When you sign someone's key and then export it,
people who know you can "trust" that person's key
much like they would trust the authenticity of a file that you sign.

    gpg --sign-key [keyid]                      sign a key (rather than a file)
    gpg --list-sigs [keyid]                     list keys and signatures
    gpg --fingerprint                           list keys and fingerprints

See above for exporting signed keys.
(Exported keys will contain all signatures.)

## GPG Options

When ecrypting, you must specify at least one recipient.
Keep in mind that this "recipient" is not necessarily one who
will receive a message but is simply one who can decrypt the file.

    --recipient [keyid]                         encrypt for [keyid]

You can have any number of recipients. Under the covers,
GPG will create a random symmetric session key and will encrypt
that key with the various asymmetric public keys of the recipients.
It will then encrypt the payload (file or message) with the session key.

GPG operations which produce output can be directed to a named file.

    --output [file]                             use a specific output file

Use the `--verbose` option to get more details from GPG.

    --verbose                                   verbose

## references

https://en.wikipedia.org/wiki/RSA_(cryptosystem)

https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange

https://en.wikipedia.org/wiki/Clifford_Cocks

https://www.cs.cmu.edu/~rdriley/487/papers/Thompson_1984_ReflectionsonTrustingTrust.pdf


