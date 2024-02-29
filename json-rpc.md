# JSON-RPC

JSON-RPC is a widely adopted standard that describes structured messages for communication between a client and server. The current version is 2.0 (published in 2010).

It combines two technologies:

- [RPC (Remote Procedure Call)][rpc]: a way for a program to call a function on a different machine and get a result (or error) back.
- [JSON (JavaScript Object Notation)][json]: a standard data format that is easy for humans to read and write and easy for machines to parse and generate.

Note that "client" and "server" are used here to describe the two ends of the communication. In practice, the client and server could be any two programs that communicate with each other. Client and server roles could be reversed at different times in their lifecycle.

## Use cases

JSON-RPC is used in many different contexts, including:

- Web APIs
- Microservices
- IoT (Internet of Things)
- Blockchain
- [Language servers](https://microsoft.github.io/language-server-protocol/)
- ...

## Message types

**Request message**

Request messages ask for an action (`method`) to be performed. The server must reply to a request with a response message.

- **`jsonrpc`** (string): the version of the JSON-RPC protocol.
- **`method`** (string): the name of the action to be performed
- **`params`** (object | array): (optional) the parameters for the method
- **`id`** (number | string): a unique identifier for the request

A result and an error are mutually exclusive. If a response includes a result, it must not include an error, and vice versa.

A result can be any JSON value, including `null`. An error is an object with a `code` and a `message` property. An error can also include a `data` property with additional information about the error.

**Response message**

Response messages are the reply to a request. They include the id of the request they are replying to and a result or an error.

- **`jsonrpc`** (string): the version of the JSON-RPC protocol.
- **`result`** (any): the result of the method
- **`error`** (object): an error message
- **`id`** (number | string): the id of the request being replied to

**Notification message**

Notification messages inform the other end about something that happened, and do not expect a reply.

- **`jsonrpc`** (string): the version of the JSON-RPC protocol.
- **`method`**: the name of the action that happened
- **`params`**: (optional) the parameters for the method

## Examples

**Request & Response**

Here, a client asks the server to add two numbers together. The server replies with the result.

Request:

```json
{
  "jsonrpc": "2.0",
  "method": "add",
  "params": [12, 5],
  "id": 1
}
```

Response:

```json
{
  "jsonrpc": "2.0",
  "result": 17,
  "id": 1
}
```

Here, a client asks the server to add a number to a string. The server replies with an error.

Request:

```json
{
  "jsonrpc": "2.0",
  "method": "add",
  "params": [3, "cat"],
  "id": 2
}
```

Response:

```json
{
  "jsonrpc": "2.0",
  "error": {
    "code": -32602,
    "message": "Invalid params",
    "data": "Cannot add a number to a string"
  },
  "id": 2
}
```

**Notification**

Here, the server informs the client that a user has logged in. The server doesn't reply to this message but may use this notification to (e.g.) update the `lastLoggedIn` field in the user's record or trigger a workflow.

```json
{
  "jsonrpc": "2.0",
  "method": "userLoggedIn",
  "params": {
    "userId": 123
  }
}
```

## Batch requests

JSON-RPC also supports batch requests, where a client sends multiple requests in a single message, and the server replies with multiple responses.

Request:

```json
[
  {
    "jsonrpc": "2.0",
    "method": "add",
    "params": [12, 5],
    "id": 1
  },
  {
    "jsonrpc": "2.0",
    "method": "add",
    "params": [3, "cat"],
    "id": 2
  }
]
```

Response:

```json
[
  {
    "jsonrpc": "2.0",
    "result": 17,
    "id": 1
  },
  {
    "jsonrpc": "2.0",
    "error": {
      "code": -32602,
      "message": "Invalid params",
      "data": "Cannot add a number to a string"
    },
    "id": 2
  }
]
```

## Further reading

- [JSON-RPC 2.0 Specification](https://www.jsonrpc.org/specification)
- [Wikipedia: JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC)
- [RPC (Remote Procedure Call)][rpc]
- [JSON (JavaScript Object Notation)][json]

# JSON-RPC

JSON-RPC is a widely adopted standard that describes structured messages for communication between a client and server. The current version is 2.0.

It combines two technologies:

- [RPC (Remote Procedure Call)][rpc]: a way for a program to call a function on a different machine and get a result (or error) back.
- [JSON (JavaScript Object Notation)][json]: a standard data format that is easy for humans to read and write and easy for machines to parse and generate.

## Message types

**Request message**

Request messages ask for an action (`method`) to be performed. The server must reply to a request with a response message.

- **`jsonrpc`** (string): the version of the JSON-RPC protocol.
- **`method`** (string): the name of the action to be performed
- **`params`** (object | array): (optional) the parameters for the method
- **`id`** (number | string): a unique identifier for the request

**Response message**

Response messages are the reply to a request. They include the id of the request they are replying to and a result or an error.

- **`jsonrpc`** (string): the version of the JSON-RPC protocol.
- **`result`** (any): the result of the method
- **`error`** (object): an error message
- **`id`** (number | string): the id of the request being replied to

A result and an error are mutually exclusive. If a response includes a result, it must not include an error, and vice versa.

A result can be any JSON value, including `null`. An error is an object with a `code` and a `message` property. An error can also include a `data` property with additional information about the error.

**Notification message**

Notification messages inform the other end about something that happened, and do not expect a reply.

- **`jsonrpc`** (string): the version of the JSON-RPC protocol.
- **`method`**: the name of the action that happened
- **`params`**: (optional) the parameters for the method

## Further reading

- [JSON-RPC 2.0 Specification](https://www.jsonrpc.org/specification)
- [Wikipedia: JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC)
- [RPC (Remote Procedure Call)][rpc]
- [JSON (JavaScript Object Notation)][json]

# JSON-RPC

JSON-RPC is a standard for communication between a client and server.

- RPC stands for Remote Procedure Call, which is a way for a program to call a function on a different machine.
- JSON is a data format that is easy for humans to read and write and easy for machines to parse and generate.

Official spec: [https://www.jsonrpc.org/specification][spec]

## Message types

- **Request** messages ask for an action (named `method`) to be performed. Besides the method, the request message can include parameters for the method. It always includes an id.
- **Response** messages are the reply to a request. They include the id of the request they are replying to and a result or an error.
- **Notification** messages inform the other end about something that happened and do not expect a reply.

# JSON-RPC

JSON-RPC is a standard for communication between a client and server.

- **Request** messages ask for an action (named `method`) to be performed.
- **Response** messages are the reply to a request.
- **Notification** messages inform the other end about something that happened and do not expect a reply.

Official spec: [https://www.jsonrpc.org/specification][spec]

# JSON-RPC

JSON-RPC is a standard for communication between a client and server.

Official spec: [https://www.jsonrpc.org/specification][spec]

[spec]: https://www.jsonrpc.org/specification
[rpc]: https://en.wikipedia.org/wiki/Remote_procedure_call
[json]: https://en.wikipedia.org/wiki/JSON
