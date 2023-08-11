# Rate Limiting (Coming soon)

To ensure our platform remains stable and available to everyone, the Engage API will be rate- limited.
We ask developers to use industry standard techniques for limiting calls, caching results and re- trying requests responsibly.
Calls to our API will be managed by request-based limits, allowing up to 40 requests per minute using a leaky bucket algorithm. You’ll be able to see the current rate using the rate limit header, for example:

`X-Engage-Api-Rate-Limit: 32/40`

In this example 32 is the current request count and 40 is the bucket size. The request count decreases according to the leak rate (in this case 1.5 requests per second), so after waiting 10 seconds the response would be down to 17/40, and 0/40 after 48 seconds.

When a request goes over the rate limit, a "HTTP 429 - Too Many Requests" response is given from the API, this will be provided with a Retry-After header with a value in seconds.

`X-Engage-Api-Rate-Limit: 40/40`

`X-Engage-Api-Retry-After: 1.5`
