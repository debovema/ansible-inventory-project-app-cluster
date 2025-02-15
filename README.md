# Ansible inventory to manage *projects*, grouped by *applications*, which target *clusters*

This repository demonstrates a simple Ansible inventory to manage projects defined as logical entities in the inventory rather than actual remote hosts.

## Prerequisites

* Ansible installed with the `ansible-playbook` CLI available

## Concepts

### Project

* A project is a *host* in Ansible inventory terminology with a **local connection** because it defines the variable ```ansible_connection: local``` in the [`projects` generic group](./inventories/group_vars/projects.yml)
* A project *must* belong to the `projects` group
* A project can belong to only one application
* A project can belong to only one cluster
* For the sake of simplicity, the name of the project will be prefixed by the name of the application it belongs to

> Example of a project name: `app1-projectA`

> Example of a project variable file for the `app1-projectA` application: [`host_vars/app1-projectA/vars.yml`](./inventories/host_vars/app1-projectA/vars.yml)

### Application

* An application is a *group* in the Ansible inventory terminology
* Common variables for an application are defined as YAML files in a `inventories/group_vars` subdirectory with the name of the application

> Example of an application variables file for `app1` application: [`group_vars/app1/vars.yml`](./inventories/group_vars/app1/vars.yml)

### Clusters

* A cluster is a *group* in the Ansible inventory terminology
* Common variables for a cluster are defined as YAML files in a `inventories/group_vars` subdirectory with the name of the cluster

> Example of a cluster variables file for `cluster1` cluster: [`group_vars/cluster1/vars.yml`](./inventories/group_vars/cluster1/vars.yml)

## Usage

To show all projects:

```shell
ansible-playbook playbooks/projects.yml
```

To show a specific project:

```shell
ansible-playbook playbooks/projects.yml -e target_projects=app1-projectB
```

To show all projects of a specific application:

```shell
ansible-playbook playbooks/applications.yml -e target_applications=app1
```

To show all projects targeting a specific cluster:

```shell
ansible-playbook playbooks/clusters.yml -e target_clusters=cluster2
```
