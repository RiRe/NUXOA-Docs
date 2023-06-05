---
title: Manager API – NUXOA

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php

toc_footers:
  - <a href='https://nuxoa.de/impressum/'>Imprint</a>

search: false
---

# Introduction

Welcome to the API documentation of NUXOA. You can use this API as client to act with your account, domains and products. Therefore, you need your customer ID and your API key. This documentation covers all available API actions.

We provide example codes in Shell and PHP. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication & Request

> To make a request, use this code:

```php
<?php
$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domains/list");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domains/list"
```

> Make sure to replace `CUSTOMER_ID` with your customer ID and `API_KEY` with your API key.

NUXOA uses an API key combined with your customer ID to allow access to the API. You can find your API key in your client area or request it at support.

Parameters can be sent via GET or POST.

NUXOA expects for the API key to be included in all API requests to the server in the request.

A request URL is formatted as follows:

`/api/CUSTOMER_ID/API_KEY/METHOD/ACTION`

<aside class="notice">
Hereby, <code>CUSTOMER_ID</code> is your customer ID, <code>API_KEY</code> is your API key, <code>METHOD</code> is the API method you want to call and <code>action</code> is the task you want to execute.
</aside>

# Cloud server

## Get server pricing

```php
<?php
$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/cloud/pricing");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/cloud/pricing"
```

> The above command returns JSON structured like this:

```json
{
  "code": "100",
  "message": "Pricing fetched.",
  "data": {
    "currency": "EUR",
    "base": {
      "net": 0.8,
      "gross": 0.952
    },
    "cores": {
      "net": 0.8,
      "gross": 0.952
    },
    "ram": {
      "net": 0.55,
      "gross": 0.6545
    },
    "storage": {
      "net": 0.04,
      "gross": 0.0476
    }
  }
}
```

Using this endpoint, you can get the current prices for our cloud servers.

### API endpoint

`/cloud/pricing`

## Order a new server

<aside class="notice">
Server orders are currently only possible via web. We will enable server orders by API soon.
</aside>

## Get server details

```php
<?php
$req = [
  "id" => 123,
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/cloud/info");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/cloud/info?id=123"
```

> The above command returns JSON structured like this:

```json
{
  "code": "100",
  "message": "Server query successful.",
  "data": {
    "status": true,
    "description": "",
    "order_date": "2022-06-01 00:00:00",
    "price": 10,
    "currency": "EUR",
    "period": "monthly",
    "next_invoice": "2023-07-01",
    "cancellation_date": "0000-00-00",
    "cancellation_dates": [
      "2023-07-01",
      "2023-08-01",
      "2023-09-01",
      "2023-10-01",
      "2023-11-01"
    ],
    "online": true,
    "ipv4": "1.2.3.4",
    "ipv6": null,
    "os": "Debian 11",
    "username": "root",
    "password": "***",
    "ssh_key": "",
    "available_os": [
      "Debian 11",
      "Debian 10",
      "Ubuntu 21.04",
      "Ubuntu 20.04",
      "Ubuntu 22.04",
      "Windows Server 2022"
    ]
  }
}
```

Using this endpoint, you can get details for one of your servers.

### API endpoint

`/cloud/info`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown

## Start server

```php
<?php
$req = [
  "id" => 123,
];

$ch = curl_init("https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/start");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/start?id=123"
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

Using this endpoint, you can start a cloud server.

### API endpoint

`/cloud/start`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract

### Return codes

This are the additional return codes for this action. The global return codes applies. If there is no error, no return code and no message is returned.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown

The `message` element can contain more details.

## Reboot server

```php
<?php
$req = [
  "id" => 123,
];

$ch = curl_init("https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/reboot");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/reboot?id=123"
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

Using this endpoint, you can reboot a cloud server.

### API endpoint

`/cloud/reboot`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract

### Return codes

This are the additional return codes for this action. The global return codes applies. If there is no error, no return code and no message is returned.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown

The `message` element can contain more details.

## Shutdown server

```php
<?php
$req = [
  "id" => 123,
];

$ch = curl_init("https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/shutdown");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/shutdown?id=123"
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

Using this endpoint, you can shutdown a cloud server.

### API endpoint

`/cloud/shutdown`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract

### Return codes

This are the additional return codes for this action. The global return codes applies. If there is no error, no return code and no message is returned.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown

The `message` element can contain more details.

## Reinstall server

```php
<?php
$req = [
  "id" => 123,
  "os" => "Debian 11",
];

