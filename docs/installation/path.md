In your terminal (**Applications > Utilities > Terminal**), find the location of nio:

```
pip3 show nio
```

Copy the path after the **Location:** heading to your clipboard. Pa

Copy this path and paste it into the following command:

```
echo 'export PATH=$PATH:/paste/your/path/here'  >> ~/.bash_profile
```

Close your terminal, open it again, then try `which niod`.

If you see a path to `niod`, nio is correctly installed.
