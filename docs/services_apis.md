# Services API #

Services are the things that run in n.io and where you connect your configured blocks together to make interesting things happen. Earlier we created a service called ``SimulateAndLog`` where we connected a CounterIntervalSimulator to a Logger block. Information and interaction with the services of a running n.io instance is available through the services API.

## Get API ##

The get API returns a json body with information about a serivce based on its name. The following example gets the information for the service ``SimulateAndLog``:

    curl -XGET 'http://localhost:8181/services/SimulateAndLog' --user 'Admin:Admin'

The result of the previous request is:

<dl>
  <dt>    {</dt>
  <dd>
    <p>{</p>
    <p>"type": "Service",</p>
    <p>"version": "1.0.0",</p>
    <p>"name": "SimulateAndLog",</p>
    <p>"log_level": "NOTSET",</p>
    <p>"auto_start": false,</p>
    <p>"status": "stopped",</p>
    <p>"execution": [</p>
    <p>{</p>
    <p>"name": "Simulate",</p>
    <p>"receivers": {</p>
    <p>"__default_terminal_value": [</p>
    <p>{</p>
    <p>"name": "Log",</p>
    <p>"input": "__default_terminal_value"</p>
    <p>}</p>
    <p>]</p>
    <p>}</p>
    <p>},</p>
    <p>{</p>
    <p>"name": "Log",</p>
    <p>"receivers": []</p>
    <p>}</p>
    <p>],</p>
    <p>"mappings": [],</p>
    <p>"sys_metadata": "{\"Simulate\":{\"locX\":248,\"locY\":102},\"Log\":{\"locX\":202,\"locY\":210}}"</p>
    <p>}</p>
  </dd>
</dl>
<dl>
  <dt>type</dt>
  <dd>The service type of the service configuration. Generally, this will simply be ``Service``.</dd>
</dl>
<dl>
  <dt>version</dt>
  <dd>The version of the service type when the service configuration was created.</dd>
</dl>
<dl>
  <dt>name</dt>
  <dd>The name of the service configuration. This must be unique among all services.</dd>
</dl>
<dl>
  <dt>log_level</dt>
  <dd>Level at which the service logs messages. Messages are logged for the specified ``log_level`` and all higher level.</dd>
</dl>
<dl>
  <dt>auto_start</dt>
  <dd>Boolean that indicates if the services will start when n.io starts up.</dd>
</dl>
<dl>
  <dt>status</dt>
  <dd>Current status of the service: configuring, configured, starting, started, stopping, stopped and error</dd>
</dl>
<dl>
  <dt>execution</dt>
  <dd>Configuration of how blocks are connected to each other within the service. It is a list of dictionaries that specify a block ``name`` and the blocks it sends signals to, specified as ``receivers``. The ``receivers`` specify why output signals are coming from on the source block and which input signals are going to on the receiving block.</dd>
</dl>
<dl>
  <dt>mappings</dt>
  <dd>When a single block configuration is used multiple times in a service, a new local name is created for each additional use of that block. Those new names are specifed here.</dd>
</dl>
<dl>
  <dt>sys_metadata</dt>
  <dd>Used by the builder to store block locations on the screen.</dd>
</dl>
## Get All API ##

In addition to getting the details of one service configuration, specified by name, you can get the details of all serivce configurations in one request:

    curl -XGET 'http://localhost:8181/services' --user 'Admin:Admin'

## Create API ##

If you're working with a n.io project from scrach, you're going to be creating and configuring services. Create a new service with the create API by POSTing JSON data. When creating a new service, you can optionally include the configured values of the service type properties. At a minimum, you must specify the service ``type``, the ``name`` of the new configuration and values for any required properties that do not have a default value. For example, to create the ``ServiceAndLog`` service of the basic type ``Service``:

    curl -XPOST 'http://localhost:8181/services' --user 'Admin:Admin' --data '{"type": "Service", "name": "SimulateAndLog"}' -H 'Content-Type: applcation/json'

## Update API ##

When you want to update the configuration of a serivce configuration, PUT the json data to the service name. You only need to PUT the properties that you are updating:

    curl -XPUT 'http://localhost:8181/services/SimulateAndLog' --user 'Admin:Admin' --data '{"log_level": "DEBUG"}' -H 'Content-Type: applcation/json'

## Delete API ##

Naturally, you'll make mistakes or refactor and want to delete a service:

    curl -XDELETE 'http://localhost:8181/services/SimulateAndLog' --user 'Admin:Admin'
