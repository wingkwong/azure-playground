# Policies

## Inbound

- Applied on requests when coming in to the API
- Used for authentication, rate limiting, caching

## Outbound

- Applied on oubound information from the API
- Used for filter and transform data, caching

## Backend

- Applied before Calling a backend service, and after a response from that service
- Used for transform data, select method, retry

## Policies Samples

https://docs.microsoft.com/en-us/azure/api-management/policy-samples