$ch = curl_init("https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/reinstall");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/reinstall?id=123&os=Debian%2011"
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

Using this endpoint, you can reinstall a cloud server.

<aside class="notice">
During reinstallation, the server credentials will change. You should obtain the new credentials by calling the <code>info</code> endpoint.
</aside>

### API endpoint

`/cloud/reinstall`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract
os | - | **Required** Name and version of operating system to install

### Return codes

This are the additional return codes for this action. The global return codes applies. If there is no error, no return code and no message is returned.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown
807 | Required task parameter is missing

The `message` element can contain more details.

## Reset administrator password

```php
<?php
$req = [
  "id" => 123,
];

$ch = curl_init("https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/password");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/password?id=123"
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

Using this endpoint, you can set a new auto-generated password for a cloud server.

<aside class="notice">
You should obtain the new credentials by calling the <code>info</code> endpoint after the password change.
</aside>

<aside class="notice">
Depending on the operating system, you may have to reboot the server before password change takes effect. There is no automatic reboot.
</aside>

### API endpoint

`/cloud/password`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract

### Return codes

This are the additional return codes for this action. The global return codes applies. If there is no error, no return code and no message is returned.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown

The `message` element can contain more details.

## Authorize SSH key

```php
<?php
$req = [
  "id" => 123,
  "key" => "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCBmgbPAwpa5LUT/9oDuFrQg9Kb0PIKhy/u6nfa6Vw0aCMp6S9wCU061lng9qfNVcthX1Aek8QyOwMq93tzP20lzI7+DPOdCLhotUcy2SQ3yVI/wNMQR91VoY7aFkhRqQEOXo2RME4Au6x3AiONjAuNJEQxmtnJfdkYel/zLUKtmIAZNhU1WNoZN5RJqx9onahMDeiESWTHRnmKha3mK8lFaP6/eXKR3qbTW426ak41Kk5/zn6YletlQJopoQP2NYeG+TWV60X9Sq0OAIY9MZqWt02zJA7Q5Na71sKREZWVczcWQcnejv70zKY9XxVNy74WmWIkVyt6qzTgz3J21/hH example",
];

$ch = curl_init("https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/key");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl -d "ssh-rsa%20AAAAB3NzaC1yc2EAAAADAQABAAABAQCBmgbPAwpa5LUT%2F9oDuFrQg9Kb0PIKhy%2Fu6nfa6Vw0aCMp6S9wCU061lng9qfNVcthX1Aek8QyOwMq93tzP20lzI7%2BDPOdCLhotUcy2SQ3yVI%2FwNMQR91VoY7aFkhRqQEOXo2RME4Au6x3AiONjAuNJEQxmtnJfdkYel%2FzLUKtmIAZNhU1WNoZN5RJqx9onahMDeiESWTHRnmKha3mK8lFaP6%2FeXKR3qbTW426ak41Kk5%2Fzn6YletlQJopoQP2NYeG%2BTWV60X9Sq0OAIY9MZqWt02zJA7Q5Na71sKREZWVczcWQcnejv70zKY9XxVNy74WmWIkVyt6qzTgz3J21%2FhH%20example" "https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/key?id=123"
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

Using this endpoint, you can authorize a SSH key for a cloud server.

<aside class="notice">
A previous set SSH key using this function will be deauthorized.
</aside>

<aside class="notice">
Setting a SSH key for a server running Windows will fail.
</aside>

<aside class="notice">
Depending on the operating system, you may have to reboot the server before the change takes effect. There is no automatic reboot.
</aside>

### API endpoint

`/cloud/key`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract
key | - | **Required** SSH key in OpenSSH format

### Return codes

This are the additional return codes for this action. The global return codes applies. If there is no error, no return code and no message is returned.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown
807 | Required task parameter is missing

The `message` element can contain more details.

## VNC console

```php
<?php
$req = [
  "id" => 123,
];

$ch = curl_init("https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/vnc");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/vnc?id=123"
```

> The above command returns JSON structured like this:

```json
{
  "url": "https://vncviewer.eu:5900/vnc.html?password=3E%3B1WHG2&autoconnect=true&resize=scale"
}
```

