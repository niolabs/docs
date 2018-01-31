# Command

`command` or `co` allows you to command running nio instances from the terminal.

This command will default for instances running on port 8181. The `-p` flag can be used to command services from instances on other ports.

Example:
```bash
nio command start simulate-and-log
```  
starts the **simulate-and-log** service on your running nio instance.

Example (port `8282`):
```bash
nio command stop simulate-and-log -p 8282
```
stops the **simulate-and-log** service on your running nio instance at port `8282`.
