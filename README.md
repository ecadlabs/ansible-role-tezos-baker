Ansible Role for Tezos Baking
=========

This Ansible Role aims to make deploying a Tezos baker fast and easy for Ansible users.

The role is heavily parameterized, allowing users to deploy nodes for different Tezos networks (mainnet/carthagenet/labnet/etc..) and various economic protocols to support block transitions.

The role uses [Version 7 of the Tezos Node][tezosv7], also known as the multinetwork node.

_This role does not manage any Tezos keys_

Requirements
------------

- Docker (Tested on Debian Buster)
- [ecadlabs.tezos_node][tezos_node_role]

Installation
------------

    ansible-galaxy install ecadlabs.tezos_node

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

The Tezos network you wish to provision. This variable does not have a default, so you must set it. Typically, values are `carthagenet` or `mainnet`. The `tezos_network` value is used for several purposes; naming of docker containers, naming of a docker network, selection of which Tezos network to use, and validating that snapshot imports are from the expected network

    tezos_network:

The location where on the host the Tezos nodes data directory will reside. This role uses Docker bind mounts over docker volumes.

    node_data_dir: "/srv/tezos/{{ network }}_node"

The location on the host where the Tezos client configuration will reside. This directory contains client configuration and keys used by the `tezos-client` command.

    client_data_dir: "/srv/tezos/{{ network }}_client"

The tezos docker image to use.

    tezos_docker_image: tezos/tezos:v7.0-rc1

Dependencies
------------

- [ecadlabs.tezos_node][tezos_node_role]

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: ecadlabs.tezos_node
          tezos_network: carthagenet

License
-------

MIT

Author Information
------------------

Created by the humans from ECAD Labs Inc. https://ecadlabs.com

[tezos_node_role]: https://galaxy.ansible.com/jevonearth/tezos_node
[tezos_v7]: https://tezos.gitlab.io/releases/version-7.html