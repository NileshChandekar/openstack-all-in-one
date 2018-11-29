# Nova commands

## list Nova instances
```
(overcloud) [stack@undercloud-0 ~]$ openstack server list 
+--------------------------------------+-------+--------+------------+-------------+------------------------------+ 
| ID                                   | Name  | Status | Task State | Power State | Networks                     | 
+--------------------------------------+-------+--------+------------+-------------+------------------------------+ 
| 291350a2-336b-4131-8d0e-38cabf18b5af | inst1 | ACTIVE | -          | Running     | private=172.0.0.10, 10.0.0.3 | 
+--------------------------------------+-------+--------+------------+-------------+------------------------------+ 
```

## Create Nova instances
```
(overcloud) [stack@undercloud-0 ~]$ openstack server create --image cirros --flavor small  \
 --nic net-id=private --security-group sec1 --key-name demo-key instance10
+-------------------------------------+-----------------------------------------------+
| Field                               | Value                                         |
+-------------------------------------+-----------------------------------------------+
| OS-DCF:diskConfig                   | MANUAL                                        |
| OS-EXT-AZ:availability_zone         |                                               |
| OS-EXT-SRV-ATTR:host                | None                                          |
| OS-EXT-SRV-ATTR:hypervisor_hostname | None                                          |
| OS-EXT-SRV-ATTR:instance_name       |                                               |
| OS-EXT-STS:power_state              | NOSTATE                                       |
| OS-EXT-STS:task_state               | scheduling                                    |
| OS-EXT-STS:vm_state                 | building                                      |
| OS-SRV-USG:launched_at              | None                                          |
| OS-SRV-USG:terminated_at            | None                                          |
| accessIPv4                          |                                               |
| accessIPv6                          |                                               |
| addresses                           |                                               |
| adminPass                           | ymzDxb4YhaRC                                  |
| config_drive                        |                                               |
| created                             | 2018-10-19T14:19:05Z                          |
| flavor                              | small (cdb97fcc-1bda-4999-9afb-ec0be72c993e)  |
| hostId                              |                                               |
| id                                  | 4ac54216-709d-4236-b63b-ac6ee18775f5          |
| image                               | cirros (4609bfef-e2e1-4ff9-9d3f-174ff600dee8) |
| key_name                            | demo-key                                      |
| name                                | instance10                                    |
| progress                            | 0                                             |
| project_id                          | 8236420e23884127b8dc976897d4ee49              |
| properties                          |                                               |
| security_groups                     | name='7cec06b5-9f4e-4286-ae8e-4b40235fb0c8'   |
| status                              | BUILD                                         |
| updated                             | 2018-10-19T14:19:05Z                          |
| user_id                             | 2f4be5059b374d609fb85f817e27ee84              |
| volumes_attached                    |                                               |
+-------------------------------------+-----------------------------------------------+
```
## Get instance information 
```
(overcloud) [stack@undercloud-0 ~]$ openstack server show instance10
+-------------------------------------+----------------------------------------------------------+
| Field                               | Value                                                    |
+-------------------------------------+----------------------------------------------------------+
| OS-DCF:diskConfig                   | MANUAL                                                   |
| OS-EXT-AZ:availability_zone         | nova                                                     |
| OS-EXT-SRV-ATTR:host                | compute-0.localdomain                                    |
| OS-EXT-SRV-ATTR:hypervisor_hostname | compute-0.localdomain                                    |
| OS-EXT-SRV-ATTR:instance_name       | instance-0000001d                                        |
| OS-EXT-STS:power_state              | Running                                                  |
| OS-EXT-STS:task_state               | None                                                     |
| OS-EXT-STS:vm_state                 | active                                                   |
| OS-SRV-USG:launched_at              | 2018-10-19T14:19:14.000000                               |
| OS-SRV-USG:terminated_at            | None                                                     |
| accessIPv4                          |                                                          |
| accessIPv6                          |                                                          |
| addresses                           | private=172.0.0.8                                        |
| config_drive                        |                                                          |
| created                             | 2018-10-19T14:19:05Z                                     |
| flavor                              | small (cdb97fcc-1bda-4999-9afb-ec0be72c993e)             |
| hostId                              | 01f0d67c24c50ca129bf2ec2e4976fb6ac19622677b086999c65a132 |
| id                                  | 4ac54216-709d-4236-b63b-ac6ee18775f5                     |
| image                               | cirros (4609bfef-e2e1-4ff9-9d3f-174ff600dee8)            |
| key_name                            | demo-key                                                 |
| name                                | instance10                                               |
| progress                            | 0                                                        |
| project_id                          | 8236420e23884127b8dc976897d4ee49                         |
| properties                          |                                                          |
| security_groups                     | name='sec1'                                              |
| status                              | ACTIVE                                                   |
| updated                             | 2018-10-19T14:19:14Z                                     |
| user_id                             | 2f4be5059b374d609fb85f817e27ee84                         |
| volumes_attached                    |                                                          |
+-------------------------------------+----------------------------------------------------------+
```