Using this endpoint, you can start a VNC session for a cloud server. The command returns an URL to a web VNC client. Using your own client is not possible.

<aside class="notice">
The VNC link is valid once and must be used within 5 seconds. After that period, the link expires for security reasons.
</aside>

### API endpoint

`/cloud/vnc`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract

### Return codes

This are the additional return codes for this action. The global return codes applies. If there is no error, no return code and no message is returned.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown

The `message` element can contain more details.

## Traffic graphs

```php
<?php
$req = [
  "id" => 123,
  "from" => strtotime("-24 hours"),
  "to" => strtotime("now"),
];

$ch = curl_init("https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/traffic");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/api/CUSTOMER_ID/API_KEY/cloud/traffic?id=123&from=168600000&to=1686004852"
```

> The above command returns JSON structured like this:

```json
{
  "image_url": "https://trafficviewer.eu/?dev=6&port=tap123i0&from=1654034400&to=1686004852&signature=92dfb78a"
}
```

Using this endpoint, you can retrieve a traffic graph for a cloud server. You must specify a time range and get a permanent valid link to the according traffic graph as image.

### API endpoint

`/cloud/traffic`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract
from | - | **Required** Start date as UNIX timestamp 
to | - | **Required** End date as UNIX timestamp 

### Return codes

This are the additional return codes for this action. The global return codes applies. If there is no error, no return code and no message is returned.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown
807 | Required task parameter is missing

The `message` element can contain more details.

## Set note/description

```php
<?php
$req = [
  "id" => 1,
  "note" => "Per API bestellt",
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/hosting/set");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/hosting/set?id=1&note=Per+API+bestellt"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Description set successful.",
  "data": {}
}
```

Using this endpoint, you can update a note for a existing contract.

### API endpoint

`/hosting/set`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract
note | "" | The note to set for the contract

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown

## Upgrade a server

<aside class="notice">
Upgrading a server is currently only possible via web. We will enable server upgrades by API soon.
</aside>

## Cancel a server

```php
<?php
$req = [
  "id" => 1,
  "date" => "2019-02-12",
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/hosting/cancel");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/hosting/cancel?id=1&date=2019-02-12"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Cancellation date set successful.",
  "data": {
    "date": "2019-02-12"
  }
}
```

Using this endpoint, you can set the cancellation date for a contract. Please make sure that you retrieve the possible dates first, as only valid dates are accepted.

<aside class="notice">
In order to revoke an existing contract cancellation, please submit the date <code>0000-00-00</code>.
</aside>

### API endpoint

`/hosting/cancel`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required** The ID of the contract
date | - | **Required** Date of cancellation

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | No contract ID specified
804 | Specified contract is unknown
805 | No cancellation is possible (product without recurring costs)
806 | Provided cancellation date is invalid

# Domains

## List your domains

```php
<?php
$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/list");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/list"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Domains fetched.",
  "data": [
    {
      "domain": "example.com",
      "recurring": 7.99,
      "created": "2019-01-13",
      "expiration": "2020-01-12",
      "auto_renew": true,
      "transfer_lock": true,
      "privacy": false,
      "privacy_price": 0.00,
      "status": "REG_OK",
      "last_sync": "2019-01-13 16:06:56",
      "trade": 0.00,
      "owner": {
        "firstname": "John",
				"lastname": "Doe",
				"company": "",
				"street": "Example street 1",
				"country": "US",
				"postcode": "12345",
				"city": "Example city",
				"telephone": "0019289999",
				"telefax": "0019289998",
				"email": "john.doe@example.com",
				"remarks": ""
      },
      "admin": {
        "firstname": "John",
				"lastname": "Doe",
				"company": "",
				"street": "Example street 1",
				"country": "US",
				"postcode": "12345",
				"city": "Example city",
				"telephone": "0019289999",
				"telefax": "0019289998",
				"email": "john.doe@example.com",
				"remarks": ""
      },
      "tech": {
        "firstname": "John",
				"lastname": "Doe",
				"company": "",
				"street": "Example street 1",
				"country": "US",
				"postcode": "12345",
				"city": "Example city",
				"telephone": "0019289999",
				"telefax": "0019289998",
				"email": "john.doe@example.com",
				"remarks": ""
      },
      "zone": {
        "firstname": "John",
				"lastname": "Doe",
				"company": "",
				"street": "Example street 1",
				"country": "US",
				"postcode": "12345",
				"city": "Example city",
				"telephone": "0019289999",
				"telefax": "0019289998",
				"email": "john.doe@example.com",
				"remarks": ""
      },
      "ns": [
        "ns1.manager.nuxoa.de",
        "ns2.manager.nuxoa.de"
      ],
    }
  ]
}
```

