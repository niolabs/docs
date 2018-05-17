In your terminal (**Applications > Utilities > Terminal**), find the location of nio:

```
pip3 show nio
```

Copy the path after the **Location** heading to your clipboard.

Paste the location path into the following command:

```
echo 'export PATH=$PATH:/paste/your/path/here'  >> ~/.bash_profile
```

Close your terminal, open it again, then try `which niod`.

If you see a path to `niod`, nio is correctly installed.

Once you have nio installed, you will need a project with a `nio.conf` file to run it against. Follow these instructions to [create a project](/running-nio/locally.md) and run nio.
