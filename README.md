# ECSS DC/OS Deployment

This set of roles is intended to allow provisioning of the DC/OS system on
Jetstream.

it should work via

`ansible-playbook -i inventory -l localhost,dcos plays/build_and_deploy.yml`
 
####I don't have the file 'clouds.yaml' included, which is a necessity. 

This is equivalent to the openrc.sh - may be included later as a vault.

The basic format looks like:

clouds:
 tacc:
  auth: 
   username: value
   auth\_url: value
   project\_name: value
   password: value 
  user\_domain\_name: value
  project\_domain\_name: value
  identity\_api\_version: 3

# Local edits
Please insert the correct path to an ssh key that you've added to Jetstream in the `ssh.cfg`.

This will need to be inserted in `inventory/group_vars/all` as well.  

If you need to increase the number of nodes, see `inventory/group_vars/all`.

# Basic Description

The `build_and_deploy.yml` playbook has two main components: `create_hosts.yml` and `install.yml`.
Naturally, `create_hosts` builds the necessary set of VMs on Jetstream, and `install` actually 
installs the DC/OS software. The roles used for that have been taken from
https://github.com/dcos-labs/ansible-dcos
and modified slightly to coexist with the deployment playbook for Jetstream, with the addition of
`roles/common/tasks/js_ip_variables.yml`

To completely tear down the DC/OS Infrastructure, use the `destroy_hosts.yml` playbook.
