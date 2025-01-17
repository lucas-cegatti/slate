# Destinations

## Get All Destinations

```ruby
require "uri"
require "net/http"

url = URI("https://webhooks2.p.rapidapi.com/destinations")

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
conn.request("GET", "/destinations", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request GET 'https://webhooks2.p.rapidapi.com/destinations' \
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

fetch("https://webhooks2.p.rapidapi.com/destinations", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "additional_headers": {
                "x-my-header": "my-value"
            },
            "attempt": 1,
            "errors": [],
            "id": "ad264149-40f8-4001-91bf-5e2f87a30e17",
            "last_attempt_at": "2021-11-08T10:42:33.399285",
            "last_response_code": "200",
            "status": "completed",
            "url": "https://example.com/webhooks"
        }
    ],
    "metadata": {
        "limit": 50,
        "next": null,
        "previous": null,
        "total_count": 1
    }
}
```

This endpoint retrieves all destinations, use the [filters](#query-parameters) available to restrict your search.

### HTTP Request

`GET https://webhooks2.p.rapidapi.com/destinations`

### HTTP Response

See [Destination Response](#destination-base-response)

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 50 | restrict the limit of records returned by the endpoint, maximum value allowed is 500
next | null | the next cursor page, returns the next 50 records on the pagination, this data is returned at the metadata object on the response, more [here](#cursor-metadata-response)
previous | null | the previous cursor page, returns the previous 50 records on the pagination, this data is returned at the metadata object on the response, more [here](#cursor-metadata-response)
status | all | filters the records by their status, the list of all possible status is available [here](#destination-status)
from_date | | the from date to limit the range of records returned, dates must be send using iso8601 format, ie yyyy-MM-DD, other formats will be ignored
to_date | | the to date to limit the range of records returned, dates must be send using iso8601 format, ie yyyy-MM-DD, other formats will be ignored

## Cancel a Destination

```ruby
require "uri"
require "net/http"

url = URI("https://webhooks2.p.rapidapi.com/destinations/40922a32-9a78-41f0-90aa-0790c0bf781a/cancel")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Post.new(url)
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
conn.request("POST", "/destinations/40922a32-9a78-41f0-90aa-0790c0bf781a/cancel", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://webhooks2.p.rapidapi.com/destinations/40922a32-9a78-41f0-90aa-0790c0bf781a/cancel' \
--header 'x-rapidapi-key: my-key' \
--header 'x-rapidapi-host: webhooks2.p.rapidapi.com' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-rapidapi-key", "my-key");
myHeaders.append("x-rapidapi-host", "webhooks2.p.rapidapi.com");

var raw = "";

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://webhooks2.p.rapidapi.com/destinations/40922a32-9a78-41f0-90aa-0790c0bf781a/cancel", requestOptions)
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

`POST https://webhooks2.p.rapidapi.com/destinations/<destination_id>/cancel`

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

### HTTP Response

See [Destination Response](#destination-base-response)

## Destination Status

Here are all possible status for a destination

Status | Description
--------- | -----------
pending | The destination was created and is awaiting its execution
running | We are delivering the payload to its destination
completed | The payload was successfully delivered to the destination
retryable | The destination is failing to receive the payload, it will have up to 10 retries until failing
cancelled | The destination was cancelled by the user
failed | The destination replied with an error code, e.g. connection refused, or it reached the maximum of 10 retries. The api will not make any further request and will remove this destination from the webhooks queue
