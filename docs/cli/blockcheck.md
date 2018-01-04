# Block Check

The `blockcheck` command will perform several checks on a block. This command is useful when developing you own custom block. When a new block successfully passes the block check it can be pulled into the official nio-blocks library.

This command must be called from the root level of the block directory. It will run checks against the formatting of the README, spec, and release files. The block code itself will also be checked against PEP8 formatting.

Example:
```bash
nio blockcheck
```
Will produce the following output for a correctly formatted block:
```
Checking PEP8 formatting ...

Checking spec.json formatting ...

Checking README.md formatting ...

Checking release.json formatting ...

Checking version formatting ...

Checking class and file name formatting ...
```
