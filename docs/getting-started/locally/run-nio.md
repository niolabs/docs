# Run nio

You will want to use the System Designer to see your local instance running.

Open the **System Designer** in a browser.

  https://designer.n.io/

If you don't already have a system you want to use for this project in the designer, click the **`+`** button to create one.

When you complete the **create new system** window and click **accept**, a new Pubkeeper server will be created in the cloud to handle the communications in your system.

To connect your local nio project to the Pubkeeper server, you will need to configure your project.

## Configure Your Local Project to use the Cloud Pubkeeper Server

With your system selected, click **edit** in the contextual toolbar to open the system's configuration.

{% include "/includes/pubkeeper-config.md" %}

## Run nio

With your project installed and Pubkeeper communication configured, you are ready to run your nio binary. In your terminal, from the root of your project directory, enter the following command:
```
niod
```
> If that command is not available, make sure your Python binary installation directory is on your PATH.

> If you need help setting your PATH in Windows, click [here](https://msdn.microsoft.com/en-us/library/aa922003.aspx).

> If you need help setting your PATH in MacOS, click [here](http://osxdaily.com/2014/08/14/add-new-path-to-path-command-line/).

Log messages should display, similar to the following output. There should be no errors.

  ```
  NIO [INFO] [main.WebServer] Server configured on 0.0.0.0:8181
  NIO [INFO] [main.WebServer] Server configured on 0.0.0.0:8181
  NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:
    to: created
  NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:
    created to: configuring
  NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:
    configuring to: configured
  NIO [INFO] [main.WebServer] Starting server on 0.0.0.0:8181
  NIO [INFO] [main.WebServer] Server 0.0.0.0:8181 started on 0.0.0.0:8181
  NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:
    configured to: starting
  NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:
    starting to: started
  ```

If you see those logs, nio is up and running. Congratulations!
