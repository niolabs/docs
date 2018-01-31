# Troubleshooting
These are some common errors and potential solutions. If your problem is not listed in this table, either contact niolabs support using the blue conversation bubble in the Portal or the System Designer or post your questions on the nio [forum](https://forum.n.io/).

| Error                                                   | Possible Cause    | Solution        |
|---------------------------------------------------------|-------------------|-----------------|
| Error Loading Instance | The instance is not running, or is not reachable at the specified address (host) and port. | **For nio-managed cloud instances:**<br>- Contact niolabs support.<br>**For self-managed instances:**<br> - Click **edit**, verify **hostname** and **port** are correct.<br>- Verify instance is running.<br> - If instance will not stay running, locate project log files and contact niolabs support. |
| Cannot connect to an insecure instance when using HTTPS. Please use this version of the designer instead. | The local instance is not secure, it lacks SSL certificates. | - Visit http://designer.n.io to continue with an insecure connection<br>- load an SSL certificate by updating paths in `nio.conf` (walk through coming soon). |
| Type error | When the System Designer attempts to fetch all of the block specifications from the product API, an error is returned. | Contact niolabs support. |
| No “nio-organization” header present in request. | The System Designer made a request to a product API end point that requires the `nio-organization` header and that header is missing in the request. | Contact niolabs support. |
