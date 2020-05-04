podman_registry
===============

This Ansible role setups a container registry using podman and an existing nginx container.

Role Variables
--------------

| Variable                            | Value                                         |
| ----------------------------------- | --------------------------------------------- |
| ``registry_domain``                 | **fqdn** of this container registry           |
| ``registry_tls_fullchain``          | remote location of certificate                |
| ``registry_tls_key``                | remote location of certificate's key          |
| ``podman_registry_user``            | ``registry``                                  |
| ``podman_registry_password``        | ``registrysecret``                            |
| ``podman_registry_dir``             | ``/var/lib/containers/registry`` (default)    |
| ``nginx_rootdir``                   | ``/tmp/nginx`` (default)                      |
| ``nginx_confdir``                   | ``/etc/nginx/conf.d`` (default)               |
| ``podman_registry_container_name``  | ``registry`` (default)                        |
| ``podman_registry_container_image`` | ``registry:2`` (default)                      |
| ``nginx_container_name``            | ``nginx`` (default)                           |
| ``skip_podman_registry_install``    | ``yes`` or ``no`` (default)                   |
| ``container_state``                 | ``present`` (default) or ``absent``           |

Dependencies
------------

* [ikke_t.podman_container_systemd](https://galaxy.ansible.com/ikke_t/podman_container_systemd)

Example Playbook
----------------

The following playbook setups an authenticated container registry for ``registry.example.com``:

    - name: Setup new container registry
      hosts: all
      tasks:
        - include_role:
            name: podman_registry
        vars:
          registry_domain: "registry.example.com"
          podman_registry_user: "registry"
          podman_registry_password: "registrysecret"
          nginx_rootdir: "/tmp/nginx"
          registry_certdir: "/etc/letsencrypt/live/{{ registry_domain }}"
          registry_tls_fullchain: "{{ registry_certdir }}/fullchain.pem"
          registry_tls_key: "{{ registry_certdir }}/privkey.pem"

License
-------

GPLv3+

Author Information
------------------

Christian Felder
