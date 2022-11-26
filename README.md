Role Name
=========

This role is an example of installing webservers and load balancer using Docker technology. This role aims to demonstrate basic docker technology and how to run rolling updates.

Requirements
------------

 To use this role, you need to have installed docker. This role was only tested against CentOS 9.

Role Variables
--------------
\### App Variables

\# App code folder name
app_name: simple-web-server
\# App repo
app_repo: 'https://github.com/FerRiosCosta/simple-web-server'
\# App version
app_version: 1
\# App image name
app_image: webserver
\# App containers params
web_containers: 
  \- name: web1
    image: webserver
    version: "{{ app_version }}"
  \- name: web2
    image: webserver
    version: "{{ app_version }}"

\### Load Balancer Variables

\# LB config version
lb_version: 1
\# LB force to rebuild the lb image
lb_force_build: false
\# LB container name
lb_container_name: lb1
\# LB container image name
lb_container_image: haproxy
\# LB container version
lb_container_version: "{{ lb_version }}"
\# LB container app port
lb_container_app_port: 80
\# LB container stats port
lb_container_stats_port: 8081
\# LB container control port
lb_container_control_port: 5555
\# LB image name
lb_image: haproxy

\### Docker params

\# Docker custom network
docker_network_name: app_network

Dependencies
------------

None other roles

Example Playbook
----------------

playbook-deploy-app.yml
---
- name: Deploy app
  hosts: all
  roles:
    - deploy_app

### Command: ansible-playbook playbook-deploy-app.yaml -i inventory/production/ -l node1

License
-------

BSD

Author Information
------------------

Author: Fernando Rios
email: fer.rios.costa@gmail.com
