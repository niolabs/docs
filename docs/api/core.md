# Core APIs #

n.io has a few crucial api endpoints: ``/n.io`` and ``/shutdown``.

## n.io API ##

The ``/n.io`` endpoint is where you will find information about your running n.io instances:

    curl -XGET 'localhost:8181/n.io'

The following json body is returned:

<dl>
  <dt>    {</dt>
  <dd>
    <p>{</p>
    <p>"start_time": "2016-05-04 18:26:46.093569",</p>
    <p>"n.io": {</p>
    <p>"binary": "n.io_full",</p>
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
- ``start_time`` - Datetime string at which n.io was started.
- ``n.io``
  
  - ``binary`` - Name of executable binary that was run against the project.
  - ``build`` - Build version of binary.
  - ``version`` - Version of n.io framework, not to be confused with ``build`` which is the version of the ``binary``.
    


## Shutdown API ##

The ``/shutdown`` endpoint is used to shutdown a running n.io instance.

    curl -XGET 'localhost:8181/n.io'

The following html is returned on a successful shutdown:

    Shutdown complete