This endpoint is used to get listed all your domains.

### API endpoint

`/domain/list`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | Filter by domain name (wildcard)

### Return codes

The global return codes applies.

## Register a domain

```php
<?php
$req = [
  "domain" => "example.com",
  "owner_firstname" => "John",
  "owner_lastname" => "Doe",
  "owner_company" => "",
  "owner_street" => "Example street 1",
  "owner_country" => "US",
  "owner_postcode" => "12345",
  "owner_city" => "Example city",
  "owner_telephone" => "0019289999",
  "owner_telefax" => "0019289998",
  "owner_email" => "john.doe@example.com",
  "admin_firstname" => "John",
  "admin_lastname" => "Doe",
  "admin_company" => "",
  "admin_street" => "Example street 1",
  "admin_country" => "US",
  "admin_postcode" => "12345",
  "admin_city" => "Example city",
  "admin_telephone" => "0019289999",
  "admin_telefax" => "0019289998",
  "admin_email" => "john.doe@example.com",
  "tech_firstname" => "John",
  "tech_lastname" => "Doe",
  "tech_company" => "",
  "tech_street" => "Example street 1",
  "tech_country" => "US",
  "tech_postcode" => "12345",
  "tech_city" => "Example city",
  "tech_telephone" => "0019289999",
  "tech_telefax" => "0019289998",
  "tech_email" => "john.doe@example.com",
  "zone_firstname" => "John",
  "zone_lastname" => "Doe",
  "zone_company" => "",
  "zone_street" => "Example street 1",
  "zone_country" => "US",
  "zone_postcode" => "12345",
  "zone_city" => "Example city",
  "zone_telephone" => "0019289999",
  "zone_telefax" => "0019289998",
  "zone_email" => "john.doe@example.com",
  "ns1" => "ns1.manager.nuxoa.de",
  "ns2" => "ns2.manager.nuxoa.de",
  "ip" => "8.8.8.8",
  "async" => true,
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/register");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/register?domain=example.com&owner_firstname=John&owner_lastname=Doe&owner_company=&owner_street=Example+street+1&owner_country=US&owner_postcode=12345&owner_city=Example+city&owner_telephone=0019289999&owner_telefax=0019289998&owner_email=john.doe%40example.com&admin_firstname=John&admin_lastname=Doe&admin_company=&admin_street=Example+street+1&admin_country=US&admin_postcode=12345&admin_city=Example+city&admin_telephone=0019289999&admin_telefax=0019289998&admin_email=john.doe%40example.com&tech_firstname=John&tech_lastname=Doe&tech_company=&tech_street=Example+street+1&tech_country=US&tech_postcode=12345&tech_city=Example+city&tech_telephone=0019289999&tech_telefax=0019289998&tech_email=john.doe%40example.com&zone_firstname=John&zone_lastname=Doe&zone_company=&zone_street=Example+street+1&zone_country=US&zone_postcode=12345&zone_city=Example+city&zone_telephone=0019289999&zone_telefax=0019289998&zone_email=john.doe%40example.com&ns1=ns1.manager.nuxoa.de&ns2=ns2.manager.nuxoa.de&ip=8.8.8.8&async=1"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Domain registration successful.",
  "data": {}
}
```

Using this endpoint, you can register a domain. Please make sure that the domain is available first.

### API endpoint

`/domain/register`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | **Required** The domain to register
owner_* | - | **Required** The owner contact data - see request for details
admin_* | - | **Required** The admin contact data - see request for details
tech_* | Provider data | The tech contact data - needs special permission
zone_* | Provider data | The zone contact data - needs special permission
ns1..5 | - | **At least first 2 required** The nameserver hostnames to use
ip | - | **Required if provider nameservers are used** The standard IP address to create DNS zone
async | false | Set to `true` in order to execute registration in the background - faster response

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | No domain name specified
804 | Invalid domain name specified
805 | TLD not supported
806 | Domain availibility status can not be fetched
807 | Domain not available
808 | Not enough credit
809 | Contact details missing (more information in `message` element)
810 | Nameserver missing
811 | Invalid IP address
812 | Domain registration already in progress
813 | Domain registration failed

