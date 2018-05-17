# Installing nio on <span class="allow-caps">Windows</span>

> **[info] <span class="allow-caps">Windows</span> System Requirements**
>
> **Windows 7–10, Server 2008–2012**
> To check which version of windows you are running, follow the instructions here: https://support.microsoft.com/en-us/help/13443/windows-which-operating-system.
>

The nio Platform requires the following for local installation.
> **[info] nio Requirements**
>
> **Python version 3.5+**<br />
>    In your terminal (Command Prompt), type `python3 --version` to see which version of Python 3 you have installed.
>    If you don't have Python 3 or have an older version, you can visit the [Python downloads page](https://www.python.org/downloads/).

> **Pip**<br />
>    Pip is a package management system built for software written in Python. We recommend updating to the most recent version.<br />
>    In your terminal (Command Prompt), type `pip3 --version` to see which version of pip you have installed.
>    Update to the most recent version with the command: `python -m pip install -U pip`.

> **Git**<br />
>    Git is a fast, scalable, distributed version-control system with a rich command set that the nio System Designer relies on for adding and updating blocks as part of your nio instance.<br />
>    In your terminal (Command Prompt), type `git` to see if git is installed.
>    Follow this [installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to get started with Git.
>

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

Once you have nio installed, you will need a project to run it against. Follow these instructions to [create a project](/running-nio/locally.md) and run nio.
