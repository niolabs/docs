# API Conventions

You can interact with most nio binaries through a REST API. The API supports the standard HTTP request types of `GET`, `POST`, `PUT`, and `DELETE`. Data responses are returned in JSON format.

The REST API is available in nio binaries that include the nio REST Component. Read more about nio core components [here](/binaries/components.md).

---

## Authentication and Authorization

Authentication is the action to verify the identity of a user or process.

Authorization is the process of giving someone permission to perform an action.

You will need to include an authorization header with your nio API requests. For examples, see [Basic Auth](#basic-authentication-basic-auth) and [JWT](#json-web-tokens-jwt). For examples of adding headers to curl requests, see [Headers](#headers).

User names and passwords are specified in the `users.json` file in the `etc` directory.

Authorization for your project's users is specified in the `permissions.json` file in the `etc` directory of your project.

If you want to secure your project and its API, change these user names and passwords and specify the permissions.

You can change the location of your users and permissions files in the `[security]` section of `nio.conf`, a YAML file.

```
[security]

# json configuration that defines users and their passwords - can point to a conf file
#
#users=etc/users.json

# json configuration that maps users to permissions - can point to a conf file
#
#permissions=etc/permissions.json
```

The default configuration is shown. You can uncomment the default configuration and it will not change. To find your users and permissions in files other than `etc/users.json` and `etc/permissions.json`, uncomment the configuration and edit it.

You can use different types of authentication, such as basic authentication and JSON Web Tokens, with nio.

### Basic Authentication (Basic Auth)

When using basic authentication, the REST API requires a username and password.

To use basic auth, include a base-64 encoded version of your `username:password` in the Authorization header of your request. The default `username:password` from the project template is `Admin:Admin`. An example of basic authorization in your request header follows:

`{ "authorization": "Basic QWRtaW46QWRtaW4=" }`

For examples of adding headers to a curl request, see  [Headers](#headers).

### JSON Web Tokens (JWT)

When using JSON Web Tokens (JWT), first obtain an access token, and then include it in the header.

`{ "authorization": "Bearer <your token>" }`

For examples of adding headers to a curl request, see [Headers](#headers).

---

## Testing with curl

To test nio API requests and responses, you can use a tool such as [Postman](https://www.getpostman.com/) or a curl command from your terminal. curl commands start with `curl`, and then include the request type, a URL, and possibly a request header and a request body. For the nio API, an authorization [header](#headers) is required.

### Request Type
Your request type will be one of `GET`, `POST`, `PUT`, or `DELETE`.

With the curl command, you can specify the request type with following options:

      -XGET
      -XPOST
      -XPUT
      -XDELETE

### URL
Your request type will be followed by a URL.

#### Base URL
The base of the URL for your API request is the address where your nio project is running. Obtain the base URL from your nio logs.

For a local project

    http://localhost:8181/

For a remote project

    https:// <IP address:port> /

#### Endpoint

The endpoint is added to the base URL

    http://localhost:8181/blocks_types

You can also add query parameters to the URL, but for the most part, the nio API does not use query parameters.

### Headers

In your request, you need to include a header with your [Basic Auth](#basic-authentication-basic-auth) or [JWT](#json-web-tokens-jwt) authentication. You can add auth to your curl requests with the `-H` header flag or the `--user` flag followed by a string. The following formats will work:

      -H 'authorization: Basic <base 64 encoded username:password>'

      -H 'authorization: Bearer <your token here>'

      --user 'Admin:Admin'

To send data with your request, you need to include the data's Content-Type in your header.

      -H 'Content-Type: application/json'

### Body

In the request body, if you need to include data, add body data to a curl request with the `-d` or `--data` flag.

    -d '{"type": "LoggerBlock", "name": "Log"}'

    --data '{"type": "LoggerBlock", "name": "Log"}'


### Putting It All Together

A typical curl request to the nio API incorporating all these parts follows:

    curl -XPOST 'http://localhost:8181/blocks' --user 'Admin:Admin' --data '{"type": "LoggerBlock", "name": "Log"}' -H 'Content-Type: application/json'
