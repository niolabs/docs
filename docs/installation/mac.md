# Installing nio on <span class="allow-caps">MacOS</span>

> **[info] <span class="allow-caps">Mac</span> System Requirements**
>
> **Version 10.9, Maverick, or above**<br>
> Click **Apple Menu > About this Mac** to view your MacOS version.
>
> **Clang** or similar C compiler<br>
> In your terminal (**Applications > Utilities > Terminal**), type `clang --version` to confirm that you have clang installed. If not, you can get it by
> installing [XCode](https://itunes.apple.com/us/app/xcode/id497799835?mt=12).
>

The nio Platform requires the following for local installation.
> **[info] nio Requirements**
>
> **Python version 3.4+**<br />
>    In your terminal (**Applications > Utilities > Terminal**), type `python3 --version` to see which version of Python 3 you have installed.
>    If you don't have Python 3 or have an older version, follow these instructions to [install Python 3 with HomeBrew](homebrew.md).

> **Pip**<br />
>    Pip is a package management system built for software written in Python. We recommend updating to the most recent version of pip3.<br />
>    In your terminal (**Applications > Utilities > Terminal**), type `pip3 --version` to see which version of pip you have installed.
>    Update to the most recent version of pip3 with the command: `pip3 install -U pip`.

> **Git**<br />
>    Git is a fast, scalable, distributed version-control system with a rich command set that the nio System Designer relies on for adding and updating blocks as part of your nio instance.<br />
>    In your terminal (**Applications > Utilities > Terminal**), type `git --version` to see if git is installed.
>    Follow this [installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to get started with Git.
>


You will also need the following, provided by nio:
{% include "/includes/nio-requirements.md" %}

---
## Installation

Open a terminal (**Applications > Utilities > Terminal**), and install nio using Python’s pip3 installer (verify the filepath and binary filename below—the `X`s represent the date of the binary in YYYYMMDD format):
```
pip3 install -U ~/Downloads/nio_lite-XXXXXXXX-py3-none-any.whl
```
You can test that nio is correctly installed by running the following command:
```
which niod
```

If you don’t see a path to niod, follow these instructions to [set your PATH in MacOS](path.md).

Once you have nio installed, you will need a project with a `nio.conf` file to run it against. Follow these instructions to [create a project](/running-nio/locally.md) and run nio.
