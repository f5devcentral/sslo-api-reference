# F5 BIG-IP SSL Orchestrator API Examples

This project is an *unofficial* compendium of API examples for creating and managing BIG-IP SSL Orchestrator objects. Please always refer to the official F5 API pages for official API reference. SSL Orchestrator Ansible modules are prefixed with "bigip_sslo_". 

References used in this project:
* [Ansible SSLO Collection](https://clouddocs.f5.com/products/orchestration/ansible/devel/sslo/sslo-collection.html)
* [Ansible SSLO Modules](https://clouddocs.f5.com/products/orchestration/ansible/devel/f5_bigip/modules_2_0/module_index.html)

The purpose of the project is to demonstrate the ease and usefulness of **automated** SSL Orchestrator configuration on BIG-IP. The SSL Orchestrator object space in BIG-IP can essentially be broken down into the following categories. Separate sections and pages are provided for each type of object.

* **Inspection Services**: represent the security "inspection" products that will receive decrypted, service chained traffic from the SSL Orchestrator. These can generally be categorized as:
  * TAP inspection services
  * ICAP inspection services
  * Inline Layer 3 inspection services
  * Inline Layer 2 inspection services
  * HTTP Transparent Proxy inspection services
  * HTTP Explicit Proxy inspection services
  * SWG inspection services

* **Service Chains**: a logical grouping of inspection services in a defined order through which SSL Orchestrator processes traffic.

* **Security Policies**: a set of rules that match traffic patterns and perform actions, including allowing or blocking traffic, decrypting or bypassing decryption, and sending flows to service chains.

* **Applications**: not specifically an SSL Orchestrator object, the security policy is applied to different types of application flows.

* **Utilities and Other**: a set of utilities (delete-all) and ancillary object configurations (resolvers, ocsp-authentication).
  
----
### F5 BIG-IP SSL Orchestrator Architecture

An SSL Orchestrator configuration is simply defined by the following parent-child relationships:
- One or more **inspection services** that receive inspectable traffic flows
- One or more **service chains** that define ordered sets of one or more inspection services
- A **security policy** that references one or more service chains in traffic rules
- An **application** that references a single security policy

<img src="https://github.com/user-attachments/assets/4b6b6248-4ab2-4500-89c9-be32b2af9a8a" width=90%>

This project contains documentation and examples to automate SSL Orchestrator objects with **Ansible**.

----
### Requirements
The SSL Orchestrator Ansible modules require the following. Please see the [Ansible-core Support Matrix](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html) for additional Python-Ansible combinations.
- Python >= 3.10
- Ansible-core >= 2.16

----
### Setting Up an Ansible Automation Environment
While there are many ways to do Ansible, a quick and easy solution is to set up a [Python Virtual Environment](https://clouddocs.f5.com/products/orchestration/ansible/devel/f5_modules/virtualenv.html). 

```bash
## Setup virtualenv (assuming Python3.12 for below)
python3 -m venv ansible_venv
source ansible_venv/bin/activate
pip3 install --upgrade pip
pip3 install ansible-core==2.17.8
pip3 install netaddr

## Setup environment
mkdir ansible && cd ansible
mkdir playbooks
echo -e "[defaults]\ndeprecation_warnings = False\nhost_key_checking = False\nretry_files_enabled = False\nstdout_callback = minimal" >> ansible.cfg

## Install latest f5networks collection
ansible-galaxy collection install git+https://github.com/F5Networks/f5-ansible-bigip.git#ansible_collections/f5networks/f5_bigip -p /home/${USER}/.ansible/collections

## - or install the latest development collection
wget https://f5-ansible.s3.amazonaws.com/collections/f5networks-f5_bigip-devel.tar.gz
ansible-galaxy collection install f5networks-f5_bigip-devel.tar.gz -p /home/${USER}/.ansible/collections --force

## Once in the Python virtual environment, execution of BIG-IP declarative Ansible playbooks look like this:
ansible-playbook -i notahost, playbooks/test.yaml
```

----
### BIG-IP Ansible Playbook Basics
The fundamental structure of a BIG-IP Ansible playbook uses the following form, allowing for the **notahost** inventory tag (no hosts inventory needed) and environment variables passed into the playbook for the BIG-IP address and admin password.

```yaml
---
- name: Create an SSL Orchestrator Config - ICAP Inspection Service
  hosts: all
  connection: httpapi
  gather_facts: false

  collections:
    - f5networks.f5_bigip

  vars:
    ansible_host: "{{ lookup('ansible.builtin.env', 'BIGHOST') }}"
    ansible_httpapi_password: "{{ lookup('ansible.builtin.env', 'BIGPASS') }}"
    ansible_httpapi_port: 443
    ansible_user: "admin"
    ansible_network_os: f5networks.f5_bigip.bigip
    ansible_httpapi_use_ssl: yes
    ansible_httpapi_validate_certs: no

  tasks:
    - fail:
        msg: "Environment variable 'BIGHOST' is empty. Do `export BIGHOST='host'`"
      when: lookup('env', 'BIGHOST') | length == 0

    - fail:
        msg: "Environment variable 'BIGPASS' is empty. Do `export BIGPASS='pass'`"
      when: lookup('env', 'BIGPASS') | length == 0
```

Once the tasks are populated, execute the playbook:
```
export BIGHOST='10.1.1.7'
export BIGPASS='password'
ansible-playbook -i notahost, playbooks/test.yaml
```

Each folder in this project describes the different objects in the SSL Orchestrator configuration, with sample playbooks.
















