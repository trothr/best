# SSL/TLS and PKI - Public Key Infrastructure

"Secure Sockets Layer" (SSL) was first introduced by Netscape
in the mid 1990s. As the world-wide web grew in popularity, the need for
secure communication on the public internet became abundantly clear.
SSL provided a way to ensure that the target web site was authentic
and provided an encrypted channel between the browser and the server.

SSLv1 was never publicly released and was quickly replaced by SSLv2.
That in turn was soon replaced by SSLv3 which was considerably stronger
and remained in use for more almost 20 years. Both SSLv2 and SSLv3
were followed by TLS, "Transport Layer Security". The protocol itself
has remained mostly stable while cipher suites have been replaced
in the releases TLS 1.0, 1.1, 1.2, and now 1.3.

PKI is the Public Key Infrastructure used for enabling *trust*
between clients (more than just browsers) and servers on a grand scale.
Various Certificate Authorities (CAs) issue certificates for various
uses, initially server, also client, and often for specific uses.
(authentication, code signing, authorization, signing on, and so forth)

## Trust Anchors

In PKI, trust anchors are the root certificates.
Makers of web browsers pre-load a large collection of root certificates
into the browsers they produce. Users of these browsers then automatically
"trust" most web sites without special action.

In most cases, a root certificate from the CA is used to "issue" an
intermediate certificate (usually from the same CA) which in turn is used
for issuing "end entity" or "leaf" certificates. The purpose of the leaf
certificates is most commonly for server authentication (a server cert)
but also often for client authentication and authorization (a PIV card
or CAC or other client cert).

## Issuance and Renewal

Before a web server (for example) can speak HTTPS rather than plain HTTP,
it must have a server certificate. To get a server cert, the administrator
must create an asymmetric key pair. The key pair is then used in creation
of a "certificate request". The request contains the public half of the
key pair along with X.509 information identifying the server.

PKI certifictes have a range of validity "not before" and "not after".
The latter is an expiration date. System administrators who support PKI
must attend to expirations on a regular basis.

There is no technical limit on certificate lifetime, but web server
certificates are commonly set to expire a year after they are issued.
Longer lifetimes could be supported except that several prominent 
providers (notably Apple, Google, and Mozilla) decided to reject
certificates which last longer than 398 days, ostensibly for security.
There action (from 2020) forced the hand of the whole consumer internet.

Privately managed certificates can last longer, sometimes *much* longer.
The rationale for longer-lived certificates is to reduce administrative
tedium and error-prone human action.





## X.509

X.509 is the standard of the International Telecommunication Union (ITU)
which definines certificate structure and usage for Public Key Infrastructure
(PKI). When we talk about "SSL certificates" or "TLS certificates" we're
talking about PKI certificates as defined by X.509.




* CN - Common Name <br/>
This is the fully qualified domain name that you wish to secure <br/>
example: `*.wikipedia.org`
* O - Organization Name <br/>
Usually the legal name of a company or entity and should include any suffixes such as Ltd., Inc., or Corp. <br/>
example: Wikimedia Foundation, Inc.
* OU - Organizational Unit <br/>
Internal organization department/division name <br/>
example: IT
* L - Locality <br/>
Town, city, village, etc. name <br/>
example: San Francisco
* ST - State <br/>
Province, region, county or state. This should not be abbreviated (e.g. West Sussex, Normandy, New Jersey). <br/>
example: California
* C - Country <br/>
The two-letter ISO code for the country where your organization is located <br/>
example: US
* EMAIL - Email Address <br/>
The organization contact, usually of the certificate administrator or IT department


Some of the above must align with legal attributes of the entity
owning and operating the server. The certificate authority (CA) may
enforce certain agreement. Utilities like OpenSSL can programmatically
enforce agreement of selected fields.



https://en.wikipedia.org/wiki/Transport_Layer_Security

https://en.wikipedia.org/wiki/Certificate_signing_request

https://en.wikipedia.org/wiki/X.509

https://thehackernews.com/2020/09/ssl-tls-certificate-validity-398.html






