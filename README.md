# monitoring-docker
# Overview
This project implements a network moniotring solution using Prometheus and Grafana in docker containers. SNMP exporter and Blackbox exporter is part of this soluiton.
# Installation
- Download all files to the host. Don't change the folder structure. The folder structure is as follows
```
  └── monitoring
    ├── alertmanager
    │   └── alertmanager.yml
    ├── blackbox_exporter
    │   └── config.yml
    ├── grafana
    │   └── prometheus_ds.yml
    ├── prometheus
    │   ├── alerts
    │   │   └── rules.yml
    │   ├── prometheus.yml
    │   └── targets
    │       └── mikrotik-targets.yml
    └── snmp_exporter
        ├── generator.yml
        ├── mibs
        │   ├── ACCOUNTING-CONTROL-MIB
        │   ├── mib-jnx-alarm.txt
        │   ├── mib-jnx-analyzer.txt
        │   ├── mib-jnx-atm-cos.txt
        │   └── ...................
        └── snmp.yml
```
- Make sure you have docker container and docker compose installed
- Run the following command `docker-compose -f monitoring-docker-compose.yml up &` to build the docker containers
# Usage
- To access Prometheus, use port 9090.
- To access Grafana, use port 3000.
- To access SNMP exporter, use port 9116.
- To access Blackbox exporter, use port 9115.
- To access Alertmanager, use port 9093.
- It is highly recommended to set up a reverse proxy with `https` and hide all these ports from external exposure.
- All applications will automatically start when the host is started or rebooted, except for snmp_generator. When snmp_generator is initiated, it will read the generator.yml file and mibs folder to generate a snmp.yml file and override the existing local one. snmp_exporter will then read the snmp.yml file for SNMP queries.
- Add MIB files to the mibs folder and OIDs to the generator.yml, and then run the container. The container will generate the snmp.yml file and stop afterward.
- To add targets, place them in the target folder located under monitoring > Prometheus.
- To add alert rules, place them in the alerts folder located under monitoring > Prometheus.
- To add a job, edit the prometheus.yml file under monitoring > Prometheus.
- To add notifications, edit the alertmanager.yml file under monitoring > alertmanager.
