%%%
title = "Usage specification of the otpauth URI format for TOTP and HOTP token generators"
abbrev = "otpauth URI spec"
ipr = "trust200902"
area = "Internet"
workgroup = ""
submissiontype = "IETF"
keyword = ["internet", "internet security", "otpauth", "totp", "hotp"]
#date = 2023-11-08T22:00:00Z

[seriesInfo]
name = "RFC"
value = "draft-linuxgemini-otpauth-uri-01"
stream = "IETF"
status = "informational"

[[author]]
initials = "I. Y."
surname = "Eroglu"
fullname = "Ilteris Yagiztegin Eroglu"
organization = "independent"
    [author.address]
    email = "ietf@linuxgemini.space"
        [author.address.postal]
         city = "Ankara"
         country = "Turkey"

%%%

.# Abstract

This document describes a foundational schema for the otpauth URI,
utilized by TOTP (and/or HOTP) based authenticators.

{mainmatter}


# Discussion {#Discussion}

This note is to be removed before publishing as an RFC.

Source for this draft and an issue tracker can be found at
https://github.com/linuxgemini/otpauth-spec-draft.


# Introduction {#Introduction}

The otpauth URI is used for easy addition of accounts to TOTP (and/or HOTP)
authenticators with various options
[@Google.Authenticator.OSS.Wiki.Key.Format].

Although available as a provisional scheme at IANA
[@IANA.URISchemes.Prov.otpauth], there are many divisions of the usage
specification per authenticator hardware and software [@Edent.Blog.Post].

This document aims to provide foundational boundaries for the URI format
and standardize the secret sharing of OTP tokens.


## Conventions and Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED",
"MAY", and "OPTIONAL" in this document are to be interpreted as
described in BCP 14 [@!RFC2119] [@!RFC8174] when, and only when, they
appear in all capitals, as shown here.

This specification uses the Augmented Backus-Naur Form (ABNF) notation
of [@!RFC5234].

This specification uses the terms "TOTP" defined by [@!RFC6238] and "HOTP"
defined by [@!RFC4226]. Both RFCs also mention "secret", "issuer" and
"account".

The term "URI" is imported from [@!RFC3986]. Mentions of "query string" in
this document references the "Query" parameter (in section 3.4) of this RFC.

The Base16, Base32, and Base64 Data Encodings mentioned here are imported
from [@!RFC4648] with the same name.


# Syntax {#syntax}

The URI MUST be formatted like below:


```
otpauth://TYPE/LABEL?PARAMETERS
```


An approximate ABNF representation of this is like below:


```
otpauth-uri    = "otpauth://" uri-type "/" uri-label "?" uri-parameters
uri-type       = "totp" / "hotp"
uri-label      = *VCHAR
uri-parameters = "secret=" *base-32 [ *uri-opt-parameters ]

uri-opt-parameters =  ("&algorithm=" otp-algorithm)
uri-opt-parameters =/ ("&digits=" otp-digits)
uri-opt-parameters =/ ("&counter=" *DIGIT) / ("&period=" *DIGIT)
uri-opt-parameters =/ ("&issuer=" *VCHAR) / ("&" *VCHAR "=" *VCHAR)
                        ; Please refer to RFC3986 for handling
                        ; complex names

otp-algorithm = "SHA1" / "SHA256" / "SHA512"

otp-digits    = %x36-38
                ; 6-8

base-32 = %x41-5A / %x32-37
                ; A-Z2-7
DIGIT   = %x30-39
                ; 0-9
VCHAR   = %x21-7E
                ; visible (printing) characters
```


## `TYPE` entry (REQUIRED)

The type entry MUST be one of `totp` or `hotp`, depending on the OTP type.


## `LABEL` entry (REQUIRED)

The label entry MUST be an identifier representing the user. For example,
can be an username, nickname or a person's name.

The label entry MUST be consided as a Path per section 3.3. of [@!RFC3986].

Although the Authenticator Team at Google recommends including the secret
issuer to be prepended to the label with the colon character (`:` or `%3A`)
as a seperator in [@Google.Authenticator.OSS.Wiki.Key.Format], the authors
of this document believe that the issuer should only be appended as a
seperate parameter (see next division).


## `PARAMETERS` entry (REQUIRED)

This entry is an URI query string. Each parameter MUST be seperated by the
`&` character and SHOULD BE "URI Safe" (see section 2.2. Reserved
Characters in [@!RFC3986]).

The following parameters SHOULD BE included:


