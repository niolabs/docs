In your terminal (**Applications > Utilities > Terminal**), find the location of your `niod` executable using the `pip3 show` command:

For Example:
```
pip3 show nio-full
```
Would return something similar to the following path under **Location**:
```
 /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages
 ```

Copy your path up to `/lib` and replace it with `/bin`. Using the example path above, your copied path would look something like:
```
 /Library/Frameworks/Python.framework/Versions/3.6/bin
 ```

Paste your copied path into the following command:

```
echo 'export PATH=$PATH:/paste/your/path/here'  >> ~/.bash_profile && source ~/.bash_profile
```

Now try the command `which niod`.

If you see a path to `niod`, the nio executable is now correctly part of your path.

Once you have nio installed, you will need a project with a `nio.conf` file to run it against. Follow these instructions to [create a project](/running-nio) and run nio.
