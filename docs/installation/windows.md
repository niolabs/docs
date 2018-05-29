# Installing nio on <span class="allow-caps">Windows</span>

> **[info] <span class="allow-caps">Windows</span> System Requirements**
>
> **Windows 7–10, Server 2008–2012**
>
> **A C++ compiler** available through http://landinghub.visualstudio.com/visual-cpp-build-tools.<br />
>   You have a C++ compiler available when you can open a **Developer Command Prompt** window and run the command `cl`.
>   If you do not have a C++ compiler available, follow the download instructions on the link provided above. Select: **Build Tools for Visual Studio** for download and follow the instrutions to install Build Tools for Visual Studio. 
>   Select Visual C++ build tools and click **Install**.
>   To confirm that everything installed correctly, you can now open a **Developer Command Prompt** and run `cl`.
>
> **Chocolatey** Package Manager (_recommended_ )<br />
> Check for an installation of Chocolatey with the command `choco --version` in your **Command Prompt**.
> To install Chocolatey, open an **Administratior Command Prompt** (right click on Command Prompt and select _Run as Administrator_), and run the following line:
>```
>@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
>```  
>
> **Git**<br />
>    Git is a fast, scalable, distributed version-control system with a rich command set that the nio System Designer relies on for adding and updating blocks as part of your nio instance.<br />
>    In your **Command Prompt**, type `git --version` to see if git is installed.
>    You can use Chocolatey to install git. Open an **Administratior Command Prompt** (right click on Command Prompt and select _Run as Administrator_), and run `choco install git`. Close and open the **Administrator Command Prompt** to see your changes and check your git version again.
>

The following must be in your environment to run nio. You can install these requirements globally if you have a dedicated, fresh machine running Python and nio. If you intend to run other Python projects on the same machine, we recommend you avoid version conflicts by using a separate Python environment containing these requirements.

> **[info] nio Requirements**
>
> **Python version 3.5+**<br />
>    In your **Command Prompt**, type `python --version` to see which version of Python you have installed.
>    If you do not have python3.5+, you can install it using Chocolatey. Open an **Administratior Command Prompt** (right click on Command Prompt and select _Run as Administrator_), and run `choco install python`. Close and open the **Administrator Command Prompt** to see your changes and check your python version again.

> **Pip**<br />
>    Pip is a package management system built for software written in Python. We recommend updating to the most recent version.<br />
>    In your **Command Prompt**, type `pip --version` to see which version of pip you have installed.
>    Update to the most recent version with the command: `python -m pip install -U pip`.


You will also need the following, provided by nio:
{% include "/includes/nio-requirements.md" %}

---
## Installation

Open a **Command Prompt**, and install nio using Python’s pip3 installer (substitute your filepath and binary filename below—the `X`s represent the date of the binary in YYYYMMDD format):
```
pip install Downloads\nio_lite-XXXXXXXX-py3-none-any.whl
```
You can test that nio is correctly installed by running the following command:
```
where niod
```
If you don’t see a path to niod, make sure Python’s binary directory is on your PATH.

> Follow this link [to update your PATH in Windows](https://msdn.microsoft.com/en-us/library/aa922003.aspx)

Once you have nio installed, you will need a project with a `nio.conf` file to run it against. Follow these instructions to [create a project](/running-nio/locally.md) and run nio.
