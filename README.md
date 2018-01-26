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




# openstack-commands


    [root@pike ~]# source keystonerc_admin 
    [root@pike ~(keystone_admin)]# 


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


