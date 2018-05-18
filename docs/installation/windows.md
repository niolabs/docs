# Installing nio on <span class="allow-caps">Windows</span>

> **[info] <span class="allow-caps">Windows</span> System Requirements**
>
> **Windows 7–10, Server 2008–2012**
>
> **A C compiler** such as the one available through http://landinghub.visualstudio.com/visual-cpp-build-tools. You have a C compiler available when you can open a **Developer Command Prompt** window and type `cl.exe`.
>
> **Git**<br />
>    Git is a fast, scalable, distributed version-control system with a rich command set that the nio System Designer relies on for adding and updating blocks as part of your nio instance.<br />
>    In your terminal (Command Prompt/Developer Command Prompt), type `git --version` to see if git is installed.
>    If not, you can download git for windows on this [Git download page](https://git-scm.com/download/win).
>

The following must be in your environment to run nio. You can install these requirements globally if you have a dedicated, fresh machine running Python and nio. If you intend to run other Python projects on the same machine, we recommend you avoid version conflicts by using a separate Python environment containing these requirements.

> **[info] nio Requirements**
>
> **Python version 3.5+**<br />
>    In your terminal (Command Prompt/Developer Command Prompt), type `python --version` to see which version of Python you have installed.
>    If you don't have Python 3.5+ or have an older version, you can visit the [Python downloads page](https://www.python.org/downloads/).
>    During installation, watch for on option to set your PATH and select it.
>

> **Pip**<br />
>    Pip is a package management system built for software written in Python. We recommend updating to the most recent version.<br />
>    In your terminal (Command Prompt/Developer Command Prompt), type `pip --version` to see which version of pip you have installed.
>    Update to the most recent version with the command: `python -m pip install -U pip`.


You will also need the following, provided by nio:
{% include "/includes/nio-requirements.md" %}

---
## Installation

Open a terminal (**Applications > Utilities > Terminal**), and install nio using Python’s pip3 installer (substitute your filepath and binary filename below—the `X`s represent the date of the binary in YYYYMMDD format):
```
pip install Downloads/nio_lite-XXXXXXXX-py3-none-any.whl
```
You can test that nio is correctly installed by running the following command:
```
where niod
```
If you don’t see a path to niod, make sure Python’s binary directory is on your PATH.

> Follow this link [to update your PATH in Windows](https://msdn.microsoft.com/en-us/library/aa922003.aspx)

Once you have nio installed, you will need a project with a `nio.conf` file to run it against. Follow these instructions to [create a project](/running-nio/locally.md) and run nio.
