[![Molecule CI/CD](https://github.com/somnoynadno/ansible-role-dockerized-services/actions/workflows/main.yml/badge.svg)](https://github.com/somnoynadno/ansible-role-dockerized-services/actions/workflows/main.yml)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Dockerized Services
===================

Infrastructure provisioning based on docker-compose'd projects.

With this role you can simply manage your services if they have docker-compose.yml in repository.

Description
-----------

Execution process is pretty straightforward:

1. Each repository in `dockerized_services_list` will be cloned to `dockerized_services_base_folder` (if it's already exists, changes will be pulled from remote origin).

2. For each service command ` $ docker-compose up --build -d` will be executed.

3. If service marked as *disabled*, ` $ docker-compose down` will be performed instead.

Requirements
------------

This role strongly depends on git, docker and docker-compose executables. 

Be sure to install them first. 

Role Variables
--------------

Default variables are listed below (see `defaults/main.yml`), you can redefine them:

```yaml
dockerized_services_user: "{{ lookup('env', 'USER') }}"
dockerized_services_group: "{{ lookup('env', 'USER') }}"
# where the repositories will be cloned
dockerized_services_base_folder: "/home/{{ dockerized_services_user }}/services"

# list of all services with configuration
dockerized_services_list: []
# - name: dockerized-service-stub # required
#   repository: "https://github.com/somnoynadno/dockerized-service-stub" # required
#   docker_compose_file: docker-compose.yml # docker-compose.yml by default
#   branch: master # branch to checkout, master by default
#   update: yes # should changes be pulled from origin, 'yes' by default
#   up: true # should this service be up and running, 'true' by default

# allow role to execute docker-compose to manage your services
dockerized_services_management_enabled: true
```

By default this role does nothing. You need to specify at least `dockerized_services_list` variable.

Platforms
---------

Only tested on Ubuntu 18.04 and 20.04.

May run on some other Linux distro, but not tested yet.


Example Usage
-------------

Just include this role in your `playbook.yml` and `requirements.yml` as follows:

```yaml
# requirements.yml
- src: https://github.com/somnoynadno/ansible-role-dockerized-services
  name: ansible-role-dockerized-services
  version: "v0.2.1"


# playbook.yml
- hosts: all
  roles:
    - ansible-role-dockerized-services

```

License
-------

MIT

Author Information
------------------

This role was created in 2022 by [Alexander Zorkin](https://github.com/somnoynadno) for personal use.
