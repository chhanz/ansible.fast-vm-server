fast-vm-server
==============

This role configures OS for use with fast-vm and installs and configures the fast-vm on it.

Requirements
------------

This roles was tested only on CentOS/RHEL 7.3. On RHEL systems this role expects that system is properly registered so it can download and install packages.

Role Variables
--------------

  - configure repositories needed for fast-vm installation
    ```
    config_repositories: true
    ```

  - install packages needed by fast-vm and fast-vm itself
    ```
    install_fastvm: true
    ```

  - configure libvirt for fast-vm access (change groups and permissions settings)
    ```
    config_libvirt_access: true
    ```

  - configure libvirt network for fast-vm (libvirtd service will be enabled after boot)
    ```
    config_libvirt_network: true
    ```

  - configure storage for fast-vm (create thinpool LV)
    ```
    config_storage: true
    ```

  - configure sudoers for fast-vm
    ```
    config_sudoers: true
    ```

  - generate /etc/fast.conf configuration file
    ```
    config_fastvm_conf: true
    ```

  - install OVMF UEFI firmware needed by UEFI fast-vm machines
    ```
    install_ovmf: true
    ```

  - group with access to fast-vm
    - **required by:** *config_libvirt_access, config_sudoers, config_fastvm_conf*
    ```
    fastvm_group: libvirt
    ```

  - name of VG where fast-vm thinpool LV is located
    - **required by:** *config_storage, config_fastvm_conf*
    ```
    fastvm_vg: c7vg
    ```

  - name of fast-vm thinpool LV
    - **required by:** *config_storage, config_fastvm_conf*
    ```
    fastvm_lv: fast-vm-pool
    ```

  - size of fast-vm thinpool LV
    - **required by:** *config_storage, config_fastvm_conf*
    ```
    fastvm_lv_size: 50G
    ```

  - fast-vm network subnet number
    - **required by:** *config_libvirt_network, config_fastvm_conf*
    ```
    fastvm_net: 42
    ```

  - name of fast-vm NAT libvirt network
    - **required by:** *config_libvirt_network, config_fastvm_conf*
    ```
    fastvm_net_name: fast-vm-nat
    ```

  - prefix for fast-vm VMs
    - **required by:** *config_fastvm_conf*
    ```
    fastvm_vm_prefix: 'fastvm-'
    ```

  - fast-vm notes directory - here fast-vm stores VM notes and other VM stateful details
    - **required by:** *config_fastvm_conf*
    ```
    fastvm_notes_dir: '/var/tmp'
    ```

  - Allow only owners of VMs and 'root' to delete them
    - **required by:** *config_fastvm_conf*
    ```
    fastvm_owner_only_delete: 'yes'
    ```

Example Playbook
----------------

Install and configure all basic things needed by fast-vm - default installation:

    - hosts: servers
      roles:
         - { role: OndrejHome.fast-vm-server }

License
-------

GPLv3

Author Information
------------------

To get in touch with author you can use email ondrej-xa2iel8u@famera.cz or create a issue on github when requesting feature(s).
