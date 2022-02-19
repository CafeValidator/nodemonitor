# nodemonitor
Quickly start monitoring your node with pre-configured best-of-class configurations.

# Introduction

This project houses pre-configured node monitoring template configurations for cosmos based nodes. 

## Why is this needed?
Setting up a node monitoring tool requires significant time to :
* Setup the tool and various components.
* Configure the tool for your needs.

Unless you are an expert in the monitoring tool (aka Zabbix), the manual configuration can be tedious.

This project was inspired by the zabbix templates from [eco stake](https://github.com/eco-stake/zabbix-templates). Most of the hard work of configuration has already been done. 
The goal of this project is to extend these templates to allow quick re-use. The plan for `nodemonitor` is to reference an example validator network topology. Then :
* Manually setup the tool to monitor the network. 
* Create a backup of the config. (in the case of zabbix -- likely SQL based backup).
* Write a script to update configuration with real values programmatically.
 
## pre-requisites

Docker, docker-compose

# How do I use this?

### Start
edit zabbix/docker-compose.yml  and set `PHP_TZ` to your timezone.
```
$cd zabbix && mkdir pgdata 
$docker-compose up -d
```

### Stop
```
$cd zabbix
$docker-compose down
```

## What can I do with it?

For now this gets you a vanilla [zabbix](https://www.zabbix.com/) version 5.0.6 installation running on port 8080. You can browse to it at [localhost](http://localhost:8080).  Default creds are "Admin:zabbix"

At this point you are free to start configuring things manually.

### Zabbix Templates

[eco stake zabbix-templates ](https://github.com/eco-stake/zabbix-templates)

## Backups

This configuration uses postgres backend and the DB file is located in `zabbix/pgdata`. You can gain access to the PG database from that directory. Note to do a backup you can do something like

```
$docker-compose down
$cp -pr zabbix/pgdata /path/to/backups
```

## Todo:

Create a backup / restore tool (outside of zabbix) that will import existing configurations, and allow SQL level backups.

## Sample topology

```
validator1: 192.168.1.100
validator2: 192.168.1.110
validator3: 192.168.1.120
```

## Interested in helping out?

If you are a zabbix expert (or power user), we would love to have a working configuration that would monitor the sample topology above. Here's how to help:
* Manually create a working configuration that would monitor the sample topology above.
* Create a backup of the configuration and send it in with a pull request.
* We will give credit to you and others can enjoy your configuration.
* Note the backup / restore capability will be added soon.