## Nova Resize
```
(overcloud) [stack@undercloud-0 ~]$ openstack server list
+--------------------------------------+------------+--------+------------------------------+--------+--------+
| ID                                   | Name       | Status | Networks                     | Image  | Flavor |
+--------------------------------------+------------+--------+------------------------------+--------+--------+
| 4ac54216-709d-4236-b63b-ac6ee18775f5 | instance10 | ACTIVE | private=172.0.0.8            | cirros | small  |
| 291350a2-336b-4131-8d0e-38cabf18b5af | inst1      | ACTIVE | private=172.0.0.10, 10.0.0.3 | cirros | small  |
+--------------------------------------+------------+--------+------------------------------+--------+--------+
```
Instance10 is running and has a flavor small.
```
(overcloud) [stack@undercloud-0 ~]$ openstack flavor list
+--------------------------------------+-------------+-----+------+-----------+-------+-----------+
| ID                                   | Name        | RAM | Disk | Ephemeral | VCPUs | Is Public |
+--------------------------------------+-------------+-----+------+-----------+-------+-----------+
| 63caba6a-2e1f-469b-ae3a-8c7f2504d812 | m1-tiny     | 512 |   10 |         0 |     1 | True      |
| b0018a6c-582a-4a34-85c0-4feebae9e912 | micro       | 100 |    1 |         0 |     1 | True      |
| cdb97fcc-1bda-4999-9afb-ec0be72c993e | small       | 300 |    1 |         0 |     1 | True      |
+--------------------------------------+-------------+-----+------+-----------+-------+-----------+
```
Create a new flavor to which you want to resize. Micro flavor is created for resize.
```
(overcloud) [stack@undercloud-0 ~]$ nova resize instance10 micro
(overcloud) [stack@undercloud-0 ~]$ openstack server list
+--------------------------------------+------------+--------+------------------------------+--------+--------+
| ID                                   | Name       | Status | Networks                     | Image  | Flavor |
+--------------------------------------+------------+--------+------------------------------+--------+--------+
| 4ac54216-709d-4236-b63b-ac6ee18775f5 | instance10 | RESIZE | private=172.0.0.8            | cirros | small  |
| 291350a2-336b-4131-8d0e-38cabf18b5af | inst1      | ACTIVE | private=172.0.0.10, 10.0.0.3 | cirros | small  |
+--------------------------------------+------------+--------+------------------------------+--------+--------+
```
After executing nova resize, instance status switch to RESIZE.
```
(overcloud) [stack@undercloud-0 ~]$ openstack server list
+--------------------------------------+------------+---------------+------------------------------+--------+--------+
| ID                                   | Name       | Status        | Networks                     | Image  | Flavor |
+--------------------------------------+------------+---------------+------------------------------+--------+--------+
| 4ac54216-709d-4236-b63b-ac6ee18775f5 | instance10 | VERIFY_RESIZE | private=172.0.0.8            | cirros | micro  |
| 291350a2-336b-4131-8d0e-38cabf18b5af | inst1      | ACTIVE        | private=172.0.0.10, 10.0.0.3 | cirros | small  |
+--------------------------------------+------------+---------------+------------------------------+--------+--------+
```
After some time notice instance status switch to VERIFY_RESIZE.
```
(overcloud) [stack@undercloud-0 ~]$ nova resize-confirm instance10
(overcloud) [stack@undercloud-0 ~]$ openstack server list
+--------------------------------------+------------+--------+------------------------------+--------+--------+
| ID                                   | Name       | Status | Networks                     | Image  | Flavor |
+--------------------------------------+------------+--------+------------------------------+--------+--------+
| 4ac54216-709d-4236-b63b-ac6ee18775f5 | instance10 | ACTIVE | private=172.0.0.8            | cirros | micro  |
| 291350a2-336b-4131-8d0e-38cabf18b5af | inst1      | ACTIVE | private=172.0.0.10, 10.0.0.3 | cirros | small  |
+--------------------------------------+------------+--------+------------------------------+--------+--------+
```
To verify resize execute nova resize_confirm and instance will come to active state with new flavor.

