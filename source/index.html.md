---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the HandCash Handle API! You can use our API to send Bitcoin Cash using $handles, and improving the UX in your applications.

You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

Different endpoints are available depending of your use:

* **Mainnet**: hand-cash-server.herokuapp.com/api/
* **Testnet**: hand-cash-server-dev.herokuapp.com/api/


# All about the $handles

Handles are user-friendly alias to refer to a receiving address. Or more specifically, to a wallet.

* Each handle is linked to a wallet hash. Only the owner of the wallet can perform write operations.
* Each time you get the receiving address of a handle, the wallet generates a new address.

![Handles components interaction](Handles_components_interaction.png)



This endpoint retrieves the current receiving address associated with the given $handle.

### HTTP Request

`GET /receivingAddress/<handle>`

### URL Parameters

Parameter | Description
--------- | -----------
handle | The handle we want to get the receiving address.


# Get address by $handle


> To get the current address, use this code:


```python
# Python 3
import urllib.request
import json

RECEIVING_ADDRESS_ENDPOINT = 'http://hand-cash-server-dev.herokuapp.com/api/receivingAddress'
HANDLE = 'apagut'

req = urllib.request.Request(f'{RECEIVING_ADDRESS_ENDPOINT}/{HANDLE}')
with urllib.request.urlopen(req) as response:
   data = json.loads(response.read().decode())
   print(f'Response: {data}')
   print(f'To send money to ${HANDLE} use the base58 address: {data["receivingAddress"]}')

```

```shell
curl https://hand-cash-server-dev.herokuapp.com/api/receivingAddress/apagut
```

```javascript
var handle = 'apagut';
var req = new XMLHttpRequest();
req.onreadystatechange = function() {
    if (req.readyState === 4) {
        var response = req.responseText;
        var json = JSON.parse(response);
        alert('To send money to ' + handle + ' use the base58 address: ' + json['receivingAddress']);
    }
};

req.open('GET', 'http://hand-cash-server.herokuapp.com/api/receivingAddress/' + handle);
req.send(null);
```


> The above command returns JSON responses like this:

```json

{"receivingAddress": "mq6nzgYzJw8zChBXw4Tvpc657KUoEjd6Ti", "publicKey": "023b0d20b09390881b182a74d5b2e2287a316c514ef22d2700d3d61178e156df8d"}

```

This endpoint retrieves the current receiving address associated with the given $handle.

### HTTP Request

`GET /receivingAddress/<handle>`

### URL Parameters

Parameter | Description
--------- | -----------
handle | The handle we want to get the receiving address.

### HTTP Response

This endpoint returns a JSON with the following fields.


Parameter | Description
--------- | -----------
receivingAddress | The base58 address associated with the current handle.
publicKey | The public key associated with the address.


Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

