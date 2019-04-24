# Docker Compose for Envoy Testing

## Structure

[![Structure](https://github.com/hpcsc/envoy-compose/raw/master/structure.png)](https://github.com/hpcsc/envoy-compose/raw/master/structure.png)

- `curl`: container that acts as downstream service
- `proxy`: Envoy proxy, listens at port 10000 (Admin API listens at 9901)
- `httpbin`: container that acts as upstream service

## Usage

```
docker-compose up -d
```

### Get Request Headers through Envoy

```
docker-compose exec curl curl proxy:10000/headers
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

### Access Envoy Admin API

```
docker-compose exec curl curl proxy:9901/stats
```

Some Admin API endpoints:

- `/certs` - the certificates on the machine
- `/clusters` - the clusters Envoy is configured with
- `/config_dump` - dump the actual Envoy config
- `/listeners` - the listeners Envoy is configured with
- `/logging` - can view and change logging settings
- `/stats` - Envoy statistics
- `/stats/prometheus` - Envoy statistics as prometheus records