## Transfer a domain

```php
<?php
$req = [
  "domain" => "example.com",
  "password" => "AuthCode",
  "owner_firstname" => "John",
  "owner_lastname" => "Doe",
  "owner_company" => "",
  "owner_street" => "Example street 1",
  "owner_country" => "US",
  "owner_postcode" => "12345",
  "owner_city" => "Example city",
  "owner_telephone" => "0019289999",
  "owner_telefax" => "0019289998",
  "owner_email" => "john.doe@example.com",
  "admin_firstname" => "John",
  "admin_lastname" => "Doe",
  "admin_company" => "",
  "admin_street" => "Example street 1",
  "admin_country" => "US",
  "admin_postcode" => "12345",
  "admin_city" => "Example city",
  "admin_telephone" => "0019289999",
  "admin_telefax" => "0019289998",
  "admin_email" => "john.doe@example.com",
  "tech_firstname" => "John",
  "tech_lastname" => "Doe",
  "tech_company" => "",
  "tech_street" => "Example street 1",
  "tech_country" => "US",
  "tech_postcode" => "12345",
  "tech_city" => "Example city",
  "tech_telephone" => "0019289999",
  "tech_telefax" => "0019289998",
  "tech_email" => "john.doe@example.com",
  "zone_firstname" => "John",
  "zone_lastname" => "Doe",
  "zone_company" => "",
  "zone_street" => "Example street 1",
  "zone_country" => "US",
  "zone_postcode" => "12345",
  "zone_city" => "Example city",
  "zone_telephone" => "0019289999",
  "zone_telefax" => "0019289998",
  "zone_email" => "john.doe@example.com",
  "ns1" => "ns1.manager.nuxoa.de",
  "ns2" => "ns2.manager.nuxoa.de",
  "ip" => "8.8.8.8",
  "async" => true,
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/transfer");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/transfer?domain=example.com&password=AuthCode&owner_firstname=John&owner_lastname=Doe&owner_company=&owner_street=Example+street+1&owner_country=US&owner_postcode=12345&owner_city=Example+city&owner_telephone=0019289999&owner_telefax=0019289998&owner_email=john.doe%40example.com&admin_firstname=John&admin_lastname=Doe&admin_company=&admin_street=Example+street+1&admin_country=US&admin_postcode=12345&admin_city=Example+city&admin_telephone=0019289999&admin_telefax=0019289998&admin_email=john.doe%40example.com&tech_firstname=John&tech_lastname=Doe&tech_company=&tech_street=Example+street+1&tech_country=US&tech_postcode=12345&tech_city=Example+city&tech_telephone=0019289999&tech_telefax=0019289998&tech_email=john.doe%40example.com&zone_firstname=John&zone_lastname=Doe&zone_company=&zone_street=Example+street+1&zone_country=US&zone_postcode=12345&zone_city=Example+city&zone_telephone=0019289999&zone_telefax=0019289998&zone_email=john.doe%40example.com&ns1=ns1.manager.nuxoa.de&ns2=ns2.manager.nuxoa.de&ip=8.8.8.8&async=1"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Domain transfer successful.",
  "data": {}
}
```

Using this endpoint, you can transfer a domain. The request is identical to the `register` request, except requiring the parameter `password`.

### API endpoint

`/domain/transfer`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | **Required** The domain to transfer
password | - | **Required** The AuthCode to transfer the domain
owner_* | - | **Required** The owner contact data - see request for details
admin_* | - | **Required** The admin contact data - see request for details
tech_* | Provider data | The tech contact data - needs special permission
zone_* | Provider data | The zone contact data - needs special permission
ns1..5 | - | **At least first 2 required** The nameserver hostnames to use
ip | - | **Required if provider nameservers are used** The standard IP address to create DNS zone
async | false | Set to `true` in order to execute transfer in the background - faster response

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | No domain name specified
804 | Invalid domain name specified
805 | TLD not supported
806 | Domain availibility status can not be fetched
807 | Domain is not registered, transfer not available
808 | Not enough credit
809 | Contact details missing (more information in `message` element)
810 | AuthCode not specified
811 | Nameserver missing
812 | Invalid IP address
813 | Domain transfer already in progress
814 | Domain transfer failed

