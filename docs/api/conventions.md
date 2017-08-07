# API Conventions

You can interact with most {{ book.product }} binaries through a REST API. The API supports the standard HTTP request types of `GET`, `POST`, `PUT`, and `DELETE`. Data responses are returned in JSON format.

The REST API is available in {{ book.product }} binaries that include the {{ book.product }} REST Component. Read more about {{ book.product }} core components in [components](../components/README.md).

## Authorization

Authorization is about what users are allowed to do.

Setting up permissions in your project.

Project template sets you up with default users and permissions.

You should change these.

Authorization for your project's users are specified in the `permissions.json` file in the `etc` directory of your project.

## Authentication

Authentication is about who somebody is.

Authentication for your project's users are specified in the `users.json` file in the `etc` directory of your project.

{{ book.product }} can use different types of authentication, for example basic auth and JWT.

### Basic Auth

When using basic authentication, the REST API is protected by usernames and passwords. To use basic auth, include a base-64 encoded username and password in the Authorization header of your request. For example:

`{ "authorization": "Basic <your encrypted password>" }`

### JWT

When using OAuth 2.0, you need to first get an access token. Once you have one, include it in the header. For example:

`{ "authorization": "Bearer <your token>" }`

## Testing with cURL

To test API requests and responses, you can use a tool like Postman or, more basic, a cURL command from your terminal. cURL commands start with `curl` and then include the request type, a URL, and possibly a request header and a request body.

### Request Type
Your request type will be one of `GET`, `POST`, `PUT`, or `DELETE`.

In your cURL command you specify these with

      -XGET
      -XPOST
      -XPUT
      -XDELETE

### URL
Your request type will be followed by a URL.

#### base URL
The base of the URL for your API request will be the address where your {{ book.product }} project is running. This will show up in your terminal in the nio logs.

For a local project

    http://localhost:8181/

For a remote project

    https:// <IP address:port> /

#### Endpoint

The endpoint is added to the base URL

    http://localhost:8181/blocks_types

You can also add query parameters to the URL, but the {{ book.product }} API does not use query parameters.

### Headers/Auth

You will need to include your basic auth or OAuth2 authentication as described above. You can add auth to your cURL requests with the `-H` header flag or the `--user` flag followed by a string. Any one of these formats should work

      -H 'authorization: Basic <you encrypted password>'

      -H 'authorization: Bearer <your token here>'

      --user 'Admin:Admin'

Other things you might need in your header include Content-Type.

      -H 'Content-Type: application/json'

### Body

In your request body, sometimes you will need to include data. You can add body data to a cURL request with the `-d` or `--data` flag

    -d '{"type": "LoggerBlock", "name": "Log"}'

    --data '{"type": "LoggerBlock", "name": "Log"}'


### Putting It All Together

A typical cURL request the the {{ book.product }} API incorporating all these parts might look like

    curl -XPOST 'http://localhost:8181/blocks' --user 'Admin:Admin' --data '{"type": "LoggerBlock", "name": "Log"}' -H 'Content-Type: application/json'
