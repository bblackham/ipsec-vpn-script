IPSec/L2TP script
=================

This script is a quick hack for bringing up an IPSec/L2TP-based VPN on Linux.
It has been tested on Ubuntu 12.04, but should work on other distributions.
It uses the in-kernel support for IPSec in 2.6 (no openswan patches required).

Installing
----------

There isn't much to install. Just drop the script somewhere of your choosing.

There are some dependencies. These are:
 * racoon
 * ipsec-tools (for setkey)
 * xl2tpd
 * iproute
 * a Linux kernel that supports IPSec

On Debian/Ubuntu systems, this will get the required dependencies:

  sudo apt-get install racoon ipsec-tools xl2tpd iproute

Running
-------

At present, the script only supports IPSec/L2TP tunnels with a pre-shared key.
Certificate-based setups are not support (though probably aren't difficult to
adapt for).

Modify vpn.cfg to suit your VPN. This file should be fairly descriptive.

To start the VPN, simply run

  $ sudo ipsec-vpn-connect vpn.cfg

This will print the output of racoon, xl2tpd and ppp (if debugging is enabled)
to stdout. The script will not return to the command prompt until the VPN is
terminated (e.g. with Ctrl-C, or some other signal).

Problems
--------

The first step to debugging problems is to set DEBUG=2 in your vpn.cfg file.
This should give a whole lot more information on what's going on in racoon and
pppd.  Now, whether or not you can make sense of it to fix it, is your problem.
You could pipe this to a file (append "| tee ipsec.log") and ask somebody for
help.

Good luck.

