Role : k8_setup
=========

To add node to kubernetes cluster.

Requirements
------------

Host will be added as Worker or Control Plane as per hostname's group from inventory (control_plane or worker).


Variables
--------------
1. **defaults/main.yml:**
    - sysctl_file_path:
    - containerd_mod_file_path
2. **vars/main.yml:**
    - k8_dependencies
    - kube_packages
    - kube_version

Tags
--------------
1. **reset**: This can be used to remove a master or worker node from cluster but will not remove kubernetes related packages.
Should be used if planing to reuse same node by changing type from worker to control-plain or vice versa
2. **full_reset**: This can used to remove a master or worker node and remove related packages and other configs.

**Note**: It is recommended to reboot a node after reseting and before adding it again.

Sample Playbook
----------------
*sample.yml*

    - hosts: ninjax
      become: yes
      roles:
         - k8s_setup

Sample ansible commands:
----------------
* Running in check mode:

        ansible-playbook sample.yml --check --diff
        
* Initialize cluster:

        ansible-playbook sample.yml -K --tags init,all

* Adding a node to cluster:

        ansible-playbook sample.yml -K

* Reset a node:

        ansible-playbook sample.yml -K --tags reset
