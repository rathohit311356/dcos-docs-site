---
layout: layout.pug
navigationTitle:  dcos security secrets create
title: dcos security secrets create
menuWeight: 300
excerpt: Creating and storing a secret
enterprise: true
---

# Description

The `dcos security secrets create` command allows you to create and store secrets under a specific path.

# Options
 
| Name |  Description |
|---------|-------------|
|  `-h`, `--help` |  Show this message and exit.|
| `-s`, `--store-id <text> `  |          Secrets backend to use.|
|  `-v`, `--value <text> `     |          Value of the secret.|
|  `-t`, `--text-file`, `--value-file <filename>` |  Treat contents of the file as value of the secret. The contents are assumed to be text encoded via UTF-8.|
|  `-f`, `--file <filename>`   |     Use the raw file contents as the value of the secret: pass the unmodified byte sequence to DC/OS Secrets service.|

# Usage

```
Usage: dcos security secrets create [OPTIONS] PATH

  Create a secret.

  Store a secret under the path PATH.

Options:
  -s, --store-id TEXT             Secrets backend to use.
  -v, --value TEXT                Value of the secret.
  -t, --text-file, --value-file FILENAME
                                  Treat contents of the file as value of the
                                  secret. The contents are assumed to be text
                                  encoded via UTF-8.
  -f, --file FILENAME             Use the raw file contents as the value of
                                  the secret: pass the unmodified byte
                                  sequence to DC/OS Secrets service.
  -h, --help                      Show this message and exit.

  ```