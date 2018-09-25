# Command

`command` or `co` allows you to command running nio instances from the terminal.

This command will default for instances running on port 8181. The `-p` flag can be used to command services from instances on other ports.

---

## Example:

```bash
nio command start simulate-and-log
```
starts the **simulate-and-log** service on your running nio instance.

---

## Example (custom port `8182`):

```bash
nio command stop simulate-and-log --instance-host https://localhost:8182
```
stops the **simulate-and-log** service on your running nio instance at port `8182`.
