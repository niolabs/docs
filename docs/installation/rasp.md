# Installing nio on a <span class="allow-caps">Raspberry Pi</span>

> **[info] <span class="allow-caps">Raspbian</span> System Requirements**
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

From the command line, type
```
pip3 install -U ~/Downloads/nio_lite-XXXXXXXX-py3-none-any.whl
```
You can test that nio is correctly installed by running the following command:
```
which niod
```
You should see a path to niod.

Once you have nio installed, you will need a project with a `nio.conf` file to run it against. Follow these instructions to [create a project](/running-nio/locally.md) and run nio.
