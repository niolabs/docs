# Long-Running

When you're ready to deploy your project, you will probably need a nio instance that starts automatically with the host system and keeps running. Whether that host is a cloud server, a Raspberry Pi, or anywhere in between, the operating system will offer a few methods to control the running nio Platform. In addition to platform-independent options such as Docker, this document covers the basic configuration of nio system services for Linux, MacOS, and Windows.

---
## Run with <span class="allow-caps">Docker</span>

Running the nio Platform as a Docker container allows you to manage its lifecycle through standard Docker deployment practices and use orchestration managers like Kubernetes. Check out our [guide to running nio with Docker](/deployment/third-party/docker.md) for more information on how to do this.

>**[info] Note**
>
>In the following examples, items inside `< ... >` need to be replaced with the actual values for your system. For example, `<my_project>` is replaced with the name you used when creating the project with `nio new <my_project> ...`, and on a Raspberry Pi `<user>` will often be replaced with the default user `pi`.

---
## Linux, MacOS - Run nio in the background

When you run `niod` from the project root without any other shell options the nio instance will die if your terminal is closed or your SSH session disconnects. To prevent this, you can run nio in the background on MacOS and Linux using `nohup`. This will not start an instance automatically.

```
nohup niod 2>&1 > /dev/null &
```

Or, `niod` can be run from outside the project root directory:

```
nohup niod -r /home/<user>/nio/projects/<my_project> 2>&1 > /dev/null & 
```

---
## Linux - Run nio with systemd

[**systemd**](https://wiki.debian.org/systemd) is an **init** system that comes included with many Linux distributions. Running nio as a systemd service will start it automatically with the system, and allows you to manage the instance using [systemctl](https://manpages.debian.org/stretch/systemd/systemctl.1.en.html).

To create a `systemd` service for nio, create a new file: `sudo nano /etc/systemd/system/<my_project>.service`, replacing `<my_project>` with the actual name of your project. `nano` is a basic text editor, when it launches you will see an empty file with controls along the bottom of the screen. Copy and paste the following into the empty file:

```
[Unit]
Description=<my_project>
After=network.target

[Service]
WorkingDirectory=/home/<user>/nio/projects/<my_project>
ExecStart=/home/<user>/nio/env/bin/niod
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=always

[Install]
WantedBy=multi-user.target
```

Use the arrow keys to move your cursor around the file, and:
1) Update `Description=`, replace `<my_project>` with the name of your nio project.
1) Update `WorkingDirectory=`, the absolute path to the nio project.
1) Update `ExecStart=`, the absolute path to the installed `niod` executable. If you are using a [virtual environment](/deployment/best-practices/) (highly recommended) use the path to `niod` within that environment.

Press `Ctrl X` to exit, followed by `Y` and `Enter` to save changes, and then enable the new service with the following commands:

```
sudo systemctl daemon-reload
sudo systemctl enable <my_project>.service
```

The nio project given in `WorkingDirectory` will be started automatically with the system (using the executable and packages installed at `ExecStart`), but has not been started yet.

```
sudo systemctl start <my_project>.service
```

Stopping is similar:
```
sudo systemctl stop <my_project>.service
```

Check the status and recent logs of your nio instance with
```
sudo systemctl status <my_project>.service
```

## Windows - Run nio as a Service

To run as a Service on a Windows host machine, the `niod` executable needs an interface (wrapper) through which the operating system can send commands and get a status of the running process. This wrapper is provided by niolabs in this [github repository](https://github.com/niolabs/nio_winservice).

{% include "https://github.com/niolabs/nio_winservice/blob/master/README.md" %}
