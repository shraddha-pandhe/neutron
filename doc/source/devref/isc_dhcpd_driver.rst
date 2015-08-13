=======================================
ISC-DHCPD Driver for Neutron DHCP Agent
=======================================

Currently, Neutron's dhcp agent only supports Dnsmasq. Dnsmasq has
a very serious limitation that, it needs a reload any time when
hosts, opts or addn hosts configs are updated. According to this
`Dnsmasq performance blog
<https://www.mirantis.com/blog/improving-dhcp-performance-openstack/>`_
, this can take unto 4 minutes with 65535 static leases.

When we consider use-cases like Baremetal Deployments (Ironic),
where thousands of baremetal nodes may need to be booted at a time,
Dnsmasq poses serious scaling limitations. Things get even worse
when a cloud provider wants their DHCP Server to handle all the
networks in the datacenter (traditional use-case), as against
having separate DHCP Server per network.

Typical industry standard is to use `ISC-DHCPD
<https://www.isc.org/downloads/dhcp/>`_ instead of Dnsmasq.
In general ISC-DHCPD has lot more features than Dnsmasq.
It also supports OMAPI, which allows creating/deleting and updating
host or lease objects runtime. There are two ways to use OMAPI: `omshell
<http://linux.die.net/man/1/omshell>`_ and `PyPureOmapi python library
<https://github.com/CygnusNetworks/pypureomapi>`_

With OMAPI, its very easy to selectively add/delete a host/lease
from configuration (as against updating full config on every
create/update port)

Considering that most of the industry uses isc-dhcpd,
this will be a great addition to OpenStack neutron.
