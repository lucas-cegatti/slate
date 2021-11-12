# Destinations

## Cancel a Destination

```ruby
require "uri"
require "json"
require "net/http"

url = URI("https://webhooks2.p.rapidapi.com/destinations/cancel")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["x-rapidapi-key"] = "my-key"
request["x-rapidapi-host"] = "webhooks2.p.rapidapi.com"
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "destination_id": "40922a32-9a78-41f0-90aa-0790c0bf781a"
})

response = https.request(request)
puts response.read_body


```

```python
import http.client
import json

conn = http.client.HTTPSConnection("webhooks2.p.rapidapi.com")
payload = json.dumps({
  "destination_id": "40922a32-9a78-41f0-90aa-0790c0bf781a"
})
headers = {
  'x-rapidapi-key': 'my-key',
  'x-rapidapi-host': 'webhooks2.p.rapidapi.com',
  'Content-Type': 'application/json'
}
conn.request("POST", "/destinations/cancel", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://webhooks2.p.rapidapi.com/destinations/cancel' \
--header 'x-rapidapi-key: my-key' \
--header 'x-rapidapi-host: webhooks2.p.rapidapi.com' \
--header 'Content-Type: application/json' \
--data-raw '{
    "destination_id": "40922a32-9a78-41f0-90aa-0790c0bf781a"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-rapidapi-key", "my-key");
myHeaders.append("x-rapidapi-host", "webhooks2.p.rapidapi.com");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "destination_id": "40922a32-9a78-41f0-90aa-0790c0bf781a"
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://webhooks2.p.rapidapi.com/destinations/cancel", requestOptions)
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
                "status": "cancelled",
                "url": "https://my-example.com"
            }
        ],
        "webhook_id": "WEH_xRJkg0mrf6KHQeV1eKWg6KF2oJjuFoYD"
    }
}
```

This endpoints cancels a `retryable` or `pending` destination

### HTTP Request

`POST https://webhooks2.p.rapidapi.com/destinations/cancel`

### Destination Parameters

Parameter | Description
--------- | -----------
destination_id | The ID of the destination to cancel

## Get a specific destination

```ruby
require "uri"
require "net/http"

url = URI("https://webhooks2.p.rapidapi.com/destinations/59c94859-6594-4f50-9cc0-54843680b5da")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["x-rapidapi-key"] = "my-key"
request["x-rapidapi-host"] = "webhooks2.p.rapidapi.com"

response = https.request(request)
puts response.read_body

```

```python
import http.client

conn = http.client.HTTPSConnection("webhooks2.p.rapidapi.com")
payload = ''
headers = {
  'x-rapidapi-key': 'my-key',
  'x-rapidapi-host': 'webhooks2.p.rapidapi.com'
}
conn.request("GET", "/destinations/59c94859-6594-4f50-9cc0-54843680b5da", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request GET 'https://webhooks2.p.rapidapi.com/destinations/59c94859-6594-4f50-9cc0-54843680b5da' \
--header 'x-rapidapi-key: my-key' \
--header 'x-rapidapi-host: webhooks2.p.rapidapi.com'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-rapidapi-key", "my-key");
myHeaders.append("x-rapidapi-host", "webhooks2.p.rapidapi.com");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://webhooks2.p.rapidapi.com/destinations/59c94859-6594-4f50-9cc0-54843680b5da", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> The above command returns JSON structured like this:

```json
{
    "data": {
        "additional_headers": null,
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
        "id": "59c94859-6594-4f50-9cc0-54843680b5da",
        "last_attempt_at": "2021-11-10T17:58:05.352116",
        "last_response_code": "404",
        "status": "retryable",
        "url": "https://my-example.com"
    }
}
```
This endpoints fetchs a specific destination and its details.

### HTTP Request

`GET https://webhooks2.p.rapidapi.com/destinations/<destination_id>`

### URL Parameters

Parameter | Description
--------- | -----------
destination_id | The ID of the destination to retrieve

## Destination Status

Here are all possible status for a destination

Status | Description
--------- | -----------
pending | The destination was created and is awaiting its execution
running | We are trying to deliver the payload to the destination
completed | The payload was successfully delivered to the destination
retryable | The destination is failing to receive the payload, it will have up to 10 retries until failing
cancelled | The destination was cancelled via api
failed | The destination replied with an error code, e.g. connection refused, or it reached the maximum of 10 retries. The api will not make any further request and will remove this destination from the webhooks queue