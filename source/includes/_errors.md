# Errors

The Engage API will return a HTTP 200 response code for all successful requests. You should check the response code to determine the success of each request.

Some common error responses that you may encounter include:

Code | Name | Description
---------- | ---------- | ----------
400 | Bad Request | Your request is invalid, most commonly a validation issue
401 | Unauthorized | Your authentication is invalid
403 | Forbidden | You cannot perform that action
404 | Not Found | The resource that you requested could not be found
406 | Not Acceptable | Your requested format isn't supported
429 | Too Many Requests | You have made too many requests in a short period of time [See Rate Limiting](#rate-limiting-coming-soon)
500 | Internal Server Error | We're having a problem processing your request. Please try again later or contact support if persistent.
503 | Service Unavailable | We're temporarily offline. Please try again later

Most errors will include a JSON body with further details.
