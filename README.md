# Docker Compose for Envoy Testing

## Structure

[![Structure](https://github.com/hpcsc/envoy-compose/raw/master/structure.png)](https://github.com/hpcsc/envoy-compose/raw/master/structure.png)

- `curl`: container that acts as downstream service
- `proxy`: Envoy proxy
- `httpbin`: container that acts as upstream service

## Usage

```
docker-compose up -d
docker-compose exec curl sh
```

Inside `curl` container:

```
curl proxy:15001/headers
```

This will ask `httpbin` (through Envoy proxy) to return `curl` request headers. Response looks something like:

```
{
  "headers": {
    "Accept": "*/*",
    "Content-Length": "0",
    "Host": "httpbin",
    "User-Agent": "curl/7.59.0",
    "X-Envoy-Expected-Rq-Timeout-Ms": "15000"
  }
}
```
