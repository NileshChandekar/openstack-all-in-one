# openstack-architecture 


                                                    |
                                                    | eth0 - Public IP (192.168.124.95) // Internet facing // Full internet access
                                                    |    
                                        +-----------+-----------+  
                                        |                       |
                                        |                       |
                                        |      Host_System      |   
                                        |                       |
                                        |     Openstack Env     |
                                        +-----------+-----------+  
                                       	            | 
                                                  Nating 
                                                    |       
                    +--------------------------------+--------------------------+
                    |                                                           |                            
                    |                                                           |
                    |  eth0-10.0.0.20 (Private-Net-IP) 				| eth0- 10.0.0.30 (Private-Net-IP)
                    |	    192.168.124.0 (Floating-IP)		          	|	192.168.124.0 (Floating-IP)		
         +----------+-----------+                                   +-----------+-----------+                                  
         |                       |                                  |                       |
         |                       |                                  |                       |
         |        VM-1           |                                  |          VM-2         |
         |                       |                                  |                       |
         |                       |                                  |                       |
         +----------+-----------+                                   +-----------+-----------+ 




### openstack-commands
 
#### source the rc file

    [root@pike ~]# source keystonerc_admin 
    [root@pike ~(keystone_admin)]# 

##### To list openstack user

    [root@pike ~(keystone_admin)]# openstack user list 
    +----------------------------------+------------+
    | ID                               | Name       |
    +----------------------------------+------------+
    | 0004f1ea0d6146ef9859f9387c523263 | ceilometer |
    | 0815c16f10f6470da42f52be8cfb19b1 | glance     |
    | 12238daf801246158eac155ebcdad999 | nova       |
    | 1a45d0d80f854f91af6a3e9863fd4873 | placement  |
    | 1e98d09bfd1046c7a8124ba32c6b6026 | cinder     |
    | 2227af0e15a14ee1942e14f4f2bee00e | admin      |
    | 32eb7328ccee461cbd1d55c01a6cd847 | gnocchi    |
    | 98817bb743c042198532c9d468cabddc | swift      |
    | 9f126202472644aeafc2448348b1a7a9 | neutron    |
    | b8909452ac9d4141a41bb42129b50952 | aodh       |
    +----------------------------------+------------+
    [root@pike ~(keystone_admin)]# 

#### To list all project 

    [root@pike ~(keystone_admin)]# openstack project list
    +----------------------------------+----------+
    | ID                               | Name     |
    +----------------------------------+----------+
    | 288724188705444e87e7ccc181a1d44a | services |
    | 4b4325a4389b4130acd2539eab299567 | admin    |
    +----------------------------------+----------+
    [root@pike ~(keystone_admin)]# 

#### To list all services 

    [root@pike ~(keystone_admin)]# openstack service list
    +----------------------------------+------------+--------------+
    | ID                               | Name       | Type         |
    +----------------------------------+------------+--------------+
    | 0e1c480877634e64b240b988a2717243 | cinderv2   | volumev2     |
    | 136dc9508cd04c7781265d2977c4fc95 | ceilometer | metering     |
    | 48ead0ca5a7f421e9eb31b0ab9670fd9 | cinder     | volume       |
    | 4eade89e6851419f9a6e70ac45b16f78 | neutron    | network      |
    | 7f89ee93d6e349ec9733fbeb266f647e | cinderv3   | volumev3     |
    | 9e91670775cd4767ab34db95e9d72fba | gnocchi    | metric       |
    | c7ec286062e54d8685a8cbbdc80418ce | placement  | placement    |
    | ce22947a9c464fc686b7f51c21ce958b | nova       | compute      |
    | d1cfaa760d874989825e6bb539f7dc7d | glance     | image        |
    | d9d2e94554ed4032976978cde242cd64 | keystone   | identity     |
    | da45bca0838d49a4a083fe9dbbb75226 | aodh       | alarming     |
    | fcbfb3080cdd413a83715c425f1acfaa | swift      | object-store |
    +----------------------------------+------------+--------------+
    [root@pike ~(keystone_admin)]# 


