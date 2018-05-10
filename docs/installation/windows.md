# Installing nio on <span class="allow-caps">Windows</span>

Your Windows machine should include the following:
> **[info] <span class="allow-caps">Windows</span> System Requirements**
>
> **Windows 7–10, Server 2008–2012**
>

The nio Platform requires a few basic dependencies for local installation.
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
where niod
```
If you don’t see a path to niod, make sure Python’s binary directory is on your PATH.

> Follow this link [to update your PATH in Windows](https://msdn.microsoft.com/en-us/library/aa922003.aspx)

Once you have nio installed, you will need a project to run it against. Follow these instructions to [run nio locally](/running-nio/locally.md) in a project.
