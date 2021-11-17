# API Responses

Here's a list of detailed response fields for the webhooks api.

## Webhook Base Response

Field | Description
----- | -----------
data | object encapsulating the response, can be a list or a single [webhook response](#webhook-response)
metadata | cursor metadata details to navigate through pages, more details [here](#cursor-metadata-response)

## Webhook Response

Field | Description
----- | -----------
webhook_id | unique id representing your webhook
destinations | list of destinations associated to your webhook, see [destination response](#destination-response)

## Destination Base Response

Field | Description
----- | -----------
data | object encapsulating the response, can be a list or a single [destination response](#destination-response)
metadata | cursor metadata details to navigate through pages, more details [here](#cursor-metadata-response)

## Destination Response

Field | Description
----- | -----------
id | unique id representing your destinations
status | current status of your destination, possible values are listed [here](#destination-status)
attempt | the number of attempts made so far
url | the url set to this destination
additional_headers | headers used when calling this destination's url
last_attempt_at | date time that happened the last attempt of this destination, in UTC
last_response_code | last response code returned by this destination's call
errors | list of errors that happened on this destination

## Cursor Metadata Response
Field | Description
----- | -----------
limit | an integer value of the limit returned per page
next | the next page cursor, returns null if there's no additional pages
previous | the previous page cursor, returns null if there's none
total_count | the total count of records of all pages