#### To list all endpoints

    [root@pike ~(keystone_admin)]# openstack catalog list
    +------------+--------------+---------------------------------------------------------------------------------+
    | Name       | Type         | Endpoints                                                                       |
    +------------+--------------+---------------------------------------------------------------------------------+
    | cinderv2   | volumev2     | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:8776/v2/4b4325a4389b4130acd2539eab299567         |
    |            |              | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:8776/v2/4b4325a4389b4130acd2539eab299567      |
    |            |              | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:8776/v2/4b4325a4389b4130acd2539eab299567        |
    |            |              |                                                                                 |
    | ceilometer | metering     | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:8777                                             |
    |            |              | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:8777                                            |
    |            |              | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:8777                                          |
    |            |              |                                                                                 |
    | cinder     | volume       | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:8776/v1/4b4325a4389b4130acd2539eab299567         |
    |            |              | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:8776/v1/4b4325a4389b4130acd2539eab299567        |
    |            |              | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:8776/v1/4b4325a4389b4130acd2539eab299567      |
    |            |              |                                                                                 |
    | neutron    | network      | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:9696                                          |
    |            |              | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:9696                                            |
    |            |              | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:9696                                             |
    |            |              |                                                                                 |
    | cinderv3   | volumev3     | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:8776/v3/4b4325a4389b4130acd2539eab299567      |
    |            |              | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:8776/v3/4b4325a4389b4130acd2539eab299567        |
    |            |              | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:8776/v3/4b4325a4389b4130acd2539eab299567         |
    |            |              |                                                                                 |
    | gnocchi    | metric       | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:8041                                             |
    |            |              | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:8041                                            |
    |            |              | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:8041                                          |
    |            |              |                                                                                 |
    | placement  | placement    | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:8778/placement                                  |
    |            |              | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:8778/placement                                |
    |            |              | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:8778/placement                                   |
    |            |              |                                                                                 |
    | nova       | compute      | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:8774/v2.1/4b4325a4389b4130acd2539eab299567      |
    |            |              | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:8774/v2.1/4b4325a4389b4130acd2539eab299567       |
    |            |              | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:8774/v2.1/4b4325a4389b4130acd2539eab299567    |
    |            |              |                                                                                 |
    | glance     | image        | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:9292                                            |
    |            |              | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:9292                                             |
    |            |              | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:9292                                          |
    |            |              |                                                                                 |
    | keystone   | identity     | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:35357/v3                                         |
    |            |              | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:5000/v3                                         |
    |            |              | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:5000/v3                                       |
    |            |              |                                                                                 |
    | aodh       | alarming     | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:8042                                             |
    |            |              | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:8042                                            |
    |            |              | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:8042                                          |
    |            |              |                                                                                 |
    | swift      | object-store | RegionOne                                                                       |
    |            |              |   admin: http://192.168.124.95:8080/v1/AUTH_4b4325a4389b4130acd2539eab299567    |
    |            |              | RegionOne                                                                       |
    |            |              |   internal: http://192.168.124.95:8080/v1/AUTH_4b4325a4389b4130acd2539eab299567 |
    |            |              | RegionOne                                                                       |
    |            |              |   public: http://192.168.124.95:8080/v1/AUTH_4b4325a4389b4130acd2539eab299567   |
    |            |              |                                                                                 |
    +------------+--------------+---------------------------------------------------------------------------------+
    [root@pike ~(keystone_admin)]# 


#### To create private network 

    [root@pike ~(keystone_admin)]# openstack network create private
    +---------------------------+--------------------------------------+
    | Field                     | Value                                |
    +---------------------------+--------------------------------------+
    | admin_state_up            | UP                                   |
    | availability_zone_hints   |                                      |
    | availability_zones        |                                      |
    | created_at                | 2018-01-26T14:43:07Z                 |
    | description               |                                      |
    | dns_domain                | None                                 |
    | id                        | 3fbbc901-3a5f-46ee-91ba-6326a426a79f |
    | ipv4_address_scope        | None                                 |
    | ipv6_address_scope        | None                                 |
    | is_default                | False                                |
    | is_vlan_transparent       | None                                 |
    | mtu                       | 1450                                 |
    | name                      | private                              |
    | port_security_enabled     | True                                 |
    | project_id                | 4b4325a4389b4130acd2539eab299567     |
    | provider:network_type     | vxlan                                |
    | provider:physical_network | None                                 |
    | provider:segmentation_id  | 59                                   |
    | qos_policy_id             | None                                 |
    | revision_number           | 2                                    |
    | router:external           | Internal                             |
    | segments                  | None                                 |
    | shared                    | False                                |
    | status                    | ACTIVE                               |
    | subnets                   |                                      |
    | tags                      |                                      |
    | updated_at                | 2018-01-26T14:43:07Z                 |
    +---------------------------+--------------------------------------+
    [root@pike ~(keystone_admin)]# 


#### To list all network 

    [root@pike ~(keystone_admin)]# openstack network list
    +--------------------------------------+---------+---------+
    | ID                                   | Name    | Subnets |
    +--------------------------------------+---------+---------+
    | 3fbbc901-3a5f-46ee-91ba-6326a426a79f | private |         |
    +--------------------------------------+---------+---------+
    [root@pike ~(keystone_admin)]# 

