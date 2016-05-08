.. _interfaces:

Netzwerk Interfaces
===================

/etc/network/interfaces

Hier richten wir hauptsachlich die GRE Tunnel zum FFRL ein.

.. seealso::
    :ref:`dhcp`
    :ref:`routing_tables`
    :ref:`policyrouting`
    :ref:`internetexit`
    :ref:`gre`

    # The loopback network interface
    auto lo
    iface lo inet loopback
            up ip address add 185.66.193.105/32 dev lo

    iface lo inet6 loopback
            up ip address add 2a03:2260:121::105/48 dev lo


    # The primary network interface
    allow-hotplug eth0
    iface eth0 inet dhcp
    allow-hotplug eth1
    iface eth1 inet6 static
            address 2a01:4f8:161:62a9::5
            netmask 64
            gateway 2a01:4f8:161:62a9::2

    # GRE Tunnel zum Rheinland Backbone
    # - Die Konfigurationsdaten werden vom Rheinland Backbone vergeben und zugewiesen

    # Berlin Router A
    auto gre-bb-a.ak.ber
    iface gre-bb-a.ak.ber inet static
            address 100.64.2.151
            netmask 255.255.255.254
            pre-up ip tunnel add $IFACE mode gre local 5.9.76.198 remote 185.66.195.0 ttl 255
            post-up ip link set $IFACE mtu 1400
            post-down ip tunnel del $IFACE

    iface gre-bb-a.ak.ber inet6 static
            address 2a03:2260:0:155::2/64
            netmask 64

    # Berlin Router B
    auto gre-bb-b.ak.ber
    iface gre-bb-b.ak.ber inet static
            address 100.64.2.153
            netmask 255.255.255.254
            pre-up ip tunnel add $IFACE mode gre local 5.9.76.198 remote 185.66.195.1 ttl 255
            post-up ip link set $IFACE mtu 1400
            post-down ip tunnel del $IFACE

    iface gre-bb-b.ak.ber inet6 static
            address 2a03:2260:0:156::2/64
            netmask 64


    # Duesseldorf Router A
    auto gre-bb-a.ix.dus
    iface gre-bb-a.ix.dus inet static
            address 100.64.2.155
            netmask 255.255.255.254
            pre-up ip tunnel add $IFACE mode gre local 5.9.76.198 remote 185.66.193.0 ttl 255
            post-up ip link set $IFACE mtu 1400
            post-down ip tunnel del $IFACE

    iface gre-bb-a.ix.dus inet6 static
            address 2a03:2260:0:157::2/64
            netmask 64


    # Duesseldorf Router B
    auto gre-bb-b.ix.dus
    iface gre-bb-b.ix.dus inet static
            address 100.64.2.157
            netmask 255.255.255.254
            pre-up ip tunnel add $IFACE mode gre local 5.9.76.198 remote 185.66.193.1 ttl 255
            post-up ip link set $IFACE mtu 1400
            post-down ip tunnel del $IFACE

    iface gre-bb-b.ix.dus inet6 static
            address 2a03:2260:0:158::2/64
            netmask 64


