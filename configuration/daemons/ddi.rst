.. _ddi:

DNS-DHCP-IP
===========

.. _bind:

BIND
----

/etc/bind/named.conf.fftdf:

    zone "fftdf" {
      type slave;
      masters { 10.188.1.100; };
      file "/var/lib/bind/db.fftdf";
    };

/etc/bind/named.conf.options


    options {
            directory "/var/cache/bind";

            // If there is a firewall between you and nameservers you want
            // to talk to, you may need to fix the firewall to allow multiple
            // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

            // If your ISP provided one or more IP addresses for stable
            // nameservers, you probably want to use them as forwarders.
            // Uncomment the following block, and insert the addresses replacing
            // the all-0's placeholder.

            // forwarders {
            //      0.0.0.0;
            // };

            //========================================================================
            // If BIND logs error messages about the root key being expired,
            // you will need to update your keys.  See https://www.isc.org/bind-keys
            //========================================================================
            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { 10.188.255.5; };
            listen-on-v6 { 2a03:2260:121::255:5; };
    };

.. _dhcp:

DHCPd
-----

Um IPv4 im Netzwerk nutzen zu können müssen wir auf dem Gateway einen DHCP Server aufsetzen. Der DHCP Server Verteilt die Adressen aus dem zum Gateway zugewiesenen Adressbereich.

.. seealso::
    :ref:`netzplan`

Die Konfiguration ist relativ einfach gehalten. Sie wird unter /etc/dhcp/dhcpd.conf abgelegt:

    ddns-update-style none;
    option domain-name "fftdf";
    default-lease-time 300;
    max-lease-time 3600;
    log-facility local7;
    subnet 10.188.0.0 netmask 255.255.0.0 {
    authoritative;
    range HIER DER RANGE AUS DEM NETZPLAN;
    option domain-name-servers 10.188.255.5;
    option routers 10.188.255.5;
    option interface-mtu 1312;
    interface bat0;
    }

TBD

.. _radvd:

RAdvD
=====

Damit die Clients im Netz auch in den Genuss von öffentlichem IPv6 kommen, müssen die Public IPv6-Prefixe zusätzlich zu den ULA-Prefixes per Router Advertisements bekannt gegeben werden. Dazu ergänzt man die Public IPv6-Prefixe in der /etc/radvd.conf:

    interface bat0 {
            AdvSendAdvert on;
            IgnoreIfMissing on;
            MaxRtrAdvInterval 200;
            RDNSS 2a03:2260:121::255:5 {};
            prefix 2a03:2260:121::/64 {
                    AdvOnLink on;
                    AdvAutonomous on;
                    AdvRouterAddr on;
            };
    };


