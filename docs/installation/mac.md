# Installing nio on <span class="allow-caps">MacOS</span>

> **[info] <span class="allow-caps">Mac</span> System Requirements**
>
> **Version 10.9, Maverick, or above**
>
> **Clang** or similar C compiler, available by installing [XCode](https://itunes.apple.com/us/app/xcode/id497799835?mt=12)
>

The nio Platform requires the following for local installation.
{% include "/includes/basic-requirements.md" %}

You will also need the following, provided by nio:
{% include "/includes/nio-requirements.md" %}

---
## Installation

Open a terminal (Applications > Utilities > Terminal), and install nio using Python’s pip3 installer (verify the filepath and binary filename below—the `X`s represent the date of the binary in YYYYMMDD format):
```
pip3 install -U ~/Downloads/nio_lite-XXXXXXXX-py3-none-any.whl
```
You can test that nio is correctly installed by running the following command:
```
which niod
```

If you don’t see a path to niod, make sure Python’s binary directory is on your PATH.

>  [Set your PATH in MacOS](http://osxdaily.com/2014/08/14/add-new-path-to-path-command-line/).

Once you have nio installed, you will need a project to run it against. Follow these instructions to [create a project](/running-nio/locally.md) and run nio.

<br>
>**MacOS Users**: While your system comes pre-installed with Python, it is an older version. When installing newer versions, Python may require that you install and trust a set of Root Certificates for its SSL package. That file is located at `/Applications/Python 3.x/Install Certificates.command`. Just double-click that file to complete the process. Check `/Applications/Python 3.x/ReadMe.rtf` for more details.

>The error string you'll see will look something like this:

>```WARNING:tornado.general:SSL Error on 7 ('x.x.x.x', 443): [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed```
