# nio binary changelog

## 20180309

**Potentially breaking changes**<br>
None

**New features**<br>
None

**Fixes**<br>
New binaries which contain pubkeeper_server, pin it to v1.0.2.

## 20180305

**Potentially breaking changes**<br>
None

**New features**<br>
Allows for aliasing of pubkeeper brews—you can now have your nio instance run multiple brews from the same brew class. For example, connect to multiple websocket servers.

**Fixes**<br>
pubkeeper client version 1.0.3 - pins version of tornado library to 4.5.x

## 20180301

**Potentially breaking changes**<br>
None

**New features**<br>
None

**Fixes**<br>
Log API Component - Requesting a service with no log files no longer returns an error (NIO-1052)

## 20180228

**Potentially breaking changes**<br>
None

**New features**<br>
None

**Fixes**<br>
Pubkeeper client bump to 1.0.2 - brew in the ioloop to prevent bad thread access

## 20180213
**Potentially breaking changes**<br>
None

**New Features**<br>
component_environment update to PUT to replace all existing user defined variables

**Fixes**<br>
None

## 20180207

**Potentially breaking changes**<br>
None

**New Features**<br>
None

**Fixes**<br>
cherrypy custom error page to return json response rather than html


## 20180130

**Potentially breaking changes**<br>
None

**New Features**<br>
None

**Fixes**<br>
Better cherrypy logging. Control cherrypy loggers via main.cherrypy and main.cherrypy.access in your project's /etc/logging.json file
