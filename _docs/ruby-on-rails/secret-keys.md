---
title: "Secret Keys"
layout: blog
order: 4
topic: Ruby
topic_path: /docs/ruby/index.html
---
Rails 6 uses credentials to manage secrets, such as API keys. Encrypted credentials are stored in the repository, and a master key is used to decrypt the credentials. The secret key is added to the `.gitignore` and therefore is not included in the repository, however it is a lot easier to share a secret key than to share a list of credentials.

To edit the secret key
```bash
EDITOR='nano' bin/rails credentials:edit
```

`nano` is a command line text editor. A different text editor can be specified, such as Sublime. Note you will need to pass in a `wait` flag to use Sublime.