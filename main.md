%%%
title = "Usage specification of the otpauth URI format for TOTP and HOTP token generators"
abbrev = "otpauth URI"
ipr = "trust200902"
area = "Security"
workgroup = ""
keyword = ["security", "otpauth", "totp", "hotp"]

[seriesInfo]
name = "Internet-Draft"
value = "draft-ietf-otpauth-uri-00"
stream = "IETF"
status = "standard"
    
[[author]]
initials = "I. Y."
surname = "Eroglu"
fullname = "Ilteris Yagiztegin Eroglu"
organization = "Trendyol"
    [author.address]
    email = "ilteris.eroglu@trendyol.com"
    emails = ["me@linuxgemini.space"]
        [author.address.postal]
        street = "Maslak Mah. Saat Sok. Spine Tower No: 5/19"
        code = "34485"
        city = "Sariyer"
        region = "Istanbul"
        country = "Turkey"

%%%

.# Abstract 

This document describes a foundational schema for the otpauth URI,
utilized by TOTP (and/or HOTP) based authenticators.

{mainmatter}


# Introduction {#Introduction}

The otpauth URI is used for easy addition of accounts to TOTP (and/or HOTP)
authenticators with various options [@Google.Authenticator.OSS.Wiki.Key.Format].

Although available as a provisional scheme at IANA [@IANA.URISchemes.Prov.otpauth],
there are many divisions of the usage specification per authenticator hardware and software
[@Edent.Blog.Post].

This document aims to provide foundational boundaries for the URI format and standardize
the secret sharing of OTP tokens.

## Conventions and Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED",
"MAY", and "OPTIONAL" in this document are to be interpreted as
described in BCP 14 [@!RFC2119] [@!RFC8174] when, and only when, they
appear in all capitals, as shown here.

This specification uses the Augmented Backus-Naur Form (ABNF) notation
of [@!RFC5234].

This specification uses the terms "TOTP" defined by [@!RFC6238] and "HOTP"
defined by [@!RFC4226]. Both RFCs also mention "secret", "issuer", "account".

The term "URI" is imported from [@!RFC9110].

# Objectives {#objective}

**todo(ilteris)**: continue

# Concept 

**todo(ilteris)**: continue

{backmatter}

# Acknowledgements {#Acknowledgements}
      
We would like to thank
The Google Authenticator Team at Google,
and others (please let us know, if you've been mistakenly omitted)
for their valuable input, feedback and general support of this work.

This document originated from discussions at the Fediverse initially
written by Terrence Eden.

# Document History

   [[ To be removed from the final specification ]]

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
   <author><fullname>Terrence Eden</fullname></author>
 </front>
</reference>

<reference anchor="Edent.Blog.Post" target="https://shkspr.mobi/blog/2022/05/why-is-there-no-formal-specification-for-otpauth-urls/">
 <front>
   <title>Why is there no formal specification for otpauth URls?</title>
   <author><fullname>Terrence Eden</fullname></author>
 </front>
</reference>