## Edit a domain

```php
<?php
$req = [
  "domain" => "example.com",
  "owner_firstname" => "John",
  "owner_lastname" => "Doe",
  "owner_company" => "",
  "owner_street" => "Example street 1",
  "owner_country" => "US",
  "owner_postcode" => "12345",
  "owner_city" => "Example city",
  "owner_telephone" => "0019289999",
  "owner_telefax" => "0019289998",
  "owner_email" => "john.doe@example.com",
  "admin_firstname" => "John",
  "admin_lastname" => "Doe",
  "admin_company" => "",
  "admin_street" => "Example street 1",
  "admin_country" => "US",
  "admin_postcode" => "12345",
  "admin_city" => "Example city",
  "admin_telephone" => "0019289999",
  "admin_telefax" => "0019289998",
  "admin_email" => "john.doe@example.com",
  "tech_firstname" => "John",
  "tech_lastname" => "Doe",
  "tech_company" => "",
  "tech_street" => "Example street 1",
  "tech_country" => "US",
  "tech_postcode" => "12345",
  "tech_city" => "Example city",
  "tech_telephone" => "0019289999",
  "tech_telefax" => "0019289998",
  "tech_email" => "john.doe@example.com",
  "zone_firstname" => "John",
  "zone_lastname" => "Doe",
  "zone_company" => "",
  "zone_street" => "Example street 1",
  "zone_country" => "US",
  "zone_postcode" => "12345",
  "zone_city" => "Example city",
  "zone_telephone" => "0019289999",
  "zone_telefax" => "0019289998",
  "zone_email" => "john.doe@example.com",
  "ns1" => "ns1.manager.nuxoa.de",
  "ns2" => "ns2.manager.nuxoa.de",
  "ip" => "8.8.8.8"
  "transfer_lock" => true,
  "auto_renew" => true,
  "privacy" => false,
  "async" => true,
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/modify");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/modify?domain=example.com&owner_firstname=John&owner_lastname=Doe&owner_company=&owner_street=Example+street+1&owner_country=US&owner_postcode=12345&owner_city=Example+city&owner_telephone=0019289999&owner_telefax=0019289998&owner_email=john.doe%40example.com&admin_firstname=John&admin_lastname=Doe&admin_company=&admin_street=Example+street+1&admin_country=US&admin_postcode=12345&admin_city=Example+city&admin_telephone=0019289999&admin_telefax=0019289998&admin_email=john.doe%40example.com&tech_firstname=John&tech_lastname=Doe&tech_company=&tech_street=Example+street+1&tech_country=US&tech_postcode=12345&tech_city=Example+city&tech_telephone=0019289999&tech_telefax=0019289998&tech_email=john.doe%40example.com&zone_firstname=John&zone_lastname=Doe&zone_company=&zone_street=Example+street+1&zone_country=US&zone_postcode=12345&zone_city=Example+city&zone_telephone=0019289999&zone_telefax=0019289998&zone_email=john.doe%40example.com&ns1=ns1.manager.nuxoa.de&ns2=ns2.manager.nuxoa.de&ip=8.8.8.8&transfer_lock=1&auto_renew=1&privacy=0&async=1"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Domain updated.",
  "data": {}
}
```

Using this endpoint, you can modify an existing domain.

### API endpoint

`/domain/modify`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | **Required** The domain to edit
owner_* | - | **Required** The owner contact data - see request for details
admin_* | - | **Required** The admin contact data - see request for details
tech_* | Provider data | The tech contact data - needs special permission
zone_* | Provider data | The zone contact data - needs special permission
ns1..5 | - | **At least first 2 required** The nameserver hostnames to use
ip | - | **Required if switching to provider nameservers** The standard IP address to create DNS zone
transfer_lock | false | Set the transfer lock status (if supported by TLD)
auto_renew | false | Set the auto renew status
privacy | false | Set the WHOIS privacy status (if supported by TLD, can be chargeable)
async | false | Set to `true` in order to execute modification in the background - faster response

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | Domain not found
804 | Internal error
805 | Contact details missing (more information in `message` element)
806 | Nameserver missing
807 | Missing credit for auto renew
808 | Invalid IP address
809 | Domain update failed

## Change domain owner (trade)

