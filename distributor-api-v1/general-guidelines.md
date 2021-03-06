# General Guidelines

## Usage  <a id="Usage"></a>

Distributor API is a public API with no authorization that is designed to be consumed directly by frontend clients. It is unsuitable for continuous polling by a single server due to the built in anti-scraping protection and such requests can fail. For server to server communication, please refer to [Connector API](https://mews-systems.gitbook.io/connector-api/)

## Requests  <a id="requests"></a>

The API accepts only`HTTP POST`requests with`Content-Type`set to`application/json`and JSON content depending on the operation to be performed. All operations follow this address pattern:

```text
[PlatformAddress]/api/distributor/v1/[Resource]/[Operation]
```

* **PlatformAddress**
  * Base address of the MEWS platform, depends on environment \(testing, staging, production\).
* **Resource**
  * Logical group of operations, in most cases identifies target of the operations.
* **Operation**
  * Name of the operation to be performed.

## Responses  <a id="responses"></a>

The API responds with`Content-Type`set to`application/json`and JSON content. In case of success, the HTTP status code is 200 and the content contains result according to the call. In case of error, there are multiple HTTP status codes for different types of errors:

* **400 Bad Request**
  * Error caused by the client app, e.g. in case of malformed request or invalid identifier of a resource. In most cases, such an error signifies a bug in the client app \(consumer of the API\).
* **401 Unauthorized**
  * Error caused by usage of invalid access token.
* **403 Forbidden**
  * Server error that should be reported to the end user of the client app. Happens for example when the server-side validation fails or when a business-logic check is violated.
* **500 Internal Server Error**
  * Unexpectced error of the server. In most cases, such an error signifies a bug on our side. We are logging it and immediately notified when such error happens. If anything like this happens, feel free to directly contact us or raise an issue here on Github.

In case of any error, the returned JSON object describes the error and has the following properties:

|  | Property | Type | Description |
| :--- | :--- | :--- | :--- |
| `Message` | string | required | Description of the error. |
| `Details` | string | optional | Additional details about the error \(request, headers, server stack trace, inner exceptions etc.\). Only available on development environment. |

Some errors may also contain additional information relevant to the error on top of this two properties. But that depends on the operation and is specificly described in the operation documentation.

