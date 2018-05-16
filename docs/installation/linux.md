# Installing nio on <span class="allow-caps">Linux</span>

> **[info] <span class="allow-caps">Linux</span> System Requirements**
>
> **Kernel 3.0**
>
> **GCC** or similar C compiler
>
> **APT** or similar package manager

The nio Platform requires the following for local installation.
{% include "/includes/basic-requirements.md" %}

You will also need the following, provided by nio:
{% include "/includes/nio-requirements.md" %}

---
## Installation

Open a terminal and install nio using Python’s pip3 installer (verify the filepath and binary filename below—the `X`s represent the date of the binary in YYYYMMDD format):
```
pip3 install -U ~/Downloads/nio_lite-XXXXXXXX-py3-none-any.whl
```
You can test that nio is correctly installed by running the following command:
```
which niod
```
If you don’t see a path to niod, make sure Python’s binary directory is on your PATH.

Once you have nio installed, you will need a project to run it against. Follow these instructions to [create a project](/running-nio/locally.md) and run nio.
