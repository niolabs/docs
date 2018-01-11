# Install nio locally

The cloud is an easy way to get the nio Platform up and running, but to see the power of nio as a distributed system, you should install and run nio on a locally or at the edge.


>**[info] Requirements**
>
>Linux / MacOS
>* **Python3**: https://www.python.org/downloads (you need Python 3.4+)
>* **A nio binary**: https://app.n.io/binaries/download (you'll need to agree to the license)
>* **A Pubkeeper Server**: A step-by-step on how to create one can be found [here](/running-nio/in-the-cloud.md).
>
>Windows users, [click here for installation instructions](/installation/windows.md).
>

---

## Installation

Open a terminal (Applications > Utilities > Terminal on MacOS), and install nio using Python’s pip3 installer (verify the filepath and binary filename below- the X's represent the date of the binary in YYYMMDD format):

```
pip3 install -U ~/Downloads/nio_lite-XXXXXXXX-py3-none-any.whl
```

> MacOS Users: You may be prompted to install a dependency called "clang". This is a standard component that comes directly from Apple, so it's safe to click "OK" and re-run the command above.

You can test that nio is correctly installed by running the following command:

```
which niod
```

> If you don’t see a path to niod, make sure Python’s binary directory is on your PATH.

> Help setting your PATH: [Windows](https://msdn.microsoft.com/en-us/library/aa922003.aspx) / [MacOS](http://osxdaily.com/2014/08/14/add-new-path-to-path-command-line/).
