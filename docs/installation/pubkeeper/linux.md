# Installing Pubkeeper Server on <span class="allow-caps">Linux</span>

> **[info] <span class="allow-caps">Linux</span> System Requirements**
>
> **Linux kernel version 3.0+**<br />
> Check your kernel version by typing the command `uname -r` into your terminal.
>
> **GCC** or similar C compiler<br />
> Check for an installation of GCC by typing the command `gcc --version` into your terminal.<br>
> If you do not have a C complier, follow the instructions to install GCC [here](https://gcc.gnu.org/wiki/InstallingGCC).
>
> **APT** or similar package tool (_recommended_ ).
>

The following must be in your environment to run Pubkeeper Server. You can install these requirements globally if you have a dedicated, fresh machine running Python and Pubkeeper Server. If you intend to run other Python projects on the same machine, we recommend you avoid version conflicts by using a separate Python environment containing these requirements.

Pubkeeper Server requires the following for local installation.
> **[info] Pubkeeper Server Requirements**
>
> **Python version 3.4+**<br />
>    In your terminal, type `python3 --version` to see which version of Python 3 you have installed.<br>
>    If you don't have Python 3 or have an older version, download Python 3 by typing the following command in your terminal `sudo apt install python3`.<br>

> **Pip**<br />
>    Pip is a package management system built for software written in Python. We recommend updating to the most recent version of pip3.<br>
>    In your terminal, type `pip3 --version` to see which version of pip you have installed.<br>
>    If you do not have pip installed you can do so by typing the following command into your terminal:<br> 
>   `sudo apt install python3-pip`<br>
>    Update to the most recent version of pip3 with the command: `pip3 install -U pip`.


You will also need the following, provided by niolabs:
{% include "/includes/pubkeeper-requirements.md" %}

---
## Installation

Open a terminal, and install nio using Python’s pip3 installer (substitute your filepath and binary filename below—the `X`s represent the version of the binary):
```
pip3 install -U pubkeeper.server.core-X.X.X-py3-none-any.whl
```
You can test that Pubkeeper Server is correctly installed by running the following command:
```
which pk_server
```
If you don’t see a path to pk_server, make sure Python’s binary directory is on your PATH.
