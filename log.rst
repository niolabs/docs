NIO log level component API
===============

Logger names retrieval
-------------------------

Logs can be retrieved through a GET call at the core or service level

core level
uri: http://[ip address]:[port]/log

service level
uri: http://[ip address]:[port]/log/service/[Service Name]


Changing log level
-------------------------

Log level can be changed through a POST or PUT call at the core or service level

core level
uri: http://[ip address]:[port]

body:
{"log_level": [New Log level],
 "logger_name": [Logger name]}

Example:
{"log_level": "DEBUG",
"logger_name": "Custom Scheduler"}


service level
uri: http://[ip address]:[port]/log/service/[Service Name]

body:
{"log_level": [New Log level],
 "logger_name": [Logger name]}

Example:
{"log_level": "INFO",
"logger_name": "Custom Scheduler"}
