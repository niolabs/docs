# Installing Pubkeeper Server on <span class="allow-caps">MacOS</span>

> **[info] <span class="allow-caps">Mac</span> System Requirements**
>
> **Version 10.9, Maverick, or above**<br>
> Click **Apple Menu > About this Mac** to view your MacOS version.
>
> **Clang** or similar C compiler<br>
> In your terminal (**Applications > Utilities > Terminal**), type `clang --version` to confirm that you have clang installed. If you do not, you can get it by
> installing Xcode Command Line Tools by entering `xcode-select --install` into your terminal.
>
>

The following must be in your environment to run Pubkeeper Server. You can install these requirements globally if you have a dedicated, fresh machine running Python and Pubkeeper Server. If you intend to run other Python projects on the same machine, we recommend you avoid version conflicts by using a separate Python environment containing these requirements.

> **[info] Pubkeeper Server Requirements**
>
> **Python version 3.4-3.6**<br />
>    In your terminal (**Applications > Utilities > Terminal**), type `python3 --version` to see which version of Python 3 you have installed.<br>
>    If you don't have Python 3 or have an older version, [download Python 3](https://www.python.org/downloads/).<br>
>    Complete the installation process of Python 3.6+ by double clicking the **Install Certificates.command** file in your **Applications > Python 3.6** folder.

> **Pip**<br />
>    Pip is a package management system built for software written in Python. We recommend updating to the most recent version of pip3.<br>
>    In your terminal (**Applications > Utilities > Terminal**), type `pip3 --version` to see which version of pip you have installed.<br>
>    If you do not have pip installed you can do so by typing `curl https://bootstrap.pypa.io/get-pip.py | python3` into your terminal.<br>
>    Update to the most recent version of pip3 with the command: `pip3 install -U pip`.

You will also need the following, provided by niolabs:
{% include "/includes/pubkeeper-requirements.md" %}

---
## Installation

Open a terminal (**Applications > Utilities > Terminal**), and install nio using Python’s pip3 installer (substitute your filepath and binary filename below—the `X`s represent the version of the binary):
```
pip3 install -U ~/Downloads/pubkeeper.server.core-X.X.X-py3-none-any.whl
```
You can test that Pubkeeper Server is correctly installed by running the following command:
```
which pk_server
```

If you don’t see a path to pk_server, follow these instructions to [set your PATH in MacOS](path.md).
