---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

toc_footers:
  - <a href='https://t.me/joinchat/GMX7LUwWo5pg_42TLbHByw'>Telegram</a>
  - <a href='https://twitter.com/handcashapp'>Twitter</a>
  - <a href='mailto:info@handcash.io'>Email</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the HandCash Handle API! You can use our API to send Bitcoin Cash using $handles, and improving the UX in your applications.

You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

Different endpoints are available depending of your environment:

* **Testnet**: `test-api.handcash.io/api/`
* **Mainnet**: `available on June 15th`


# All about the $handles

## How it works

Handles are user-friendly alias to refer to a receiving address. Or more specifically, to a wallet.

* Each handle is linked to a wallet hash. Only the owner of the wallet can perform write operations (update the receiving address).
* Each time you get the receiving address of a handle the referenced wallet generates a new address. In case the wallet is not available, you will get the last known receiving address.

<p align="center">
  <img src="/images/Handles_components_interaction.png"/>
</p>

## Use cases

This Handles API are help the developers to increase the UX of the sending or withdraw process inside the Bitcoin Cash ecosystem.

Following a few uses cases where the API suits great:

### TipprBot

This bot can include commands like:

<p align="center">
"Send 5$ to my $myFriendHandle" OR "Withdraw to $myHandle"
</p>

This integration can be done by following the next steps:

1. Retrieve the `$handle` expression from the message.
2. Use the Handles API to get a receiving address associated to this `$myHandle`.
3. Create a regular tx using the previous address.

### Yours

Once in a while, Yours users decide to withdraw their founds or just a portion. They could integrate a new sophisticated withdraw method like:

1. Include a new withdraw method like: `Withdraw using my $handle`.
2. User enters the $handle.
3. Yours service uses the Handles API to get a receiving address associated to the `$handle`. 
3. Yours create a regular tx using the previous address to withdraw the funds.

### More use cases

Additionally, the API includes the `public key` of the current receiving address of the $handle for encryption purposes.

Do you have any other use case in mind? **Please contact us, we are glad to hear new ideas!**


# Get address by $handle


> To get the current address, use this code:


```python
# Python 3
import urllib.request
import json

RECEIVING_ADDRESS_ENDPOINT = 'http://test-api.handcash.io/api/receivingAddress/'
HANDLE = 'rjseibane'

req = urllib.request.Request(f'{RECEIVING_ADDRESS_ENDPOINT}/{HANDLE}')
with urllib.request.urlopen(req) as response:
   data = json.loads(response.read().decode())
   print(f'Response: {data}')
   print(f'To send money to ${HANDLE} use the base58 address: {data["receivingAddress"]}')

```

```shell
curl http://test-api.handcash.io/api/receivingAddress/rjseibane
```

```javascript
var handle = 'rjseibane';
var req = new XMLHttpRequest();
req.onreadystatechange = function() {
    if (req.readyState === 4) {
        var response = req.responseText;
        var json = JSON.parse(response);
        alert('To send money to ' + handle + ' use the base58 address: ' + json['receivingAddress']);
    }
};

req.open('GET', 'http://test-api.handcash.io/api/receivingAddress/' + handle);
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
handle | The handle you want to get the receiving address.

### HTTP Response

This endpoint returns a JSON with the following fields.


Parameter | Description
--------- | -----------
receivingAddress | The base58 address associated with the given handle.
publicKey | The public key associated with the address.


