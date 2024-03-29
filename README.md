Ansible Role for Tezos Baking
=========

This Ansible Role aims to make deploying a Tezos baker fast and easy for Ansible users.

The role is heavily parameterized, allowing users to deploy nodes for different Tezos networks (mainnet/ithacanet/jakartanet/etc..) and various economic protocols to support block transitions.

The role has been tested against [Version 13 of the Tezos Node][tezos_v13].

_This role does not manage any Tezos keys_

https://galaxy.ansible.com/ecadlabs/tezos_baker

Requirements
------------

- Docker (Tested on Debian Buster)
- [ecadlabs.tezos_node][tezos_node_role]

Installation
------------

    ansible-galaxy install ecadlabs.tezos_baker

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

The Tezos network you wish to provision. This variable does not have a default, so you must set it. Typically, values are `jakartanet` or `mainnet`. The `tezos_network` value is used for several purposes; naming of docker containers, naming of a docker network, selection of which Tezos network to use, and validating that snapshot imports are from the expected network

    tezos_network:

The location where on the host the Tezos nodes data directory will reside. This role uses Docker bind mounts over docker volumes.

    node_data_dir: "/srv/tezos/{{ tezos_network }}_node"

The location on the host where the Tezos client configuration will reside. This directory contains client configuration and keys used by the `tezos-client` command.

    client_data_dir: "/srv/tezos/{{ tezos_network }}_client"

The tezos docker image to use.

    octez_version: v13.0

The Tezos economic protocol to run. Around the time of a protocol transition, bakers should run both protocols in parallel. A baker and accuser docker container will be started for each protocol.

    tezos_economic_protocols:
      - 011-PtHangz2
      - 012-Psithaca

Dependencies
------------

- [ecadlabs.tezos_node][tezos_node_role]

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: ecadlabs.tezos_baker
          tezos_network: mainnet

License
-------

MIT

Author Information
------------------

Created by the humans from ECAD Labs Inc. https://ecadlabs.com

[tezos_node_role]: https://galaxy.ansible.com/ecadlabs/tezos_node
[tezos_v13]: https://tezos.gitlab.io/releases/version-13.html
