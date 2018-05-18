# Installing nio on <span class="allow-caps">Linux</span>

> **[info] <span class="allow-caps">Linux</span> System Requirements**
>
> **Kernel 3.0**
>
> **GCC** or similar C compiler
>
> **APT** or similar package manager
>
> **Git**<br />
>    Git is a fast, scalable, distributed version-control system with a rich command set that the nio System Designer relies on for adding and updating blocks as part of your nio instance.<br />
>    In your terminal, type `git --version` to see if git is installed.<br>
>    Follow this [installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to get started with Git.
>

The following must be in your environment to run nio. You can install these requirements globally if you have a dedicated, fresh machine running Python and nio. If you intend to run other Python projects on the same machine, we recommend you avoid version conflicts by using a separate Python environment containing these requirements.

The nio Platform requires the following for local installation.
> **[info] nio Requirements**
>
> **Python version 3.4+**<br />
>    In your terminal, type `python3 --version` to see which version of Python 3 you have installed.<br>
>    If you don't have Python 3 or have an older version, [download Python 3](https://www.python.org/downloads/).<br>
>    Complete the installation process of Python 3.6+ by double clicking the **Install Certificates.command** file in your **Applications > Python 3.6** folder.

> **Pip**<br />
>    Pip is a package management system built for software written in Python. We recommend updating to the most recent version of pip3.<br>
>    In your terminal, type `pip3 --version` to see which version of pip you have installed.<br>
>    Update to the most recent version of pip3 with the command: `pip3 install -U pip`.


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

Once you have nio installed, you will need a project with a `nio.conf` file to run it against. Follow these instructions to [create a project](/running-nio/locally.md) and run nio.
