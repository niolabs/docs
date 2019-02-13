Open a terminal (Applications > Utilities > Terminal on MacOS), and install nio using Python’s pip3 installer (verify the filepath and binary filename below—the `X`s represent the date of the binary in YYYYMMDD format):
```
pip3 install -U ~/Downloads/nio_full-XXXXXXXX-py3-none-any.whl
```
> MacOS Users: You may be prompted to install a dependency called "clang". This is a standard component that comes directly from Apple, so it's safe to click "OK" and re-run the command above.

You can test that nio is correctly installed by running the following command:
```
which niod
```
If you don’t see a path to niod, make sure Python’s binary directory is on your PATH.

> Help setting your PATH: [Windows](https://msdn.microsoft.com/en-us/library/aa922003.aspx) / [MacOS](http://osxdaily.com/2014/08/14/add-new-path-to-path-command-line/).
