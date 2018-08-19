ansible-role-docker
=========
This role can be used to install or update docker. The update will only proceed if docker is at least 1.12. If version is older playbook will fail on purpose.
The role uses docker-ce package. Currently it is set to install latest version of this package. Role also allows to set content
of /etc/docker/daemon.json file. See "Role Variables" section for more info.

Role Variables
--------------
```
docker_deamon_config:
 storage-driver: "overlay"
package_version: 18.03
package_name: docker-ce
```

If you want to add option to docker daemon you have to do it via `docker_daemon_config` dict.
If file exists backup will be created and existing config will be combined with one defined in `docker_deamon_config`

Currently, due to way how VMs are configured docker uses `overlay` storage driver. This is not recommended for distros from RHEL family
but for now it has to stay this way. To use recommended `devicemapper` first new disk has to be added to VM which will be exclusively used by docker containers.

Example Playbook
----------------

```
---
- hosts: all
  roles:
    - { role: ansible-role-docker, package_version: "18.03" }
```