```php
<?php
$req = [
  "domain" => "example.com",
  "owner_firstname" => "John",
  "owner_lastname" => "Doe",
  "owner_company" => "",
  "owner_street" => "Example street 1",
  "owner_country" => "US",
  "owner_postcode" => "12345",
  "owner_city" => "Example city",
  "owner_telephone" => "0019289999",
  "owner_telefax" => "0019289998",
  "owner_email" => "john.doe@example.com",
  "admin_firstname" => "John",
  "admin_lastname" => "Doe",
  "admin_company" => "",
  "admin_street" => "Example street 1",
  "admin_country" => "US",
  "admin_postcode" => "12345",
  "admin_city" => "Example city",
  "admin_telephone" => "0019289999",
  "admin_telefax" => "0019289998",
  "admin_email" => "john.doe@example.com",
  "tech_firstname" => "John",
  "tech_lastname" => "Doe",
  "tech_company" => "",
  "tech_street" => "Example street 1",
  "tech_country" => "US",
  "tech_postcode" => "12345",
  "tech_city" => "Example city",
  "tech_telephone" => "0019289999",
  "tech_telefax" => "0019289998",
  "tech_email" => "john.doe@example.com",
  "zone_firstname" => "John",
  "zone_lastname" => "Doe",
  "zone_company" => "",
  "zone_street" => "Example street 1",
  "zone_country" => "US",
  "zone_postcode" => "12345",
  "zone_city" => "Example city",
  "zone_telephone" => "0019289999",
  "zone_telefax" => "0019289998",
  "zone_email" => "john.doe@example.com",
  "async" => true,
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/trade");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/trade?domain=example.com&owner_firstname=John&owner_lastname=Doe&owner_company=&owner_street=Example+street+1&owner_country=US&owner_postcode=12345&owner_city=Example+city&owner_telephone=0019289999&owner_telefax=0019289998&owner_email=john.doe%40example.com&admin_firstname=John&admin_lastname=Doe&admin_company=&admin_street=Example+street+1&admin_country=US&admin_postcode=12345&admin_city=Example+city&admin_telephone=0019289999&admin_telefax=0019289998&admin_email=john.doe%40example.com&tech_firstname=John&tech_lastname=Doe&tech_company=&tech_street=Example+street+1&tech_country=US&tech_postcode=12345&tech_city=Example+city&tech_telephone=0019289999&tech_telefax=0019289998&tech_email=john.doe%40example.com&zone_firstname=John&zone_lastname=Doe&zone_company=&zone_street=Example+street+1&zone_country=US&zone_postcode=12345&zone_city=Example+city&zone_telephone=0019289999&zone_telefax=0019289998&zone_email=john.doe%40example.com&async=1"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Trade successful.",
  "data": {}
}
```

Using this endpoint, you can execute a domain owner change (trade). This is a chargeable action required if you want to change the domain owner data for a TLD with chargeable domain owner change. You are not able to change the domain owner via the `domain/modify` endpoint in this case.

### API endpoint

`/domain/trade`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | **Required** The domain to execute the trade for
owner_* | - | **Required** The owner contact data - see request for details
admin_* | - | **Required** The admin contact data - see request for details
tech_* | Provider data | The tech contact data - needs special permission
zone_* | Provider data | The zone contact data - needs special permission
async | false | Set to `true` in order to execute trade in the background - faster response

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | Domain not found
804 | Internal error
805 | Contact details missing (more information in `message` element)
806 | Trade not possible for this TLD
807 | Not enough credit
808 | Trade failed

## Request authcode

```php
<?php
$req = [
  "domain" => "example.com",
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/password");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/password?domain=example.com"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Authcode fetched.",
  "data": {
    "code": "q1w2e3r4t5"
  }
}
```

Using this endpoint, you can request the authcode for your domain.

### API endpoint

`/domain/password`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | **Required** The domain to request the authcode for

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | Domain not found
804 | Internal error

## Delete/return a domain

```php
<?php
$req = [
  "domain" => "example.com",
  "type" => "0",
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/delete");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/domain/delete?domain=example.com&type=0"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Domain deleted/returned to registry.",
  "data": {}
}
```

Using this endpoint, you can delete a domain or return it to registry.

### API endpoint

`/domain/delete`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | **Required** The domain to request the authcode for
type | - | **Required** The type of deletion (0 = normal delete, 1 = connected return, 2 = disconnected return)

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | Domain not found
804 | Internal error
805 | Invalid type specified
806 | Deletion/Returnation failed