#### To create private subnet 

    [root@pike ~(keystone_admin)]# neutron subnet-create --name subpriv private 10.10.10.0/24
    +-------------------+------------------------------------------------+
    | Field             | Value                                          |
    +-------------------+------------------------------------------------+
    | allocation_pools  | {"start": "10.10.10.2", "end": "10.10.10.254"} |
    | cidr              | 10.10.10.0/24                                  |
    | created_at        | 2018-01-26T14:44:35Z                           |
    | description       |                                                |
    | dns_nameservers   |                                                |
    | enable_dhcp       | True                                           |
    | gateway_ip        | 10.10.10.1                                     |
    | host_routes       |                                                |
    | id                | 81a69f6c-34c4-4f14-8d43-4b9cd6977548           |
    | ip_version        | 4                                              |
    | ipv6_address_mode |                                                |
    | ipv6_ra_mode      |                                                |
    | name              | subpriv                                        |
    | network_id        | 3fbbc901-3a5f-46ee-91ba-6326a426a79f           |
    | project_id        | 4b4325a4389b4130acd2539eab299567               |
    | revision_number   | 0                                              |
    | service_types     |                                                |
    | subnetpool_id     |                                                |
    | tags              |                                                |
    | tenant_id         | 4b4325a4389b4130acd2539eab299567               |
    | updated_at        | 2018-01-26T14:44:35Z                           |
    +-------------------+------------------------------------------------+


#### To list subnet

    [root@pike ~(keystone_admin)]# neutron subnet-list
    +--------------------------------------+---------+----------------------------------+---------------+------------------------------------------------+
    | id                                   | name    | tenant_id                        | cidr          | allocation_pools                               |
    +--------------------------------------+---------+----------------------------------+---------------+------------------------------------------------+
    | 81a69f6c-34c4-4f14-8d43-4b9cd6977548 | subpriv | 4b4325a4389b4130acd2539eab299567 | 10.10.10.0/24 | {"start": "10.10.10.2", "end": "10.10.10.254"} |
    +--------------------------------------+---------+----------------------------------+---------------+------------------------------------------------+
    [root@pike ~(keystone_admin)]# 

#### To cretae router

    [root@pike ~(keystone_admin)]# neutron router-create router1
    +-------------------------+--------------------------------------+
    | Field                   | Value                                |
    +-------------------------+--------------------------------------+
    | admin_state_up          | True                                 |
    | availability_zone_hints |                                      |
    | availability_zones      |                                      |
    | created_at              | 2018-01-26T14:48:48Z                 |
    | description             |                                      |
    | distributed             | False                                |
    | external_gateway_info   |                                      |
    | flavor_id               |                                      |
    | ha                      | False                                |
    | id                      | de6d0c7d-8421-4844-b5e0-289c8a1c848f |
    | name                    | router1                              |
    | project_id              | 4b4325a4389b4130acd2539eab299567     |
    | revision_number         | 1                                    |
    | routes                  |                                      |
    | status                  | ACTIVE                               |
    | tags                    |                                      |
    | tenant_id               | 4b4325a4389b4130acd2539eab299567     |
    | updated_at              | 2018-01-26T14:48:48Z                 |
    +-------------------------+--------------------------------------+

#### To attach private subnet to router

    [root@pike ~(keystone_admin)]# neutron router-interface-add router1 subpriv
    Added interface 9814c909-8c85-44f1-8819-2c9719a50730 to router router1.
    [root@pike ~(keystone_admin)]# 

#### To create public network 

    [root@pike ~(keystone_admin)]# openstack network create public
    +---------------------------+--------------------------------------+
    | Field                     | Value                                |
    +---------------------------+--------------------------------------+
    | admin_state_up            | UP                                   |
    | availability_zone_hints   |                                      |
    | availability_zones        |                                      |
    | created_at                | 2018-01-26T14:49:40Z                 |
    | description               |                                      |
    | dns_domain                | None                                 |
    | id                        | a8be8e5c-a0ee-4892-835e-8e0fb6ce6e63 |
    | ipv4_address_scope        | None                                 |
    | ipv6_address_scope        | None                                 |
    | is_default                | False                                |
    | is_vlan_transparent       | None                                 |
    | mtu                       | 1450                                 |
    | name                      | public                               |
    | port_security_enabled     | True                                 |
    | project_id                | 4b4325a4389b4130acd2539eab299567     |
    | provider:network_type     | vxlan                                |
    | provider:physical_network | None                                 |
    | provider:segmentation_id  | 92                                   |
    | qos_policy_id             | None                                 |
    | revision_number           | 2                                    |
    | router:external           | Internal                             |
    | segments                  | None                                 |
    | shared                    | False                                |
    | status                    | ACTIVE                               |
    | subnets                   |                                      |
    | tags                      |                                      |
    | updated_at                | 2018-01-26T14:49:40Z                 |
    +---------------------------+--------------------------------------+
    [root@pike ~(keystone_admin)]# 
 
