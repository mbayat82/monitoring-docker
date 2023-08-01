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
- Access Prometheus using port 9090. 
- Access Grafana using port 3000.
- Access SNMP exporter using port 9116.
- Access Blackbox exporter using port 9115.
- Access Alertmanager using port 9093.
- It is recommened to install a reverse proxy with `https` and unexpose all these ports.
- All applications will start automatically when the host is started or rebooted except snmp_generator. When snmp_generator is started, it will read the generator.yml file and mibs folder and generate snmp.yml file and override the local one. snmp_exporter ready the snmp.yml local file for snmp queries.
- Add mib files to the mibs folder and oids to the generator.yml and run the container. The container will run, generate the snmp.yml file and stop.
- Targets can be added to the target folder under monitoring > promethues
- Alert rules can be added to the alerts folder under monitoring > promethues
- To add a job, edit promethues.yml file under  monitoring > promethues
- To add notifications, edit file alertmanager.yml under monitoring > alertmanager
