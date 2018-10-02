# In production

Eventually you will want to run your nio instances for longer durations and have them be more resilient to network outages and system restarts. There are many ways to use existing tools to make this easier, here are a few recommended options.

---
## Run with <span class="allow-caps">Docker</span>

Running the nio Platform as a Docker container allows you to manage its lifecycle through standard Docker deployment practices and use orchestration managers like Kubernetes. Check out our [guide to running nio with Docker](/deployment/docker.md) for more information on how to do this.

---
## Run nio in the background

When you run `niod` without any other shell options the nio instance will die if your terminal is closed or your SSH session disconnects. To prevent this, you can run nio in the background on MacOS and Linux using `nohup`. Not available on Windows.

```
nohup niod -r path/to/my_project 2>&1 > /dev/null &
```

---
## Run nio with systemd

**systemd** is an **init** system that comes included with many Linux distributions. Running nio as a systemd service allows you to manage the instance using standard `sysctl` commands.

To create a systemd service for running nio, create a new systemd service file in `/etc/systemd/system/nio.service`. Here is a template service file you can start with. You can find more systemd service options on the [official systemd documentation](https://www.freedesktop.org/software/systemd/man/systemd.service.html). Update the `WorkingDirectory` to the location of your nio project and make sure the executable path for `niod` is correct. If you are using a [virtual environment](https://docs.n.io/deployment/best-practices/) (highly recommended) use the path to `niod` with that env active.

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

## Run nio with Windows Task Scheduler

The Task Scheduler provides a simple interface to start a process at the selected trigger, in this case start up. Note that the Task Scheduler does not provide any support for restarting a stopped process.
1. Start the Task Scheduler
  - Start
  - Type to search for `task scheduler`
  - press [Enter]
1. Click `Create Task` from the right pane
1. [General] Tab
  - Enter a name for the task and select a user. If nio is intended to run without a specific user logged on, consult your IT department to set up a service account for this machine, and select that account.
1. [Triggers] Tab
  - Create a new trigger
  - Select the desired value from the drop-down, such as `At startup`
1. [Actions] Tab
  - Create a new action
  - Select `Start a Program` from the drop-down
  - Enter `niod` for *Program/Script*. If you are using a [virtual environment](https://docs.n.io/deployment/best-practices/) (highly recommended) put the absolute path to `niod` inside that environment, for example: `C:\Users\<user>\nio\env\bin\niod`
  - Enter the absolute path to the project folder for *Start In*, for example: `C:\Users\<user>\nio\projects\<my_project>`
1. [Settings] Tab
    - Verify these options, by default Windows will stop tasks that run longer than 3 days.
