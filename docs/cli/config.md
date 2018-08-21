# Config

The `config` or `cfg` command displays the configuration of any block or service within your running nio instance. The configuration is returned from the nio Platform in JSON format and displayed.

When run without any parameters or with the optional `project` parameter, you will be prompted to enter configuration for Pubkeeper. These values are optional. Pressing enter without typing in configuration values will not change the corresponding fields in `nio.conf`.

The `project` option of this command must be run from the root level of your nio project directory.

The `blocks` and `services` option of this command will default for instances running on port 8181. The `-p` flag can be used to list block or service configurations from instances on other ports.

---

## Example (blocks):

```bash
nio cfg blocks Simulate
```
returns the following JSON:
```
{
  'log_level': 'NOTSET',
  'total_signals': -1,
  'num_signals': 1,
  'attr_name': 'sim',
  'type': 'CounterIntervalSimulator',
  'name': 'Simulate',
  'version': '1.3.0',
  'interval': { 'days': 0, 'seconds': 1, 'microseconds': 0 },
  'attr_value': { 'end': 1, 'step': 1, 'start': 0 }
}
```

---

## Example (services):

```bash
nio cfg services simulate-and-log
```
returns the following JSON:
```
{
  'sys_metadata': '{
    "Simulate": { "locX":443,"locY":238 },
    "Log":{ "locX":398,"locY":477 }
  }',
  'mappings': [],
  'auto_start': True,
  'log_level': 'NOTSET',
  'type': 'Service',
  'version': '0.1.0',
  'name': 'simulate-and-log',
  'execution': [{
    'receivers': {
      '__default_terminal_value': [{
        'input': '__default_terminal_value',
        'name': 'Log'
      }]
    },
    'name': 'Simulate'
  },
  {
    'receivers': {},
    'name': 'Log'
  }],
  'status': 'stopped'
}
```

---

## Example (project):

```bash
nio cfg project --ip <ip> --port <port> --username <username> --password <password> --pubkeeper-hostname <hostname> --pubkeeper-token <token> --ssl
```

Your instance hostname and runtime port can be specified with `--ip` and `--port`. When these flags are set, nio will configure to run at `ip:port` rather than the default `0.0.0.0:8181`. The changes made from these flags are reflected in your project `nio.conf` file under the `[user_defined]` section.

Pubkeeper communication settings can be added using the `--pubkeeper-hostname` and `--pubkeeper-token` options. When these are set, your nio instance will configure to connect to a specified Pubkeeper server for system wide communication. The changes made from these flags are reflected in your project `nio.conf` file under the `[user_defined]` section.

Instance authentication can be configured by passing `--username` and `--password` options. This will update the authentication used by your instance for all HTTP requests. By default, instances use basic authentication credentials (Admin:Admin) to authorize access. The changes made from these flags are reflected in your project `etc/users.json` and `etc/permissions.json` files.

Additionally, a `--ssl` flag can be passed to create and/or install an SSL certificate for your nio instance.  This allows you to configure your nio instance with an additional layer of security and enables the nio System Designer to connect via HTTPS.  For more information on SSL certificates and their application, follow this [link](https://www.globalsign.com/en/ssl-information-center/what-is-an-ssl-certificate/).
