# dummy-prometheus

This dummy project just pull the latest Prometheus image and run.

It collects metrics from the Dummy Python API and from its own metrics.

## Examples of PromQL

Get the all requests made to the endpoint `/api/resource`:

```promql
request_latency_seconds_sum{endpoint="/api/resource"}
```

You can filter by the method too:

```promql
request_latency_seconds_sum{method="GET", endpoint="/api/resource"}
```

You can sum all the number of the request no matter the http method:

```promql
sum(request_latency_seconds_sum{endpoint="/api/resource"})
```

The media latency (the time waste by the server to generate the response):

```
sum(request_latency_seconds_sum{endpoint="/api/resource"}) / sum(request_latency_seconds_count{endpoint="/api/resource"})
```

You can check how many http 400 was produced by the application:

```promql
request_count_total{endpoint="/api/resource", http_status="400"}
```

Or if you want to filter by method too, you can query like:

```promql
request_count_total{endpoint="/api/resource", http_status="400", method="POST"}
```
