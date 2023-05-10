# Usage specification of the `otpauth` URI format

This document defines a set specification for `otpauth` URI format, used by various
TOTP and HOTP token generators.

Written in markdown for the [mmark processor](https://github.com/mmarkdown/mmark).

## Compiling

### using Docker
From the root of this repository, run
```bash
docker run -v `pwd`:/data danielfett/markdown2rfc main.md
```
(see https://github.com/oauthstuff/markdown2rfc)

### without Docker
compile using mmark and xml2rfc: `mmark main.md > draft.xml; xml2rfc --html draft.xml`
