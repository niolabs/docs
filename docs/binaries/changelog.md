# nio binary changelog


---
## 20180524

**Added**<br>
- updated package metadata shown in `pip3 show nio-lite`
- block properties have an `advanced` option for display purposes

**Changed**<br>
- updated `component_project_manager` removes failed block download folders
- **Block and service config name changes** will rename old v3.0.0 configs with a more human friendly label
- Replace time calculations using datetime with a monotonic time
---
## 20180425

**Added**<br>
- nio framework to use id for services and blocks
- Backwards compatibility: an id will be generated if has none
- updated `component_log_api` to be able to query by id

**Changed**<br>
- execution / receiver / mappings to use `id` rather than `name`

----
## 20180309

**Changed**<br>
None

**Added**<br>
None

**Fixed**<br>
 * New binaries which contain pubkeeper_server pin it to v1.0.3
 * Pubkeeper server doesn't set DEBUG log level for all loggers anymore
 * Pin pyjwt version to 1.5.x

----
## 20180305

**Changed**<br>
None

**Added**<br>
 * Allows for aliasing of pubkeeper brews—you can now have your nio instance run multiple brews from the same brew class. For example, connect to multiple websocket servers.

**Fixed**<br>
 * pubkeeper client version 1.0.3 - pins version of tornado library to 4.5.x

----
## 20180301

**Changed**<br>
None

**Added**<br>
None

**Fixed**<br>
 * Log API Component - Requesting a service with no log files no longer returns an error (NIO-1052)

----
## 20180228

**Changed**<br>
None

**Added**<br>
None

**Fixed**<br>
 * Pubkeeper client bump to 1.0.2 - brew in the ioloop to prevent bad thread access

----
## 20180213
**Changed**<br>
None

**New Features**<br>
 * component_environment update to PUT to replace all existing user defined variables

**Fixed**<br>
None

----
## 20180207

**Changed**<br>
None

**New Features**<br>
None

**Fixed**<br>
 * cherrypy custom error page to return json response rather than html

----
## 20180130

**Changed**<br>
None

**New Features**<br>
None

**Fixed**<br>
 * Better cherrypy logging. Control cherrypy loggers via main.cherrypy and main.cherrypy.access in your project's /etc/logging.json file
