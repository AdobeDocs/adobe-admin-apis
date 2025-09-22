# Rate limits

The Adobe Admin APIs enforce default rate limits on the volume and frequency of API calls.

## Summary of rate limits

Each client ID or API key is subject to the following limit: **20 requests per second (RPS)**.

## Purpose of rate limits

API rate limits are a standard practice designed to:

- **Prevent abuse**: Protects APIs from being overwhelmed by excessive requests.
- **Protect against downtime**: Reduces the risk of service interruptions.
- **Control costs**: Helps manage resource consumption and associated expenses.

## Handling rate limit errors

When the client-specific or global access limit is exceeded, the API responds with an HTTP **429 Too Many Requests** error. This response includes a **Retry-After** header, which indicates the minimum time the client must wait before making another request. For detailed specifications, refer to [RFC 7231](https://datatracker.ietf.org/doc/html/rfc7231#section-7.1.3).

To address this error, consider the following actions:

- Review your usage and reduce unnecessary requests.
- Implement retry logic using [Retry-After HTTP header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Retry-After) or an [exponential backoff strategy](https://en.wikipedia.org/wiki/Exponential_backoff).