### `secret` parameter (REQUIRED)

The secret of the OTP MUST be provided within this parameter. The secret
MUST be encoded in Base32. The padding specified in [@!RFC4648]
section 3.2 is not required and SHOULD BE omitted.

For example:


```
otpauth://totp/ietfuser?secret=NBSWY3DPFQQHO33SNRSAU
```


### `algorithm` parameter (OPTIONAL)

The algorithm used for TOTP or HOTP tokens SHOULD BE provided
in this parameter. When not provided, `SHA1` is assumed by default.

The ABNF representation is defined below:

```
otp-algorithm   = "SHA1" / "SHA256" / "SHA512"
```


Some authenticators at the time writing of this document ignore this
parameter, the authors of this document believes that this parameter
MUST be supported in all cases.


### `digits` parameter (OPTIONAL)

The amount of digits to be outputted for TOTP or HOTP tokens
SHOULD BE provided in this parameter. This value MUST be
between 6 and 8. When not provided, 6 digits is assumed by default.

Some authenticators at the time writing of this document ignore this
parameter, the authors of this document believes that this parameter
MUST be supported in all cases.


### `counter` parameter (REQUIRED if HOTP)

The provisioning counter for HOTP tokens MUST BE provided in this
parameter.

This parameter is ignored if the token type is TOTP.


### `period` parameter (OPTIONAL, only TOTP)

The refresh period (in seconds) for TOTP tokens SHOULD BE provided
in this parameter. When not provided, 30 seconds is assumed by default.

Some authenticators at the time writing of this document ignore this
parameter, the authors of this document believes that this parameter
MUST BE supported in all cases.

This parameter is ignored if the token type is HOTP.


### `issuer` parameter (OPTIONAL)

The issuer name of TOTP or HOTP tokens SHOULD BE provided
in this parameter.


### Other parameters (OPTIONAL)

Vendors MAY include other parameters in their issued otpauth URIs.
These parameters are OPTIONAL for the function of TOTP or HOTP
tokens and not necessary to be included in this document.


# Examples {#Examples}


```
otpauth://totp/ietfuser?secret=NBSWY3DP

otpauth://hotp/13tfus3r?secret=NBSWY3DP&counter=192

otpauth://totp/big?issuer=IETF&secret=NBSWY3DP&period=5&algorithm=SHA256
```


# Security Considerations {#SecurityConsiderations}


This URI format does not in itself pose a security threat. However,
the Security Considerations of [@!RFC3986] SHOULD BE followed.


# IANA Considerations {#IANAConsiderations}

This format is already available as a provisional entry
[@IANA.URISchemes.Prov.otpauth]. IANA is asked to change
the provisional URI scheme to reference [[this RFC]].


{backmatter}


# Acknowledgements {#Acknowledgements}

We would like to thank
Q Misell,
Terence Eden,
The Google Authenticator Team at Google,
and others (please let us know, if you've been mistakenly omitted)
for their valuable input, feedback and general support of this work.

This document originated from discussions at the Fediverse initially
written by Terence Eden [@Edent.Mastodon.Post].


# Document History

   [[ To be removed from the final specification ]]

   -01

   *  corrected Terence's name
   *  corrected parameter confusion between TOTP and HOTP

   -00

   *  first draft


<reference anchor="IANA.URISchemes.Prov.otpauth" target="https://www.iana.org/assignments/uri-schemes/prov/otpauth">
 <front>
   <title>Provisional scheme for the otpauth URI</title>
   <author><organization>IANA</organization></author>
 </front>
</reference>

<reference anchor="Google.Authenticator.OSS.Wiki.Key.Format" target="https://github.com/google/google-authenticator/wiki/Key-Uri-Format">
 <front>
   <title>Google Authenticator Key Uri Format</title>
   <author><organization>Google</organization></author>
 </front>
</reference>

<reference anchor="Edent.Mastodon.Post" target="https://mastodon.social/@Edent/108266107975107228">
 <front>
   <title>Fediverse post for "Why is there no formal specification for otpauth URls?"</title>
   <author><fullname>Terence Eden</fullname></author>
 </front>
</reference>

<reference anchor="Edent.Blog.Post" target="https://shkspr.mobi/blog/2022/05/why-is-there-no-formal-specification-for-otpauth-urls/">
 <front>
   <title>Why is there no formal specification for otpauth URls?</title>
   <author><fullname>Terence Eden</fullname></author>
 </front>
</reference>
