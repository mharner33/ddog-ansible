# Example Datadog deployment using Ansible
Example of Datadog install with Ansible with custom agent check for lm-sensors

This repo shows a small example of installing the Datadog Agent using Ansible and includes:
- Install the Datadog agent
- Enable Process collection
- Enable Network Performance Monitoring (NPM)
- Deploy custom agent check files
- set a custom flag (availibilty-zone) based on the host name
- Install the lm_sensors package if not installed (on physical hosts only)
- Install the PySensors package - needed for the Datadog custom check (this uses the pip command installed by Datadog)

Detailed information can be found at [here](https://github.com/DataDog/ansible-datadog)

This script is geared towards linux distributions and there are group settings under the group_vars
directory for the following types:
- Centos
- Ubuntu
- Rocky Linux

You can copy these for any additional linux distros such as Redhat.  Change the user/password/SSH key path for each.
This script does assume management via SSH as described [here](https://docs.ansible.com/ansible/latest/user_guide/connection_details.html)

**Enhancements**
The Datadog ansible role will perform the majority of the installation.  This script assumes the inventory is one large list of hosts, 
as a result, in order to change the availibility-zone tag, I let the role set the default and then change it later.

A better way would be to group your inventory hosts by the appropriate name, and allow the role to set the tag for each group.

**lm_sensors custom check**
The files for the custom check can be found [here](https://github.com/csnewman/datadog-sensors)
It allows Datadog to poll temperature data from the many sensors found in most servers.

There is a remove_agent.yaml file included - which will automate removal of the Datadog agent if you are testing.
