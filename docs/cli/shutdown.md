# Shutdown nio server

The `shutdown` command stops a running nio instance. This command is useful when running the nio Platform as a daemon process.

This command can be run from anywhere to shut down a currently running nio instance.

This command will default for instances running on port 8181. The `-p` flag can be used to shutdown instances on other ports.

---

## Example:

```bash
nio shutdown
```

---

## Example (custom port `8182`):

```bash
nio shutdown --instance-host https://localhost:8182
```
