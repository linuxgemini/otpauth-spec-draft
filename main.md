%%%
title = "Usage specification of the otpauth URI format for TOTP and HOTP token generators"
abbrev = "otpauth URI"
ipr = "trust200902"
area = "Security"
workgroup = ""
keyword = ["security", "otpauth", "totp", "hotp"]

[seriesInfo]
name = "Internet-Draft"
value = "draft-ietf-otpauth-uri-23"
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

**TODO(ilteris)**: fillin

{mainmatter}


# Introduction {#Introduction}

**TODO(ilteris)**: fillin

## Conventions and Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED",
"MAY", and "OPTIONAL" in this document are to be interpreted as
described in BCP 14 [@!RFC2119] [@!RFC8174] when, and only when, they
appear in all capitals, as shown here.

This specification uses the Augmented Backus-Naur Form (ABNF) notation
of [@!RFC5234].

This specification uses the terms "TOTP" defined by [@!RFC6238] and "HOTP"
defined by [@!RFC4226].

The terms "request", "response", "header field", and "target URI"
are imported from [@!RFC9110].

This document contains non-normative examples of partial and complete HTTP messages.
Some examples use a single trailing backslash \ to indicate line wrapping for long values, as per [@RFC8792].
The \ character and leading spaces on wrapped lines are not part of the value.

{backmatter}