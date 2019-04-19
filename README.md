# Copyright
Copyright (c) 2018 Alessandro Lima alessandrolima1987@gmail.com

# About
QoS-Flux is a management of dynamic traffic control algorithms to provide quality of service in SDN in different flows (elephants vs. mice, alpha vs. beta and Cheetah vs. snails) on one or more switches in an SDN network. It does this by invoking the iproute tc command automatically. 

The script was developed in the Shell Script language based on the SuperShaper-SOHO 2.0 project and Wonder Shaper 1.4. This script has the perspective of improving SDN (Software Defined Network) networks in relation to packet loss, delay, jitter and bandwidth in different streams.

To run this script, you will need iproute2 (tc) and the Linux kernel netfilter installed. The howto of the TC filter can be found here: http://lartc.org/howto/lartc.qdisc.filters.html.

The Man page of the u32 classifier can be found here: http://man7.org/linux/man-pages/man8/tc-u32.8.html.

# Instructions
 
The following instructions are designed to work in an Ubuntu 16.04. It should work in other linux OS with the correct packages installed.

# Requirements

- Iproute2 (tc command)

- Linux kernel with support for HFSC and fq_codel schedulers (3.6 should work, but use 3.12 or later for better performance).

- Mininet Network Emulator

- Openvswitch-switch.

- Ryu SDN Controller 

Ubuntu 16.04 was used for testing. However, qos-flux can be configured on any system based on Debian or Ubuntu.

# Installation

1) Installation Qos-Flux:

Modify the variables on top of QoS-flux.init and copy this file to /etc/init.d/QoS-flux. Make sure that the file has executable bits set. Then make sure it starts up automatically at startup.

On Ubuntu/Debian this is usually done like this:

$ sudo cp qoS-flux.init /etc/init.d/qos-flux

$ sudo chown root:root /etc/init.d/qos-flux

$ sudo chmod 0755 /etc/init.d/qos-flux

$ sudo update-rc.d qos-flux defaults

create the file qos-flux.csv in the root directory:

$ touch /root/qos-flux.csv

Another way to run QoS-Flux, can be done directly in the root folder, where the download was done. We should add QoS-Flux.init as executable and then select the standard start, stop, filter, or status commands inside the Linux terminal under root.

$ sudo ./QoS-Flux start

$ sudo ./QoS-Flux stop

$ sudo ./QoS-Flux filter

$ sudo ./QoS-Flux status

2) Configuration of the Ryu SDN controller (taken from the Ryubook 1.0 manual):

- Start in Ryu controller

ryu-manager ryu.app.simple_switch_13 ryu.app.rest_conf_switch

3) Configuration of the Mininet:

In the mininet we used in the tests a topology with 4 switches (an aggregation switch and 3 edge switches) as well as 9 hosts. In addition, we configured a topology with Openflow v1.3 and a network with 1 GBit of bandwidth, as we can see in the command below:

mn --topo tree,depth=2,fanout=3 --switch ovsk --controller=remote, ip=10.2.0.15,protocols=OpenFlow13 --link tc,bw=1000

# Support

If you require support for this product or have other contracting assignments, please contact the author directly via email.

