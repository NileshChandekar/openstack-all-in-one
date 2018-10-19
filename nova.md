# Nova commands

## list Nova instances

(overcloud) [stack@undercloud-0 ~]$ openstack server list
+--------------------------------------+-------+--------+------------+-------------+------------------------------+
| ID                                   | Name  | Status | Task State | Power State | Networks                     |
+--------------------------------------+-------+--------+------------+-------------+------------------------------+
| 291350a2-336b-4131-8d0e-38cabf18b5af | inst1 | ACTIVE | -          | Running     | private=172.0.0.10, 10.0.0.3 |
+--------------------------------------+-------+--------+------------+-------------+------------------------------+

## Create Nova instances

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

## Get instance information 

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


