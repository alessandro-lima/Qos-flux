# Qos-flux
Traffic Shaping rules for SDN

Dynamic traffic shaping for SDN in different flows (elephants vs. mice, alpha vs. beta and Cheetah vs. snails).


# Instructions
 
The following instructions are designed to work in an Ubuntu 16.04. It should work in other linux OS with the correct packages installed.

# Requirements

- Iproute2 (tc command)

- Linux kernel with support for HFSC and fq_codel schedulers (3.6 should work, but use 3.12 or later for better performance). If your Linux operating system is older, enable the SFQ algorithm in the qos-flux.init script.

- Mininet Network Emulator

- Openvswitch-switch.

- Ryu SDN Controller 

Ubuntu 16.04 was used for testing. However, qos-flux can be configured on any system based on Debian or Ubuntu.

# Installation

1) Installation Qos-Flux 

Modify the variables on top of QoS-flux.init and copy this file to /etc/init.d/QoS-flux. Make sure that the file has executable bits set. Then make sure it starts up automatically at startup.

On Ubuntu this is usually done like this:

$ sudo cp qoS-flux.init /etc/init.d/qos-flux

$ sudo chown root:root /etc/init.d/qos-flux

$ sudo chmod 0755 /etc/init.d/qos-flux

$ sudo update-rc.d qos-flux defaults

2) Configuration of the Ryu SDN controller (Taken from the Ryubook 1.0 manual)

- Modify the file "simple_switch_13.py" in the "~/ryu/ryu/app/simple_switch_13.py" folder, considering the user "ryu" in Linux as root. After this procedure, exit the ryu folder and run the build.

sudo su sed '/OFPFlowMod(/,/)/s/)/, table_id=1)/' ryu/ryu/app/simple_switch_13.py > ryu/ryu/app/qos_simple_switch_13.py

cd ryu/; 

python ./setup.py install

- Start rest_qos, qos_simple_switch_13 and rest_conf_switch on terminal Linux.

ryu-manager ryu.app.rest_qos ryu.app.qos_simple_switch_13 ryu.app.rest_conf_switch

3) Configuration of the Mininet

In the mininet we used in the tests a topology with 4 switches (an aggregation switch and 3 edge switches) as well as 9 hosts. In addition, we configured a topology with Openflow v1.3 and a network with 1 GBit of bandwidth, as we can see in the command below:

mn --topo tree,depth=2,fanout=3 --switch ovsk --controller=remote, ip=10.1.1.1,protocols=OpenFlow13 --link tc,bw=1000

# Support

If you require support for this product or have other contracting assignments, please contact the author directly via email.

# Author, copyright and license

See the main script and the file LICENSE for details.
