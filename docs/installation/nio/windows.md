# Installing nio on <span class="allow-caps">Windows</span>

> **[info] <span class="allow-caps">Windows</span> System Requirements**
>
> **Windows 7–10, Server 2008–2012**
>
> **A C++ compiler** such as the one available [here](https://www.visualstudio.com/downloads/#build-tools-for-visual-studio-2017). Select the Download link for **Build Tools for Visual Studio 2017** and _Run_. Follow the on screen instructions, being sure to select **Visual C++ build tools** when prompted on the _Workloads_ tab, then click _Install_.<br> 
>   You have a C++ compiler available when you can open a **Developer Command Prompt** window and run the command `cl`. 
>   * This should be the only time you need to use a **Developer Command Prompt**. You can close this window after confirming a C++ compiler is available.
>
> **Git 1.8.4 or later**<br />
>    Git is a fast, scalable, distributed version-control system with a rich command set that the nio System Designer relies on for adding and updating blocks as part of your nio instance.<br />
>    In a **Command Prompt** , type `git --version` to see if git is installed.
>    If not, you can download git for windows on this [Git download page](https://git-scm.com/download/win) and follow the on screen instructions.
>    * When the install is complete, you can reopen a **Command Prompt** and check for a successful installation with `git --version`.
>

The following must be in your environment to run nio. You can install these requirements globally if you have a dedicated, fresh machine running Python and nio. If you intend to run other Python projects on the same machine, we recommend you avoid version conflicts by using a virtual Python environment containing these requirements.

> **[info] nio Requirements**
>
> **Python version 3.5-3.6**<br />
>    In a **Command Prompt**, type `python --version` to see which version of Python you have installed.
>    If you don't have a version of Python 3.5 or higher, you can visit the [Python downloads page](https://www.python.org/downloads/).
>   * **Note:** During the installation, watch for on option to set your PATH and select it.
>   * When the install is complete, you can reopen a **Command Prompt** and check for a successful installation with `python --version`.

> **Pip**<br />
>    Pip is a package management system built for software written in Python. We recommend updating to the most recent version.<br />
>    In a **Command Prompt**, type `pip --version` to see which version of pip you have installed.
>    Update to the most recent version with the command: `python -m pip install -U pip`.


You will also need the following, provided by nio:
{% include "/includes/nio-requirements.md" %}
>   If prompted, select to **Save** this file and not **Open**.

---
## Installation

Open a **Command Prompt**, and install nio using Python’s pip3 installer (substitute your filepath and binary filename below—the `X`s represent the date of the binary in YYYYMMDD format):
```
pip install Downloads/nio_lite-XXXXXXXX-py3-none-any.whl
```
You can test that nio is correctly installed by running the following command:
```
where niod
```

Once you have nio installed, you will need a project with a `nio.conf` file to run it against. Follow these instructions to [create a project](/running-nio) and run nio.
