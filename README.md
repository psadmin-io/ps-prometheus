# Prometheus for PeopleSoft
This is a repository for information on setup and configuration of using Prometheus with PeopleSoft systems. Once configured, the JMX Exporter will expose metrics out of PeopleSoft Tuxedo and Weblogic domains. Prometheus can scrape these metrics which can then be alerted on using Alertmanager and/or vizualized with Grafana.

This is leveraging the JMX metrics delivered by PeopleSoft for use with the PeopleSoft Health Center with a javaagent to expose them.

Goals are to provide curated config files to expose useful metrics with minimal setup, and to provide sample dashboards for use with Grafana.

## Installing JMX Exporter
If planning to use JMX Exporter with PeopleSoft (why else are you here?), I recommend using modified version of JMX Exporter [here](https://github.com/cfazzini/ps-jmx_exporter/) 


Choose a port number, and modify `psappsrv.cfg` or `psprcs.cfg` as shown:
```
[PSMONITORSRV]
JavaVM Options=-Dxdo.ConfigFile=%PS_HOME%/appserv/xdo.cfg -javaagent:/path/to/ps-jmx_exporter-0.1.jar=PORTNUM:/path/to/config.yml -Xms32m -Xmx256m
```
Also be sure to enable remote administration (port/user/pass is not important, exporter doesn't use it, but data not available otherwise)
```
[PSTOOLS]
Enable Remote Administration=1
```
***Be sure to modify JavaVM Options in PSMONITORSRV***

## Notes
This has currently only been tested on PeopleTools 8.56. Later releases might have changed the MBean info. Not Production tested yet.

Original JMX Exporter is available [here](https://github.com/prometheus/jmx_exporter)
## Credits
Huge thanks to Nate Werner and his JMX metrics and Mike Ripley for his Javaagent experiments with PeopleSoft.
