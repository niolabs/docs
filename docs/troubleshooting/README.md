# Troubleshooting
These are some common errors and potential solutions. If your problem is not listed in this table, either contact niolabs support using the blue conversation bubble in the Portal or the System Designer or post your questions on the nio [forum](https://forum.n.io/).

| Error                                                   | Possible Cause    | Solution        |
|---------------------------------------------------------|-------------------|-----------------|
| Error Loading Instance | The instance is not running, or is not reachable at the specified address (host) and port. | **For nio-managed cloud instances:**<li>Contact niolabs support.</li><br>**For self-managed instances:**<li>Click <strong>edit</strong>, verify <strong>hostname</strong> and <strong>port</strong> are correct.</li><li>Verify instance is running.</li><li>If instance will not stay running, locate project log files and contact niolabs support.</li> |
| Cannot connect to an insecure instance when using HTTPS. Please use <a href="http://designer.n.io">this</a> version of the designer instead. | The local instance is not secure, it lacks SSL certificates. | <li>Visit <a href="http://designer.n.io">http://designer.n.io</a> to continue with an insecure connection</li><li>Load an SSL certificate by updating paths in <code>nio.conf</code> (walk through coming soon).</li> |
| Type error | When the System Designer attempts to fetch all of the block specifications from the product API, an error is returned. | Contact niolabs support. |
| No “nio-organization” header present in request. | The System Designer made a request to a product API end point that requires the `nio-organization` header and that header is missing in the request. | Contact niolabs support. |
