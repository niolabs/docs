# Long Running nio Instances

Eventually you will want to run your nio instances for longer durations and have them be more resilient to network outages and system restarts. There are many ways to use existing tools to make this easier, here are a few recommended options.

## Run with Docker

Running nio as a Docker container allows you to manage its lifecycle through standard Docker deployment practices and use orchestration managers like Kubernetes. Check out our [guide to running nio with Docker](/running-nio/docker.md) for more information on how to do this.

## Run nio in the Background

When you run `niod` without any other shell options the nio instance will die if your terminal is closed or your SSH session disconnects. To prevent this, you can run nio in the background on MacOS and Linux using `nohup` like so:

```
nohup niod -r path/to/my_project 2>&1 > /dev/null &
```

## Run nio with systemd

systemd is an init system that comes included with many Linux distributions. Running nio as a systemd service allows you to manage the instance using standard `sysctl` commands.

To create a systemd service for running nio, create a new systemd service file in `/etc/systemd/system/nio.service`. Here is a template service file you can start with. You can find more systemd service options on the [official systemd documentation](https://www.freedesktop.org/software/systemd/man/systemd.service.html). Update the `WorkingDirectory` to the location of your nio project and make sure the executable path for `niod` is correct.

```
[Unit]
Description=nio
After=network.target

[Service]
WorkingDirectory=/full/path/to/your/project
ExecStart=/usr/local/bin/niod
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=always

[Install]
WantedBy=multi-user.target
```

After you have created your service file and placed it in `/etc/systemd/system`, you can activate the new service with the following commands:

```
sudo systemctl daemon-reload 
sudo systemctl enable nio.service
```

Now, you can start your nio instance like so:
```
sudo service nio start
```

Stopping is similar:
```
sudo service nio stop
```

Check the status and recent logs of your nio instance with
```
sudo service nio status
```
