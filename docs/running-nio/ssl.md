# Securing your nio instance with SSL

When you use the System Designer to configure and interact with your nio instance, you are executing HTTP requests to the instance's HTTP API from your local browser. This is different than many software products, which have you interact with a cloud server rather than your edge device directly. This means the niolabs cloud environments do not have to have any direct access to your nio instances. It also comes with some additional complexity around securing the instance access using SSL/TLS certificates.

Modern browsers contain many restrictions around interacting with HTTP and HTTPS APIs. Specifically, a browser will not let you make a non-secure HTTP request in the background of a browser tab that has been loaded securely with HTTPS. This means, if you are on the secure HTTPS version of the System Designer, you will not be able to interact with a non-secure HTTP nio instance. If you try to do this you will likely see an http error modal pop up in the System Designer. You have two options to remedy this:

1. Secure your nio instance so it is accessible with HTTPS (recommended)
2. Use the non-secure HTTP version of the System Designer ([http://app.n.io](http://app.n.io))

## Generating Certificates for your nio Instance

In order to secure your nio instance with an SSL certificate, you will need a few things:
1. An x509 certificate for your instance's hostname/IP
2. The private key for the aforementioned certificate
3. Optional - The certificate chain for the certificate authority

One option is to get your certificate from a global trusted authority such as DigiCert or LetsEncrypt. However, this can be complex, costly, and requires that your instance is publicly accessible. For convenience, the nio CLI allows you to create certificates that are trusted on your local machine.

From your project directory, run this command to configure SSL for your local instance:
```
nio config --ssl
```

It will prompt you for a CA location, if you don't have a CA that you want to use, don't enter anything and one will be created for you at that location. Read more about the local CA below. Once the CA is created and trusted, you will be prompted for a hostname. This is the hostname that you will enter in the System Designer for how you will access your instance. If your instance will only run on your local machine, enter `localhost`. The certificate will be created for that hostname.

The CA will be created in `~/.nio/` and your certificate and private key will be created in the `etc/ssl` folder of your project.

## The niolabs Local Certificate Authority

In order to expedite secure local development, the nio CLI can create a local certificate authority that can be used to sign your instances' SSL certificates. This authority is only created once and can be trusted in your host's trusted certificate store. Then, all subsequent certificates that are signed by this CA will be trusted as well.

This local CA is created by default in your `~/.nio/` folder on your machine. The CA consists of a certificate and a private key that will be used to sign other certificates.

### Trusting the Local CA on a Mac

The nio CLI will prompt you to trust the certificate authority when it is created. If you would like to trust the CA manually you can run the following command in your terminal, replacing the correct CA cert location if necessary. Note that this command will pop up a prompt for your password.

```
security add-trusted-cert -r trustRoot -k $HOME/Library/Keychains/login.keychain $HOME/.nio/ca.crt
```

### Trusting the Local CA on Firefox

Firefox [does not use the system's trusted cert store](https://www.mozilla.org/en-US/about/governance/policies/security-group/certs/policy/) and instead uses its own. That means that trusting a local CA in your host's store will not be sufficient if you wish to use Firefox as a browser. To trust the local CA in Firefox go to `Preferences` > `Privacy & Security` > `View Certificates...`. From the `Authorities` tab click `Import...` and select the local CA.

> The local CA is in a hidden folder by default and will not be visible in the Import modal. To make hidden files viewable in this modal on a Mac press `Command+Shift+.` (command + shift + period).

## Troubleshooting

Browsers provide some useful tools to view and troubleshoot SSL certificates. If you are unable to connect to your nio instance from the System Designer and believe that SSL is the issue, try opening a direct connection to your instance in a new tab. For example, try navigating to [https://localhost:8181/nio](https://localhost:8181/nio) if your instance is running on `localhost`. It's ok if we see a JSON blob indicating an Unauthorized error, what we are looking for here is whether the certificate is trusted or not. If you see the JSON 401 error and you see a green lock icon for the certificate in the URL bar, it means the certificate is trusted and working. If you instead see your browser's security warning page, something is wrong with your certificate. Make sure your local CA is trusted and that it is shown as the signing CA when you view the certificate in your browser (typically do-able by clicking the lock icon in the URL bar). Feel free to reach out to niolabs support if you can't figure out why your certificate is not working.
