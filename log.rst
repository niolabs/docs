NIO log level component API
===============

Logger names retrieval
-------------------------

Logs can be retrieved through a GET call at the core or service level

1) core level
uri: http://[ip address]:[port]/log

2) service level
uri: http://[ip address]:[port]/log/service/[Service Name]


Changing log level
-------------------------

Log level can be changed through a POST or PUT call at the core or service level

1) core level
uri: http://[ip address]:[port]

body:
{"log_level": [New Log level],
 "logger_name": [Logger name]}

Example:
{"log_level": "DEBUG",
"logger_name": "Custom Scheduler"}

2) service level
uri: http://[ip address]:[port]/log/service/[Service Name]

body:
{"log_level": [New Log level],
 "logger_name": [Logger name]}

Example:
{"log_level": "INFO",
"logger_name": "Custom Scheduler"}


Note: For core and service level changes, if  'logger_name' parameter is
missing in the body, the level is changed across whole process
