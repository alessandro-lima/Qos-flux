# Qos-flux
Traffic Shaping rules for SDN

Dynamic traffic shaping for SDN in different flows (elephants vs. mice, alpha vs. beta and Cheetah vs. turtles).


 Instructions
 
The following instructions are designed to work in an Ubuntu 16.04. It should work in other linux OS with the correct packages installed.

# Requirements

Iproute2 (tc command)

Linux kernel with support for HFSC and fq_codel schedulers (3.6 should work, but use 3.12 or later for best performance)

Mininet Network Emulator

Openvswitch-switch.

Ryu SDN Controller 

Ubuntu 16.04 is known to work and is the author's primary development platform.

# Installation

Modify the variables on top of QoS-flux.init and copy this file to /etc/init.d/QoS-flux. Make sure that the file has executable bits set. Then make sure it starts up automatically at startup.

On Ubuntu this is usually done like this:

$ sudo cp qoS-flux.init /etc/init.d/qos-flux

$ sudo chown root:root /etc/init.d/qos-flux

$ sudo chmod 0755 /etc/init.d/qos-flux

$ sudo update-rc.d qos-flux defaults

# Support

If you require support for this product or have other contracting assignments, please contact the author directly via email.

# Author, copyright and license

See the main script and the file LICENSE for details.
