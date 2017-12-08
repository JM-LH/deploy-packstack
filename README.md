# deploy-packstack
Scripts and Guides to make deploying Packstack Easier


# Deploy on Bare Metal 
# Prepping the Server
  # Prepping Interfaces
  
   # Creating Bond Interface, ready to be the connection for the external network
    
   In this Instance, the interfaces used are ens2f0 and ens2f1
   So the Bond config should look like this: 
    
    ifcfg-bond0:
        DEVICE=bond0
        DEVICETYPE=ovs
        TYPE=OVSPort
        OVS_BRIDGE=br-ex
        ONBOOT=yes
        IPADR=10.72.0.X
        BONDING_MASTER=yes
        BONDING_OPTS="mode=802.3ad"
        
        
   And changing the following line in ifcfg-ens2f0 and ifcfg-ens2f1
        BOOTPROTO="none"
        
   
   As well as adding: 
        ONBOOT=yes
        MASTER=bond0
        SLAVE=yes
   
   Then activate Bonding: 
   
        $ modprobe --first-time bonding
        
        $ ifup ifcfg-ens2f0 | ifup ifcfg-ens2f1
        
        
        
   Now deactivate Network Manager and Start Network Instead
   
        $ systemctl disable NetworkManager
        $ systemctl stop NetworkManager
        $ systemctl enable network
        $ systemctl start network
        
        
  # install packstsack files
  # Create Answer File
  
  
  
