# ansiblefest-2016
Playbooks for the Docker demo I did at AnsibleFest SF, July 2016.

ROH directory contains the playbooks for launching routing on the host with dual-attached links and using docker bridge. This pulls Cumulus' quagga container from docker repo and uses that to advertise routing from the host.

RedistARP directory contains the playbooks for launching docker with MacVlan driver and using redistribute neighbor to advertise container reachability. Hosts are single-attached as MacVlan binds to a single parent interface and using bonds involves running MLAG. Not that MLAG can't be done, but this was an attempt to build out a pure L3 solution.

Both playbooks assume a 2-tier CLOS with 2 spines and 4 leaves with 2 hosts per leaf.

If you want to modify the size of the network or hosts, modify all the appropriate parameters in properties.yml. Remember to adjust the port numbers as well.

=====================
Running the Playbooks
======================
* Spin up the VMs via 'vagrant up'
* Launch the playbook in each directory via: ansible-playbook -s RUNME.yml

You can then log into any of the hosts, say host-12, and spin up a container via:
  * docker run -it alpine /bin/sh (for ROH)
  * docker run --net=mv1 --ip=10.128.0.10 -it alpine /bin/sh (for RedustArp)

Log into some other host, say host-41, and spin up another container via:
 * docker run -it alpine /bin/sh (for ROH)
 * docker run --net=mv1 --ip=10.128.0.11 -it alpine /bin/sh (for RedustArp)

Log into one container and run ping the other container's IP address.