## Nova Snapshot

```
(overcloud) [stack@undercloud-0 ~]$ openstack server backup create --name snap1 instance10
+------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Field            | Value                                                                                                                                                                                                                                                                 |
+------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| checksum         | None                                                                                                                                                                                                                                                                  |
| container_format | bare                                                                                                                                                                                                                                                                  |
| created_at       | 2018-10-20T08:30:03Z                                                                                                                                                                                                                                                  |
| disk_format      | qcow2                                                                                                                                                                                                                                                                 |
| file             | /v2/images/49cab764-574b-4d74-91dc-d357af41de7a/file                                                                                                                                                                                                                  |
| id               | 49cab764-574b-4d74-91dc-d357af41de7a                                                                                                                                                                                                                                  |
| min_disk         | 1                                                                                                                                                                                                                                                                     |
| min_ram          | 0                                                                                                                                                                                                                                                                     |
| name             | snap1                                                                                                                                                                                                                                                                 |
| owner            | 8236420e23884127b8dc976897d4ee49                                                                                                                                                                                                                                      |
| properties       | backup_type='', base_image_ref='4609bfef-e2e1-4ff9-9d3f-174ff600dee8', boot_roles='admin', image_type='backup', instance_uuid='4ac54216-709d-4236-b63b-ac6ee18775f5', owner_project_name='admin', owner_user_name='admin', user_id='2f4be5059b374d609fb85f817e27ee84' |
| protected        | False                                                                                                                                                                                                                                                                 |
| schema           | /v2/schemas/image                                                                                                                                                                                                                                                     |
| size             | None                                                                                                                                                                                                                                                                  |
| status           | queued                                                                                                                                                                                                                                                                |
| tags             |                                                                                                                                                                                                                                                                       |
| updated_at       | 2018-10-20T08:30:03Z                                                                                                                                                                                                                                                  |
| virtual_size     | None                                                                                                                                                                                                                                                                  |
| visibility       | private                                                                                                                                                                                                                                                               |
+------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```
To verify snapshot creation, check images list
```
(overcloud) [stack@undercloud-0 ~]$ openstack image list
+--------------------------------------+------------+--------+
| ID                                   | Name       | Status |
+--------------------------------------+------------+--------+
| 4609bfef-e2e1-4ff9-9d3f-174ff600dee8 | cirros     | active |
| 21cb1227-7cad-4ab8-b1b6-49a6f82bd398 | rhel7      | active |
| dc29de08-b711-4f8f-b965-02af65f4f2a7 | snap-inst1 | active |
| 49cab764-574b-4d74-91dc-d357af41de7a | snap1      | active |
+--------------------------------------+------------+--------+
```


### Enable - Disable Hypervisor 

~~~
[stack@undercloud-0 ~]$ nova hypervisor-list
~~~

```
+----+-----------------------+-------+---------+
| ID | Hypervisor hostname   | State | Status  |
+----+-----------------------+-------+---------+
| 1  | compute-0.localdomain | up    | enabled |
+----+-----------------------+-------+---------+
[stack@undercloud-0 ~]$ 
```

~~~
[stack@undercloud-0 ~]$ nova service-disable compute-0.localdomain nova-compute
~~~

```
+-----------------------+--------------+----------+
| Host                  | Binary       | Status   |
+-----------------------+--------------+----------+
| compute-0.localdomain | nova-compute | disabled |
+-----------------------+--------------+----------+
[stack@undercloud-0 ~]$ 
```

~~~
[stack@undercloud-0 ~]$ nova service-enable compute-0.localdomain nova-compute
~~~

```
+-----------------------+--------------+---------+
| Host                  | Binary       | Status  |
+-----------------------+--------------+---------+
| compute-0.localdomain | nova-compute | enabled |
+-----------------------+--------------+---------+
[stack@undercloud-0 ~]$ 
```


