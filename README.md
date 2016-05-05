# ansible-example-openstack-ceph
> An example Ansible project that demonstrates provisioning, configuring, and managing a Ceph cluster in an OpenStack environment.

## Important Notes
- This project is meant for demonstration purposes only.
- The `library` and `plugins` directories are from the `ceph-ansible` project.
- This is a work in progress

## Overview
This project leverages the roles published by the [ceph/ceph-ansible](https://github.com/ceph/ceph-ansible) project in order to deploy a Ceph storage cluster:
- [ceph/ansible-ceph-common](https://github.com/ceph/ansible-ceph-common)
- [ceph/ansible-ceph-osd](https://github.com/ceph/ansible-ceph-osd)
- [ceph/ansible-ceph-mon](https://github.com/ceph/ansible-ceph-mon)

The main goal of the project is to demonstrate how role-reuse can be accomplished. The strategy used here is to keep track of all required roles in [requirements.yml](requirements.yml). Local usage and development of this project should install roles to the `galaxy-roles` directory, which is ignored by `[.gitignore](.gitignore)`.

[Ansible Tower](https://www.ansible.com/tower) will automatically download all roles contained in `requirements.yml` as part of a project sync.

## Usage
### Ansible Core
1. Install role dependencies
  - `ansible-galaxy install -r requirements.yml -p galaxy-roles -f`
2. Create a `group_vars/all/rhn.yml` containing required variables from [wtcross/ansible-examples-role-base](https://github.com/wtcross/ansible-example-role-base)
3. Modify `group_vars/all/openstack.yml` to have the correct settings
4. Download your OpenStack RC File
5. run `source /path/to/your/openstackrc.sh`
6. run `ansible-playbook create-ceph-cluster.yml`

### Ansible Tower
1. Create a project for `https://github.com/wtcross/ansible-tower-ceph`
2. Create a credential for your OpenStack environment
3. Create a job template for the `create-ceph-cluster.yml` playbook
