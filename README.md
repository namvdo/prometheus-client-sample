### Run the HTTP server:

```shell
go get -d
go build
./main/main -listen-address=:8080
```
See some metrics at: `http://localhost:8080/metrics`
### Run Prometheus using Docker:
```shell
docker run --rm -it -p 9090:9090 prom/prometheus
```
Configure the Prometheus to listen to some metrics from `localhost:8080`.

#### Insider the root of working directory, rerun the Prometheus server by using this command:
```shell
docker run --rm -it -p 9090:9090 -v $(pwd)/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus
```

Now open `http://localhost:9090/graph` to see some metrics pulled from `http://localhost:8080`.

Type this command in the Expression to see some data for a window of 5 minutes:
```shell
avg(rate(rpc_durations_seconds_count[5m])) by (job, service)
```
