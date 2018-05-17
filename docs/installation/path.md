In your terminal (**Applications > Utilities > Terminal**), find the location of nio:

```
pip3 show
```

You will see a path after the **location:** heading.

Copy this path and paste it into the following command: 

```
echo "export PATH:$PATH:/paste/your/path/here" >> ~/.bash_profile   
```
