---
title: FastWebhooks API Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href="https://rapidapi.com/fastwebhooks-fastwebhooks-default/api/webhooks2" target="_blank"><img src="https://storage.googleapis.com/code-snippets/connect-on-rapidapi-light.png" width="215" alt="Connect on RapidAPI"></a>

  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - destinations
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the FastWebhooks API
---

# Introduction
## Why use our api?

- We will take care of delivery your message to its destination, giving 10 retries per destination in case of failures
- You can customize the request headers sent to your destinations
- Up to 3 destinations per webhook
- Encrypted payload within our environment
- Simple and easy to use

## About this documentation

We have language bindings in Shell, Ruby, Python and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

## How to connect

Our api is hosted at [RapidApi](https://rapidapi.com/) you must have an account there, it's free and our api supports a free plan that allows you to test our endpoints, check our plans [here](https://rapidapi.com/fastwebhooks-fastwebhooks-default/api/webhooks2/pricing).

# Authentication

We use RapidApi for authentication, you just need to subscribe to one of our plans and use the provided keys to call our endpoints. 

We have a free plan where you can create 150 webhooks per day, check our plans [here](https://rapidapi.com/fastwebhooks-fastwebhooks-default/api/webhooks2/pricing).

RapidApi will expect two headers to be given:

- `x-rapidapi-key` your unique rapid api key to use on your subscribed apis
- `x-rapidapi-host` the api host you're calling, in our case `webhooks2.p.rapidapi.com`

For more details here's a [quick start guide](https://docs.rapidapi.com/docs/consumer-quick-start-guide) from RapidApi's doc

<aside class="notice">
Your created webhooks will be associated to your RapidApi's user key.
</aside>

# Webhooks

## Create a webhook

```ruby
require "uri"
require "json"
require "net/http"

url = URI("https://webhooks2.p.rapidapi.com/")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["x-rapidapi-key"] = "my-key"
request["x-rapidapi-host"] = "webhooks2.p.rapidapi.com"
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "webhook": {
    "payload": "{\"id\": 1}",
    "destinations": [
      {
        "url": "https://my-example.com",
        "additional_headers": {
          "x-my-header": "my-value"
        }
      }
    ]
  }
})

response = https.request(request)
puts response.read_body

```

```python
import http.client
import json

conn = http.client.HTTPSConnection("webhooks2.p.rapidapi.com")
payload = json.dumps({
  "webhook": {
    "payload": "{\"id\": 1}",
    "destinations": [
      {
        "url": "https://my-example.com",
        "additional_headers": {
          "x-my-header": "my-value"
        }
      }
    ]
  }
})
headers = {
  'x-rapidapi-key': 'my-key',
  'x-rapidapi-host': 'webhooks2.p.rapidapi.com',
  'Content-Type': 'application/json'
}
conn.request("POST", "/", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://webhooks2.p.rapidapi.com/' \
--header 'x-rapidapi-key: my-key' \
--header 'x-rapidapi-host: webhooks2.p.rapidapi.com' \
--header 'Content-Type: application/json' \
--data-raw '{
    "webhook": {
        "payload": "{\"id\": 1}",
        "destinations": [
            {
                "url": "https://my-example.com",
                "additional_headers": {
                    "x-my-header": "my-value"
                }
            }
        ]
    }
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-rapidapi-key", "my-key");
myHeaders.append("x-rapidapi-host", "webhooks2.p.rapidapi.com");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "webhook": {
    "payload": "{\"id\": 1}",
    "destinations": [
      {
        "url": "https://my-example.com",
        "additional_headers": {
          "x-my-header": "my-value"
        }
      }
    ]
  }
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://webhooks2.p.rapidapi.com/", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> The above command returns JSON structured like this:

```json
{
    "data": {
        "destinations": [
            {
                "additional_headers": {
                    "x-my-header": "my-value"
                },
                "attempt": 0,
                "errors": [],
                "id": "40922a32-9a78-41f0-90aa-0790c0bf781a",
                "last_attempt_at": null,
                "last_response_code": null,
                "status": "pending",
                "url": "https://my-example.com"
            }
        ],
        "webhook_id": "WEH_xRJkg0mrf6KHQeV1eKWg6KF2oJjuFoYD"
    }
}
```

This endpoint creates a new webhook with up to 3 destinations.

### HTTP Request

`POST https://webhooks2.p.rapidapi.com/`

### Webhook Parameters

Parameter | Description
--------- | -----------
payload | The payload to be sent to this webhook's destinations, we accept payload as strings. Payloads are encrypted in our environment and we decrypt them before sending to the destinatination. Avoid sending sensitive data.
destinations | list of destinations to send the payload to, you can set up to 3 destinations per webhook

### Destinations Parameters
Parameter | Description
--------- | -----------
url | the url to send the payload to
additional_headers | additional headers to append to the request

<aside class="notice">
We always send the payload as a POST method, this cannot be changed.
</aside>

<aside class="notice">
Our default content-type header is application/json, you can change it at destination's additional headers
</aside>


## Get All Webhooks

```ruby
require "uri"
require "net/http"

url = URI("https://webhooks2.p.rapidapi.com/")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["x-rapidapi-key"] = "your-key"
request["x-rapidapi-host"] = "webhooks2.p.rapidapi.com"

response = https.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("webhooks2.p.rapidapi.com")
payload = ''
headers = {
  'x-rapidapi-key': 'your-key',
  'x-rapidapi-host': 'webhooks2.p.rapidapi.com'
}
conn.request("GET", "/", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))

```

```shell
curl --location --request GET 'https://webhooks2.p.rapidapi.com/' \
--header 'x-rapidapi-key: your-key' \
--header 'x-rapidapi-host: webhooks2.p.rapidapi.com'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-rapidapi-key", "your-key");
myHeaders.append("x-rapidapi-host", "webhooks2.p.rapidapi.com");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://webhooks2.p.rapidapi.com/", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "destinations": [
                {
                    "additional_headers": {
                        "x-my-header": "myHeaderValue"
                    },
                    "attempt": 1,
                    "errors": [],
                    "id": "445a95fa-cd68-4b29-8962-4d728d58324a",
                    "last_attempt_at": "2021-11-11T17:54:54.499069",
                    "last_response_code": "200",
                    "status": "completed",
                    "url": "https://my-example-2.com"
                }
            ],
            "webhook_id": "WEH_02sNtwPH4CiFjFK9XzEQLup1E31b_BpV"
        },
        {
            "destinations": [
                {
                    "additional_headers": {},
                    "attempt": 2,
                    "errors": [
                        {
                            "error_code": "404",
                            "error_hint": "https://http.cat/404",
                            "error_message": "<?xml version=\"1.0\" encoding=\"iso-8859-1\"?>\n<!DOCTYPE html PUBLIC \"-//W3C//DTD XHTML 1.0 Transitional//EN\"\n         \"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd\">\n<html xmlns=\"http://www.w3.org/1999/xhtml\" xml:lang=\"en\" lang=\"en\">\n\t<head>\n\t\t<title>404 - Not Found</title>\n\t</head>\n\t<body>\n\t\t<h1>404 - Not Found</h1>\n\t\t<script type=\"text/javascript\" src=\"//wpc.75674.betacdn.net/0075674/www/ec_tpm_bcon.js\"></script>\n\t</body>\n</html>\n"
                        },
                        {
                            "error_code": "404",
                            "error_hint": "https://http.cat/404",
                            "error_message": "<?xml version=\"1.0\" encoding=\"iso-8859-1\"?>\n<!DOCTYPE html PUBLIC \"-//W3C//DTD XHTML 1.0 Transitional//EN\"\n         \"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd\">\n<html xmlns=\"http://www.w3.org/1999/xhtml\" xml:lang=\"en\" lang=\"en\">\n\t<head>\n\t\t<title>404 - Not Found</title>\n\t</head>\n\t<body>\n\t\t<h1>404 - Not Found</h1>\n\t\t<script type=\"text/javascript\" src=\"//wpc.75674.betacdn.net/0075674/www/ec_tpm_bcon.js\"></script>\n\t</body>\n</html>\n"
                        }
                    ],
                    "id": "ed692c05-ddb2-453e-9613-5c5fb70245c3",
                    "last_attempt_at": "2021-11-11T17:54:58.922085",
                    "last_response_code": "404",
                    "status": "retryable",
                    "url": "https://my-example.com/"
                }
            ],
            "webhook_id": "WEH_0qXRu3IEQNfH8OCoZYIZ9hNTeEpQMFgy"
        }
    ]
}
```

This endpoint retrieves all webhooks and their correspondent destinations.

### HTTP Request

`GET https://webhooks2.p.rapidapi.com/`


### HTTP Response

See [Webhook Responses](#webhook-responses)

<!-- ### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted. -->

<!-- <aside class="success">
Webhook retention period is 15 days!
</aside> -->

## Get a Specific Webhook

```ruby
require "uri"
require "net/http"

url = URI("https://webhooks2.p.rapidapi.com/WEH_Pmvq-fpEGMeSPTCyKKfi3mBJL0TV4EVQ")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["x-rapidapi-key"] = "your-key"
request["x-rapidapi-host"] = "webhooks2.p.rapidapi.com"

response = https.request(request)
puts response.read_body

```

```python
import http.client

conn = http.client.HTTPSConnection("webhooks2.p.rapidapi.com")
payload = ''
headers = {
  'x-rapidapi-key': 'your-key',
  'x-rapidapi-host': 'webhooks2.p.rapidapi.com'
}
conn.request("GET", "/WEH_Pmvq-fpEGMeSPTCyKKfi3mBJL0TV4EVQ", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request GET 'https://webhooks2.p.rapidapi.com/WEH_Pmvq-fpEGMeSPTCyKKfi3mBJL0TV4EVQ' \
--header 'x-rapidapi-key: your-key' \
--header 'x-rapidapi-host: webhooks2.p.rapidapi.com'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-rapidapi-key", "your-key");
myHeaders.append("x-rapidapi-host", "webhooks2.p.rapidapi.com");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://webhooks2.p.rapidapi.com/WEH_Pmvq-fpEGMeSPTCyKKfi3mBJL0TV4EVQ", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> The above command returns JSON structured like this:

```json
{
    "data": {
        "destinations": [
            {
                "additional_headers": {
                    "x-my-header": "my-header-value"
                },
                "attempt": 1,
                "errors": [],
                "id": "d6356729-505d-43e6-8016-016e223dfdd0",
                "last_attempt_at": "2021-11-10T17:47:40.132472",
                "last_response_code": "200",
                "status": "completed",
                "url": "https://my-example.com"
            }
        ],
        "webhook_id": "WEH_Pmvq-fpEGMeSPTCyKKfi3mBJL0TV4EVQ"
    }
}
```

This endpoint retrieves a specific webhook and its destinations.

### HTTP Request

`https://webhooks2.p.rapidapi.com/<webhook_id>`

### URL Parameters

Parameter | Description
--------- | -----------
webhook_id | The ID of the webhook to retrieve

### HTTP Response

See [Webhook Responses](#webhook-responses)


## Webhook Responses

Here's a list of detailed response fields for the webhooks api.

### Webhook

Field | Description
----- | -----------
webhook_id | unique id representing your webhook
destinations | list of destinations associated to your webhook

### Destination

Field | Description
----- | -----------
id | unique id representing your destinations
status | current status of your destination, possible values are listed [here](#status)
attempt | the number of attempts made so far
url | the url set to this destination
additional_headers | headers used when calling this destination's url
last_attempt_at | date time that happened the last attempt of this destination, in UTC
last_response_code | last response code returned by this destination's call
errors | list of errors that happened on this destination

### Errors

Field | Description
----- | -----------
error_code | last http code returned
error_hint | a hint linking to http.cat with the error code returned
error_message | the http body returned by the destination