Most RFC authoring guides are available at IETF Authors guide: https://authors.ietf.org/

This repository uses [`mmark`](https://mmark.miek.nl/post/syntax/) for the writing.

To add authorship, an example entry on the title area of `main.md` can be:

```toml
[[author]]
initials = "J."
surname = "Doe"
fullname = "John Doe"
organization = "independent"
    [author.address]
    email = "jdoe@example.org"
```
