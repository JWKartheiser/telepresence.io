---
layout: doc
weight: 2
title: "Running local processes"
categories: reference
---

There are two ways you can have Telepresence run your local process.

### `--run`

`--run` takes one or more arguments and runs the resulting command, e.g. to run `ruby myserver.rb` you can do:

```console
$ telepresence --new-deployment example --run ruby myserver.rb
```

This process will have access to the environment variables, outgoing proxying and volumes proxied by Telepresence.

### `--run-shell`

`--run-shell` takes no arguments, it simply runs a `bash` process:

```console
$ telepresence --new-deployment example --run-shell
@minikube|$
```

Any process run inside the shell will have access to the environment variables, outgoing proxying and volumes proxied by Telepresence.
