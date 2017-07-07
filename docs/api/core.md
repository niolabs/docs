# Core APIs #

n.io has a few crucial api endpoints: ``/nio`` and ``/shutdown``.

## n.io API ##

The ``/nio`` endpoint is where you will find information about your running nio instances:

    curl -XGET 'localhost:8181/nio'

The following json body is returned:

<dl>
  <dt>    {</dt>
  <dd>
    <p>{</p>
    <p>"start_time": "2016-05-04 18:26:46.093569",</p>
    <p>"nio": {</p>
    <p>"binary": "nio_full",</p>
    <p>"build": "20160426",</p>
    <p>"version": "2.0.0b4"</p>
    <p>},</p>
    <p>"modules": {},</p>
    <p>"components": {</p>
    <p>"ProjectManager": {},</p>
    <p>"ManagementPublisher": {},</p>
    <p>"BlockManager": {},</p>
    <p>"LogManager": {},</p>
    <p>"ServiceExecutor": {},</p>
    <p>"ConfigMonitor": {},</p>
    <p>"RESTManager": {},</p>
    <p>"ServiceMonitor": {},</p>
    <p>"ServiceManager": {}</p>
    <p>}</p>
    <p>}</p>
  </dd>
</dl>
- ``start_time`` - Datetime string at which nio was started.
- ``nio``
  
  - ``binary`` - Name of executable binary that was run against the project.
  - ``build`` - Build version of binary.
  - ``version`` - Version of nio framework, not to be confused with ``build`` which is the version of the ``binary``.
    


## Shutdown API ##

The ``/shutdown`` endpoint is used to shutdown a running n.io instance.

    curl -XGET 'localhost:8181/nio'

The following html is returned on a successful shutdown:

    Shutdown complete
