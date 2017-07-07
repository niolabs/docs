# Setup #

## Setup ##

This section provides information on how to install nio, configure it to your liking and get it running.

### n.io binaries ###

n.io has many varieties in the form of installable and runable binaries. While each binary uses the same n.io Framework and blocks, the functionality and features of a binary can vary greatly. For example, one binary may have minimal features for the sake of running on lower power devices, while another may incorporate a plethora of security enhancements for running in an enterprise environment.

When you install the binary, the required n.io Framework and other Python dependences will be installed as well.

### Supported platforms ###

n.io can run on any computer with Python 3.4 (or greater), the ability to pip install additional (but minimal Python libraries) and a file system.

### Installation ###

After downloading a n.io binary, use pip to install it:

    pip3 install <nio-binary.whl>

You will also want to install the n.io CLI to assist in the creation and running of a n.io project:

    pip3 install nio-cli

### Creating and running a project ###

Create a project with the n.io CLI and the run nio from the root of that project:

<dl>
  <dt>    nio new first_project</dt>
  <dd>
    <p>nio new first_project</p>
    <p>cd first_project</p>
    <p>nio server</p>
  </dd>
</dl>
### Running as a daemon ###

To run n.io in the background, use the `-d` flag:

    nio server -d

## Configuration ##

n.io configuration settings generally exist at the root of your project directory.

### n.io settings ###

Most configuration exists in the file ``nio.conf`` at the root of your project. The configuration format is INI.

#### communication ####

When running a network of n.io devices, keep one as the master broker and configure the others to talk to it:

<dl>
  <dt>    [communication]</dt>
  <dd>
    <p>[communication]</p>
    <p>master=false</p>
    <p>broker_ip_address=192.168.100.41</p>
  </dd>
</dl>
#### service ####

If you have services that auto-start when n.io boots up and it is running on a slow device (like a Raspberry Pi), you may want those services to start in series to help with the CPU hit:

<dl>
  <dt>    [service]</dt>
  <dd>
    <p>[service]</p>
    <p>async_start=false</p>
  </dd>
</dl>
#### rest ####

If you want the n.io REST API to run on a different port, perhaps because you have multiple n.io instances on one computer:

<dl>
  <dt>    [rest]</dt>
  <dd>
    <p>[rest]</p>
    <p>port=8182</p>
  </dd>
</dl>
### n.io environment variables ###

You can specify project specific environement variables to be used in configuration files. These variables can used in ``nio.conf``, logging config and block and service property configurations. The values of these variables are not accessible through the n.io REST API so they are a good place for things that need to be kept private. It is common to use these environment variables so that you can run the same project in different environments and change the behavior simply by referencing a different variable file.

The default environment variable file is ``nio.env`` and is located at the project root.

When starting n.io, specify a non-default environment variable file with the ``-e`` flag.

Popular variables and their meaning:

<dl>
  <dt>COMHOST</dt>
  <dd>The publically accessible IP address of the master broker.</dd>
</dl>
<dl>
  <dt>PROJECT_ROOT</dt>
  <dd>Automatically populated by n.io and used to reference files and directories relative to the project root.</dd>
</dl>
### Logging ###

n.io uses Python logging so the same documentation applies. By defauly, the logging file ``logging.json`` is in the ``etc`` directory of your project.

## Running as a Service on Linux ##

### Debian/Ubuntu ###

n.io can be run as a service using upstart. You'll place the job file ``nio.conf`` in ``/etc/init``.

You can modify this script, but something like this will work.

<dl>
  <dt>    description "n.io"</dt>
  <dd>
    <p>description "n.io"</p>
    <p>author      "n.io"</p>
    <p>start on filesystem or runlevel [2345]</p>
    <p>stop on shutdown</p>
    <p>script</p>
    <p>exec /usr/local/bin/nio_full -r /home/nio/nio/projects/main > /dev/null 2>> /var/log/nio.log</p>
    <p>end script</p>
    <p>pre-start script</p>
    <p>echo "[`date`] n.io server starting" >> /var/log/nio.log</p>
    <p>end script</p>
    <p>pre-stop script</p>
    <p>echo "[`date`] n.io server stopping" >> /var/log/nio.log</p>
    <p>end script</p>
  </dd>
</dl>
## Auto-starting n.io on Raspberry Pi (and other Operating Systems) ##

On a Raspberry Pi, get n.io to start on boot by running it in ``/etc/rc.local``. Add the following command before the last line:

    /usr/local/bin/nio_full -r /home/nio/nio/projects/main > /dev/null 2>> /var/log/nio.log &

Modify accordingly for different binaries and project directories.

## Project Directory Layout ##

<dl>
  <dt>=====================  =====================================  =========================</dt>
  <dd>
    <p>=====================================  =========================</p>
    <p>Type                      Description                  Default Location/File</p>
  </dd>
</dl>
=====================  =====================================  =========================
Project Configuration  Settings for n.io project               [[PROJECT_ROOT]]/nio.conf
Environment Variables  Variables to use in configuration      [[PROJECT_ROOT]]/nio.env
Blocks                 n.io blocks available to project        [[PROJECT_ROOT]]/blocks
Logs                   n.io core and service logs              [[PROJECT_ROOT]]/logs
# Other Configuration    Additional settings for logging, etc.  [[PROJECT_ROOT]]/etc #

=====================================  =========================
