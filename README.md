# Ansible Snom Reboot

This role reboots snom phones of the D-Series and M-Series.

## Example Playbook

```yaml
---

- name: Reboot M-Series
  hosts: snom_mseries
  gather_facts: no
  connection: local

  roles:
    - sebastian13.snom-reboot

  vars:
  	series: m

- name: Reboot D-Series
  hosts: snom_dseries
  gather_facts: no
  connection: local

  roles:
    - sebastian13.snom-reboot

  vars:
  	series: d
```

## Example inventory

```
[snom_dseries]
phone_01           ansible_host=10.11.0.5 ansible_password=password

[snom_mseries:vars]
ansible_password=password

[snom_mseries]
dect_base_01       ansible_host=10.11.1.5
dect_base_02       ansible_host=10.11.2.5
```

*Ansible recommends to not store passwords in plain text, see [Variables and Vaults](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html#best-practices-for-variables-and-vaults)*

## How to run

Run the playbook. Optionally limit the deployment to a single device or group.

```bash
ansible-playbook snom-reboot.yml --limit phone_01
ansible-playbook snom-reboot.yml --limit snom_dseries
```
	
## Further Information

- [Snom: Can I control my snom phone remotely](http://wiki.snom.com/FAQ/Can_I_control_my_snom_phone_remotely)
- [Ansible: uri - Interacts with webservices](https://docs.ansible.com/ansible/latest/modules/uri_module.html)
