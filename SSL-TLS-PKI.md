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
intermediate certificate (usually from the same CA) which in turn is
used for issuing end or "leaf" certificates. The purpose of the leaf
certificates is most commonly for server authentication (a server cert)
but also often for client authentication and authorization (a PIV card
or CAC or other client cert).


## Issuance and Renewal

Before a web server (for example) can speak HTTPS rather than plain HTTP,
it must have a server certificate. To get a server cert, the administrator
must create an asymmetric key pair. The key pair is then used in creation
of a "certificate request". The request contains the public half of the
key pair along with X.509 information identifying the server.






CN      Common Name             This is fully qualified domain name that you wish to secure                                                     *.wikipedia.org
O       Organization Name       Usually the legal name of a company or entity and should include any suffixes such as Ltd., Inc., or Corp.      Wikimedia Foundation, Inc.
OU      Organizational Unit     Internal organization department/division name                                                                  IT
L       Locality                Town, city, village, etc. name                                                                                  San Francisco
ST      State                   Province, region, county or state. This should not be abbreviated (e.g. West Sussex, Normandy, New Jersey).     California
C       Country                 The two-letter ISO code for the country where your organization is located                                      US
EMAIL   Email Address           The organization contact, usually of the certificate administrator or IT department












https://en.wikipedia.org/wiki/Transport_Layer_Security

https://en.wikipedia.org/wiki/Certificate_signing_request














##
