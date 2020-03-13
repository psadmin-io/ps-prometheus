# Prometheus for PeopleSoft
This is a repository for information on setup and configuration of using Prometheus with PeopleSoft systems. Once configured, the JMX Exporter will expose metrics out of PeopleSoft Tuxedo and Weblogic domains. Prometheus can scrape these metrics which can then be alerted on using Alertmanager and/or vizualized with Grafana.

This is leveraging the JMX metrics delivered by PeopleSoft for use with the PeopleSoft Health Center with a javaagent to expose them.

Goals are to provide curated config files to expose useful metrics with minimal setup, and to provide sample dashboards for use with Grafana.

## Installing JMX Exporter
You'll need the latest javaagent release of the [JMX Exporter](https://github.com/prometheus/jmx_exporter) (currently 0.12)


Choose a port number, and modify `psappsrv.cfg` or `psprcs.cfg` as shown:
```
[PSMONITORSRV]
JavaVM Options=-Dxdo.ConfigFile=%PS_HOME%/appserv/xdo.cfg **-javaagent:/path/to/jmx_prometheus_javaagent-0.12.0.jar=PORTNUM:/path/to/config.yml** -Xms32m -Xmx256m
```


## Credits
Huge thanks to Nate Werner and his JMX metrics and Mike Ripley for his experiments with Javaagents with PeopleSoft.