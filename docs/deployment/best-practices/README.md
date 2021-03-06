# nio Deployment Best Practices

The nio software is designed to be flexible in its installation and requirements. This means it fits into many different shapes and sizes of deployments. However, it also means that mistakes can be made when running nio in a production setting. In this document we've collected some tips and tricks based on our own and our customers' experiences that can help you make sure your nio instance runs reliably and securely.

## Use Virtual Environments

We recommend running your Python nio instance inside of a [Python virtual environment](https://docs.python-guide.org/dev/virtualenvs/) rather than using the system Python installation. Doing this helps manage and prevent conflicts with Python dependencies and also makes it easier to run nio without using the root user.

## Don't Run as Root

As tempting as it can be to throw a `sudo` in front of an installation or a command when you see permissions errors, niolabs highly recommends not running nio as root. Because nio instances run block code and expressions that can be edited by users, root access could allow a nio instance to make potentially catastrophic changes to your host device. Root permissions are not required for a nio instance in nearly every circumstance.

Furthermore, it is often useful to run nio as a new, dedicated user so that filesystem access can be configured for that user specifically. When using a separate user, this user will only need filesystem access to the nio project directory in a standard install.

## Use SSL/TLS Certificates

For security reasons, it is very important to secure your nio instances with an SSL/TLS certificate. The nio CLI makes it convenient to [generate your own certificate](/cli/config.html) if you do not have one from a trusted certificate authority. Using an SSL/TLS certificate means you can access your nio instance's API over HTTPS instead of HTTP. This will also allow you to use the HTTPS version of the management applications like the nio System Designer.

## Keep your secrets separate

Often times your nio settings files will contain credentials or other secrets that you may not want to commit to version control. We recommend either using system environment variables or a separate secrets settings file, depending on how you are deploying, to keep them separate so that they can be ignored from version control.

Your nio settings file (`nio.conf`) can populate values from OS environment variables by wrapping them in double square brackets. Many deployment strategies like docker or systemd allow you to specify environment variables when running. These are often a useful place for secrets. For example, to load your Pubkeeper access token from an environment variable called `PK_ACCESS_TOKEN` use the following settings in your `nio.conf` file:
```
[pubkeeper_client]
token= [[ PK_ACCESS_TOKEN ]]
```

You can also keep a separate settings file that is used for keeping secrets that won't be committed to version control. When you start nio with the `niod` command it assumes your settings file is located at `nio.conf`. You can specify a different settings file with the `-s` flag but you can also specify multiple settings files and they will be "merged" together. Settings from the later files will take precedence over the earlier files. For example, to keep a separate `secrets.conf` that contains your configuration secrets and credentials you would start nio with the following command:
```
niod -s nio.conf -s secrets.conf
```

## Secure Host Checklist

We can secure our nio instance until the cows come home but if the host that nio is running on is not secure then our efforts are all in vain. We have assembled the following checklist of items to pay attention to when deploying nio on to your devices. This list has been created by referencing many [industry standard security documents](https://niolabs.com/security). It is not intended to be exhaustive, but it's a good start.

 * &#9745; Use ntp for clock synchronization
 * &#9745; Make sure WiFi connections use a strong encryption mechanism
