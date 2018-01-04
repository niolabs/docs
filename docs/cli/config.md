# Config

The `config` or `cfg` command will display the configuration of any block or service within your running nio instance. The configuration is returned from nio in JSON format and displayed.

Example (blocks):
```bash
nio cfg blocks Simulate
```
Will return the following JSON:
```
{'log_level': 'NOTSET', 'total_signals': -1, 'num_signals': 1, 'attr_name': 'sim', 'type': 'CounterIntervalSimulator', 'name': 'Simulate', 'version': '1.3.0', 'interval': {'days': 0, 'seconds': 1, 'microseconds': 0}, 'attr_value': {'end': 1, 'step': 1, 'start': 0}}
```

Example (services):
```bash
nio cfg services simulate-and-log
```
Will return the following JSON:
```
{'sys_metadata': '{"Simulate":{"locX":443,"locY":238},"Log":{"locX":398,"locY":477}}', 'mappings': [], 'auto_start': True, 'log_level': 'NOTSET', 'type': 'Service', 'version': '0.1.0', 'name': 'simulate-and-log', 'execution': [{'receivers': {'__default_terminal_value': [{'input': '__default_terminal_value', 'name': 'Log'}]}, 'name': 'Simulate'}, {'receivers': {}, 'name': 'Log'}], 'status': 'stopped'}
```
