# role_iptvservice
An Ansible role to create Patch Linux and Windows servers

Requirements
------------

* Collections:

```yaml
ansible.windows (If Patching Windows)
```

Role Variables
--------------

| Variable | Type | Required | Comments |
|-|:-:|:-:|-|
| role_patching_all__linux_dist_upgrade | Bool | Yes | Perform dist-upgrade on Linux or not |
| role_patching_all__linux_storage_server | String | Yes | Server to delegate storing Linux patching logs on |
| role_patching_all__linux_temp_dir | String | Yes | Path to store temporary Linux patching logs |
| role_patching_all__linux_patching_logs_storage | String | Yes | Path to store Linux patching log archives |
| role_patching_all__windows_patching_logs_storage | String | Yes | Path to store Windows patching log archives |
| role_patching_all__windows_storage_server | String | Yes | Server to delegate storing Windows patching logs on |
| role_patching_all__windows_temp_dir | String | Yes | Path to store temporary Windows patching logs |
| role_patching_all__windows_patching_logs_storage | String | Yes | Path to store Windows patching log archives |
| role_patching_all__windows_reject_list | List | No | List of patches to not upgrade on Windows |


Sample Usage:
```yaml
- name: Patch Servers
  hosts: all
  gather_facts: true
  tasks:

    - name: Include Role
      ansible.builtin.include_role:
        name: role_patching_all
      vars:
        role_patching_all__linux_dist_upgrade: false
        role_patching_all__linux_patching_logs_storage: '/patching-logs'
        role_patching_all__linux_storage_server: 'linuxserver'
        role_patching_all__linux_temp_dir: '/tmp'
        role_patching_all__windows_patching_logs_storage: 'c:\patching_logs'
        role_patching_all__windows_patching_temp_dir: 'c:\windows\temp'
        role_patching_all__windows_storage_server: 'windowserver'
        role_patching_all__windows_reject_list:
          - "Razer Inc - HIDClass - 12/1/2013 12:00:00 AM - 6.2.9200.16430"
          - "Realtek Semiconductor Corp. - MEDIA - 9/5/2017 12:00:00 AM - 6.0.1.8248"
          - "Intel - Other hardware - Intel® Ready Mode Technology Device"
          - "Rivet Networks LLC - SoftwareComponent - 3/8/2019 12:00:00 AM - 2.0.2369.0"
          - "INTEL - System - 7/18/1968 12:00:00 AM - 10.1.6.2"
```
