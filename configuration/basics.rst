.. _basics:

Grundkonfiguration
==================

.. _hostname:

Hostname
--------

Den Hostnamen setzen (ohne Domain)::

    echo "hostname" > /etc/hostname

/etc/hosts (am Beispiel von troisdorf5)::

    127.0.0.1   localhost
    127.0.1.1   troisdorf5.freifunk-troisdorf.de    troisdorf5

    # The following lines are desirable for IPv6 capable hosts
    ::1     localhost ip6-localhost ip6-loopback
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters
    5.9.76.198 troisdorf5.freifunk-troisdorf.de troisdorf5
    2a01:4f8:161:62a9::5 troisdorf5.freifunk-troisdorf.de troisdorf5


.. _routing_tables:

Routing Tabellen
----------------

/etc/iproute2/rt_tables::

    #
    # reserved values
    #
    255 local
    254 main
    253 default
    0   unspec
    #
    # local
    #
    #1  inr.ruhep
    42 ffrl

.. _packages:

Pakete
------

Pakete aus den Standard-Repos installieren::

    apt-get install -y git make gcc build-essential pkg-config libgps-dev libnl-3-dev libjansson-dev isc-dhcp-server collectd libcap-dev iproute libnetfilter-conntrack3 python-dev libevent-dev ebtables python-virtualenv iptables-persistent iftop screen bridge-utils tcpdump bind9 radvd curl htop psmisc dnsutils ntp

.. _ntp:

NTP
---

Da die Kisten recht viel mit Crypto machen, ist es von Vorteil eine halbwegs genaue Uhrzeit parat zu haben.

Die ``/etc/ntp.conf`` bleibt nahezu unverändert::

    # /etc/ntp.conf, configuration for ntpd; see ntp.conf(5) for help

    driftfile /var/lib/ntp/ntp.drift

    # Specify one or more NTP servers.
    server 0.de.pool.ntp.org
    server 1.de.pool.ntp.org
    server 2.de.pool.ntp.org
    server 3.de.pool.ntp.org

    # Use Ubuntu's ntp server as a fallback.
    server ntp.ubuntu.com

    # By default, exchange time with everybody, but don't allow configuration.
    restrict -4 default kod notrap nomodify nopeer noquery
    restrict -6 default kod notrap nomodify nopeer noquery

    # Local users may interrogate the ntp server more closely.
    restrict 127.0.0.1
    restrict ::1