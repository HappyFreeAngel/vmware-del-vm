Role Name
=========

vmware vsphere 自动删除虚拟机

Requirements
------------
vcenter6.0 以上版本

Role Variables
--------------
````  vmware_esxi:
        vcenterhostname: "yourhostname"      #vcenter.yourdomain.com 如果域名没有解析,在执行机器上设置hosts也可以
        vcenterusername: "administrator@vsphere.local"
        vcenterpassword: "yourpassword"
        datacenter: "hewutong"
        default_datastore: "cw_m4_sas_datastore"
        template: "centos1611_docker_jdk8_template"
        virtual_machine_template_disk_size_in_gb: 30
        resource_pool: "sparkcluster2"
        folder: "/vm"

#        vlan: "10.10.x.x"
#        gateway: "10.20.2.1"
#        netmask: "255.255.0.0"
        dnsserver1: "10.20.1.1"   #这个是create-dns-record.yml 里面要访问到的IP,也是dns-host[0].ip
        dnsserver2: "114.114.114.114"
        state: "poweredon"

        esxi_nic_network:
          vlan: "VM Network"      #"192.100.x.x"
          gateway: "10.20.0.1"  # sudo route  add -net 11.23.3.0 -netmask 255.255.255.128 11.23.3.1
          netmask: "255.255.0.0"
          dnsserver1: "10.20.1.1"
          dnsserver2: "114.114.114.114"

        datastore:
          rabbitmq_datastore: "cw_m4_sas_datastore"

      vmware_workstation:

      openstack:

      huawei_fusion_vsphere:

    deploy_vsphere_platform: "vmware_esxi"  #当前部署在什么平台上,  这个参数只能从上面参数获取
```
Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------
```
    - role: vmware-del-vm
      user_vcenterconfig: "{{ vcenterconfig }}"
      user_host_list: "{{ hostdict['spark-hosts'] }}"  #这个名称不能用appconfig,会冲突.
      async: 300
      poll: 0
      when: projectroot['deploy_vsphere_platform']=="vmware_esxi"
 #     when: inventory_hostname.find('spark')!=-1



```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
