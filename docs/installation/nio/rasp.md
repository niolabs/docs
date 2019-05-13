# Installing nio on a <span class="allow-caps">Raspberry Pi</span>

The easiest installation method is to run [this script](https://github.com/niolabs/nio_install) by following the instructions in the README of that github repository. This is recommended for most users and/or fresh [Raspbian images](https://www.raspberrypi.org/downloads/raspbian/). Otherwise, if you have an existing environment set up on your Pi, follow the instructions below.

> **[info] <span class="allow-caps">Raspbian</span> System Requirements**
>
> **GCC** or similar C compiler<br />
> Check for an installation of GCC by typing the command `gcc --version` into your terminal.<br>
> If you do not have a C complier, follow the instructions to install GCC [here](https://gcc.gnu.org/wiki/InstallingGCC).
>
> **Git 1.8.4 or later**<br />
>    Git is a fast, scalable, distributed version-control system with a rich command set that the nio System Designer relies on for adding and updating blocks as part of your nio instance.<br />
>    In your terminal, type `git --version` to see if git is installed.<br>
>    Follow this [installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to get started with Git.
>
> **APT** or similar package tool (_recommended_ )<br />
> Check for an installation of APT by typing the command `apt --version` into your terminal.
>

The following must be in your environment to run nio. You can install these requirements globally if you have a dedicated, fresh machine running Python and nio. If you intend to run other Python projects on the same machine, we recommend you avoid version conflicts by using a separate Python environment containing these requirements.

The nio Platform requires the following for local installation.
> **[info] nio Requirements**
>
> **Python version 3.4+**<br />
>    In your terminal, type `python3 --version` to see which version of Python 3 you have installed.<br>
>    If you don't have Python 3 or have an older version, download Python 3 by typing the following command in your terminal `sudo apt install python3`.<br>

> **Pip**<br />
>    Pip is a package management system built for software written in Python. We recommend updating to the most recent version of pip3.<br>
>    In your terminal, type `pip3 --version` to see which version of pip you have installed.<br>
>    If you do not have pip installed you can do so by running the following commands in your terminal:<br> 
>```
>wget https://bootstrap.pypa.io/get-pip.py
>python3 get-pip.py --user
>echo 'export PATH=/home/pi/.local/bin:$PATH' >> ~/.bashrc && source ~/.bashrc
>```
>    Or, update to the most recent version of pip3 with the following commands: 
>```
>curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
>python3 get-pip.py —-user
>echo 'export PATH=/home/pi/.local/bin:$PATH' >> ~/.bashrc && source ~/.bashrc
>```
>   After running these commands, typing `pip3 --version` should return with the most up to date version of the Pip package manager.
>


You will also need the following, provided by nio:
{% include "/includes/nio-requirements.md" %}

---
## Installation

Open a terminal, and install nio using Python’s pip3 installer (substitute your filepath and binary filename below—the `X`s represent the date of the binary in YYYYMMDD format):

From the command line, type
```
pip3 install -U ~/Downloads/nio_full-XXXXXXXX-py3-none-any.whl --user
```
You can test that nio is correctly installed by running the following command:
```
which niod
```
You should see a path to niod.

Once you have nio installed, you will need a project with a `nio.conf` file to run it against. Follow these instructions to [create a project](/running-nio) and run nio.
