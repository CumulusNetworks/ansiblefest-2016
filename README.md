# ansiblefest-2016
Playbooks for the Docker demo I did at AnsibleFest SF, July 2016

ROH directory contains the playbooks for launching routing on the host with dual-attached links and using docker bridge.

RedistARP directory contains the playbooks for launching docker with MacVlan driver and using redistribute neighbor to advertise container reachability.

Both playbooks assume a 2-tier CLOS with 2 spines and 4 leaves with 2 hosts per leaf.

If you want to modify the size of the network or hosts, modify all the appropriate parameters in properties.yml. Remember to adjust the port numbers as well.

Launch the playbooks via: ansible-playbook -s configure.yml
