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
<<<<<<< HEAD
                                        		    | 
                                                  Nating 
=======
<<<<<<< HEAD
                                       		    | 
                                                 Nating 
=======
                                        		        | 
                                                  Nating 
>>>>>>> 6c541f1e00155c3a4dd59dd5bb6c6fc2611b3f49
>>>>>>> bc361c3cbce490ead34bfe21af00a276b5acaa48
                                                    |       
                    +--------------------------------+--------------------------+
                    |                                                           |                            
                    |                                                           |
                    |  eth0-10.0.0.20 (Private-Net-IP) 				| eth0- 10.0.0.30 (Private-Net-IP)
                    |	    192.168.124.0 (Floating-IP)		          	|	192.168.124.0 (Floating-IP)		
         +-----------+-----------+                                  +-----------+-----------+                                  
         |                       |                                  |                       |
         |                       |                                  |                       |
         |        VM-1           |                                  |          VM-2         |
         |                       |                                  |                       |
         |                       |                                  |                       |
         +-----------+-----------+                                  +-----------+-----------+ 


