<!-- source: https://www.opswat.com/docs/myop/configuration/external-monitoring -->

# External Monitoring

My OPSWAT exposes metrics that can be scraped by monitoring solutions like Prometheus. To view these metrics you can

BashCopycurl http://localhost:9100/metrics

You should see an output like

BashCopy# HELP go_gc_duration_seconds A summary of the GC invocation durations.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 3.8996e-05
go_gc_duration_seconds{quantile="0.25"} 4.5926e-05
go_gc_duration_seconds{quantile="0.5"} 5.846e-05
# etc.

For further configuration with regards to Prometheus please refer to the Prometheus documentation: <https://prometheus.io/docs/guides/node-exporter/#configuring-your-prometheus-instances>
