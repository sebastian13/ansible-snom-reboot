# Ansible Snom Reboot

This playbook reboots snom phones of the D-Series and M-Series.

## How to use

1. Clone this repo in `roles`

	```
	cd roles
	git clone https://github.com/sebastian13/ansible-snom-reboot.git snom-reboot
	```

1. Create a playbook `snom-reboot.yml`

	```yaml
	---
	- hosts: "{{ hostname | default('snom_mseries') }}"
	  roles:
	    - snom-reboot
	  gather_facts: no
	  connection: local
	  vars:
	    series: m
	
	- hosts: "{{ hostname | default('snom_dseries') }}"
	  roles:
	    - snom-reboot
	  gather_facts: no
	  connection: local
	  vars:
	    series: d
	```

1. Define phones in the `hosts` file

	```
	[snom_dseries]
	phone_01           ansible_host=10.11.0.5 ansible_password=password
	
	[snom_mseries:vars]
	ansible_password=password
	
	[snom_mseries]
	dect_base_01       ansible_host=10.11.1.5
	dect_base_02       ansible_host=10.11.2.5
	```
	
	Ansible recommends to not store passwords in plain text, see [Variables and Vaults](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html#best-practices-for-variables-and-vaults)
	
1. Run the playbook. Optionally limit the deployment to a single device or group.

	```
	ansible-playbook snom-reboot.yml --limit phone_01
	ansible-playbook snom-reboot.yml --limit snom_dseries
	```
	
### Further Information

- [Snom: Can I control my snom phone remotely](http://wiki.snom.com/FAQ/Can_I_control_my_snom_phone_remotely)
- [Ansible: uri - Interacts with webservices](https://docs.ansible.com/ansible/latest/modules/uri_module.html)