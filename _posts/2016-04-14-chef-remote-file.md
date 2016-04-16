---
layout: post
title: Underscores in URIs
summary: TIL about underscores in URIs and how Chef treats them
---
# URIs
According to [RFC 3986](https://tools.ietf.org/html/rfc3986) _Uniform Resource Identifier (URI): Generic Syntax_ section 2.3, underscores are considered valid in URIs.

```
Characters that are allowed in a URI but do not have a reserved
   purpose are called unreserved.  These include uppercase and lowercase
   letters, decimal digits, hyphen, period, underscore, and tilde.

      unreserved  = ALPHA / DIGIT / "-" / "." / "_" / "~"
```

# `remote_file` resource
I was testing my call to `remote_file` with a dummy URI for `source`, `http://dummy_url.com`, and the test [failed](https://github.com/chef/chef/blob/c1a389c2a8452e9b796aa1d34c4d9e51f4af30c7/lib/chef/resource/remote_file.rb#L151). I was confused because I thought that the URI was valid, and I learned that Chef [doesn't think so](https://github.com/chef/chef/blob/c1a389c2a8452e9b796aa1d34c4d9e51f4af30c7/lib/chef/mixin/uris.rb#L29).
