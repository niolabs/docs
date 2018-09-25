# nio CLI

The nio command line interface (CLI) is a tool that simplifies many of the tasks needed to work with a local nio instance. This tool is included with your installed nio binary. The nio CLI is the primary tool for creating new nio projects, adding blocks to an existing project, and listing information about a running nio instance.

---

## Quick Examples

### [Create a new project](new.md)

```bash
nio new [your project name]
```

### [Add blocks to your project](add.md)

```bash
nio add [block name]
```

### [List services in a running instance](list.md)

```bash
nio ls services
```

### [Start/Stop services in a running instance](command.md)

```bash
nio command <start|stop> <service-id>
```
This section outlines all of the available CLI commands that can be used when running the nio Platform locally.

## Instance Access Arguments

Many of the CLI commands will access your nio instance's API. For example, the `nio list` commands will execute fetch (`GET`) requests to your nio instance. The host of this instance defaults to `https://localhost:8181` but can be configured with command line arguments.

### Custom nio Instance Host

This command will list the services running on an HTTP instance of nio running at myhost.com on port 8182.
```bash
nio list --instance-host http://myhost.com:8182 services
```

For SSL/HTTPS instances, you may need to pass the path to the certificate authority (CA) to verify your instance's SSL certificate. Do this with the `--ssl-ca-path` argument. This argument defaults to `~/.nio/ca.crt` which is where the local CA would be created if you used `nio new` or `nio config --ssl` to configure your instance.

```bash
nio list --instance-host https://customdomain.local:8181 --ssl-ca-path /private/certs/ca.pem services
```