# DNS zones

## List your zones

```php
<?php
$req = [
  "domain" => "example.com",
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/dns/list");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/dns/list?domain=example.com"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Zones fetched.",
  "data": [
    "example.com",
    "example.de"
  ]
}
```

Using this endpoint, you can get all DNS zones existing for domains using the nameservers of the provider.

### API endpoint

`/dns/list`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | Filter by domain (wildcard)

### Return codes

The global return codes applies.

## Get zone records

```php
<?php
$req = [
  "domain" => "example.com"
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/dns/show");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/dns/show?domain=example.com"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Zone fetched.",
  "data": {
    "262": {
      "name": "",
      "type": "A",
      "content": "8.8.8.8",
      "ttl": 3600,
      "priority": 0
    },
    "263": {
      "name": "",
      "type": "MX",
      "content": "example.com",
      "ttl": 3600,
      "priority": 10
    }
  }
}
```

Using this endpoint, you can get all records existing in the specified DNS zone.

### API endpoint

`/dns/show`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | **Required** The domain/zone name you want to get

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | Domain not found
804 | Zone not found

## Add a record

```php
<?php
$req = [
  "domain" => "example.com",
  "name" => "www",
  "type" => "A",
  "content" => "8.8.8.8",
  "ttl" => "3600",
  "priority" => "0",
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/dns/add");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/dns/add?domain=example.com&name=www&type=A&content=8.8.8.8&ttl=3600&priority=0"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Record added.",
  "data": {}
}
```

Using this endpoint, you can create a new record in a DNS zone.

### API endpoint

`/dns/add`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | **Required** The domain/zone name you want to add a record in
name | - | **Required** The record name (can be empty)
type | - | **Required** The record type
content | - | **Required** The content of the record
ttl | - | **Required** Time-to-live (e.g. 3600)
priority | - | **Required** Priority (can be 0)

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | Domain not found
804 | Zone not found
805 | Error at adding record (invalid record data)

## Edit a record

```php
<?php
$req = [
  "domain" => "example.com",
  "record" => "262",
  "name" => "www",
  "type" => "A",
  "content" => "8.8.8.8",
  "ttl" => "3600",
  "priority" => "0",
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/dns/edit");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/dns/edit?domain=example.com&record=262&name=www&type=A&content=8.8.8.8&ttl=3600&priority=0"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Record edited.",
  "data": {}
}
```

Using this endpoint, you can edit an existing record in a DNS zone.

### API endpoint

`/dns/edit`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | **Required** The domain/zone name you want to edit a record in
record | - | **Required** The ID of the record to be edited (find in `dns/show` as key)
name | - | **Required** The record name (can be empty)
type | - | **Required** The record type
content | - | **Required** The content of the record
ttl | - | **Required** Time-to-live (e.g. 3600)
priority | - | **Required** Priority (can be 0)

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | Domain not found
804 | Zone not found
805 | No valid record ID specified
806 | Record not found
807 | Error at editing record (invalid record data)

## Delete a record

```php
<?php
$req = [
  "domain" => "example.com",
  "record" => "262",
];

$ch = curl_init("https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/dns/delete");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://manager.nuxoa.de/api/CUSTOMER_ID/API_KEY/dns/delete?domain=example.com&record=262"
```

> The above command returns JSON structured like this:

```json
{
  "code": 100,
  "message": "Record deleted.",
  "data": {}
}
```

Using this endpoint, you can delete an existing record from a DNS zone.

### API endpoint

`/dns/delete`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | **Required** The domain/zone name you want to delete a record in
record | - | **Required** The ID of the record to be deleted (find in `dns/show` as key)

### Return codes

This are the additional return codes for this action. The global return codes applies.

Return Code | Meaning
---------- | -------
803 | Domain not found
804 | Zone not found
805 | No valid record ID specified
806 | Record not found

# Return codes

The NUXOA API uses the following return codes, they are contained in the `code` element in the JSON response:

Return Code | Meaning
---------- | -------
100 | Request was successful
800 | Authorization failed, please check customer ID and API key
801 | Method unknown
802 | Action unknown

There are additional return codes in failure case for each action, please see the corresponding documentation.

<aside class="notice">
The response also contains the <code>message</code> element, which contains a textual description of the error code and more error details.
</aside>
