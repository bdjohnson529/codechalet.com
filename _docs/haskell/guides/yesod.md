---
title: "Yesod blog"
layout: blog
topic: Haskell
topic_path: /docs/haskell/index.html
---
Instructions for building a Yesod blog, taken from [this tutorial.](https://www.youtube.com/watch?v=SadfV-qbVg8&t=39s)

# Setup
Create a new yesod project
```bash
stack new haskell-blog yesodweb/postgres
cd haskell-blog
```
Setup, build and run the server
```bash
stack build
stack exec -- yesod devel
```


# Sandboxes
Create a new sandbox, an isolated environment
```bash
cabal sandbox init
```

## References
* [Stack README](https://docs.haskellstack.org/en/stable/README/)