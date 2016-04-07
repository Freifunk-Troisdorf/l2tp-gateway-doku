.. _bird:

Bird Konfiguration
==================

Bird wird benutzt um BGP auf den Tunneln zum Freifunk Rheinland e.v. zu sprechen. Es sorgt für das dynamische Routing.

Bird muss für IPv4 und IPv6 kofiguriert werden. 

bird
----

Die Konfiguration für Bird (IPv4) wird unter /etc/bird/bird.conf erledigt.

Dies ist eine Beispielkonfiguration für bird auf unserem Supernode:


    /*
     *      This is an example configuration file.
     */

    #debug protocols all;

    # Override router ID
    router id 10.188.255.5;


    protocol direct {
            interface "*";
    };

    protocol kernel {
            device routes;
            import all;
            export all;
            kernel table 42;
    };

    protocol device {
            scan time 8;
    };

    function is_default() {
            return (net ~ [0.0.0.0/0]);
    };

    # own network
    function is_self_net() {
        return (net ~ [ 10.188.0.0/16+ ]);
    }

    # freifunk ip ranges in general
    function is_freifunk() {
      return net ~ [ 10.0.0.0/8+,
        104.0.0.0/8+
      ];
    }

    filter hostroute {
            if net ~ 185.66.193.105/32 then accept;
            reject;
    };

    # Uplink über ff Rheinland
    template bgp uplink {
            local as 65066;
            import where is_default();
            export filter hostroute;
            next hop self;
            multihop 64;
            default bgp_local_pref 200;
    };

    protocol bgp ffrl_bb_a_ak_ber from uplink {
            source address 100.64.2.151;
            neighbor 100.64.2.150 as 201701;
    };

    protocol bgp ffrl_bb_b_ak_ber from uplink {
            source address 100.64.2.153;
            neighbor 100.64.2.152 as 201701;
    };

    protocol bgp ffrl_bb_a_ix_dus from uplink {
            source address 100.64.2.155;
            neighbor 100.64.2.154 as 201701;
    };

    protocol bgp ffrl_bb_b_ix_dus from uplink {
            source address 100.64.2.157;
            neighbor 100.64.2.156 as 201701;
    };

bird6
-----

Die Konfiguration für Bird6 (IPv6) wird unter /etc/bird/bird6.conf erledigt.

Dies ist eine Beispielkonfiguration für bird6 auf unserem Supernode:

    # Configure logging
    #log syslog { debug, trace, info, remote, warning, error, auth, fatal, bug };
    #log stderr all;
    #log "tmp" all;
    #log syslog all;

    #debug protocols all;

    # Override router ID
    router id 10.188.255.5;

    protocol direct {
    #        interface "*";  # Restrict network interfaces it works with
    #        interface "bat0", "gre-*", "eth*", "lo";  # Restrict network interfaces it works with
            interface "bat0", "gre-*", "lo";  # Restrict network interfaces it works with

    }


    protocol kernel {
            device routes;
            import all;
            export all;             # Default is export none
            kernel table 42;                # Kernel table to synchronize with (default: main)
    }

    protocol device {
            scan time 10;           # Scan interfaces every 10 seconds
    }

    function is_default() {
            return (net ~ [::/0]);
    }

    # own networks
    function is_self_net() {
    return net ~ [ fda0:747e:ab29:7405::/64+ ];
    }

    # freifunk ip ranges in general
    function is_freifunk() {
    return net ~ [ fc00::/7{48,64},
    2001:bf7::/32+];
    }

    filter hostroute {
            if net ~ 2a03:2260:121::/48 then accept;
            reject;
    }



    # Uplink zum FF Rheinland
    template bgp uplink {
            local as 65066;
            import where is_default();
            export filter hostroute;
            gateway recursive;
    }


    protocol bgp ffrl_bb_a_ak_ber from uplink {
            source address 2a03:2260:0:155::2;
            neighbor 2a03:2260:0:155::1 as 201701;
    }

    protocol bgp ffrl_bb_b_ak_ber from uplink {
            source address 2a03:2260:0:156::2;
            neighbor 2a03:2260:0:156::1 as 201701;
    }


    protocol bgp ffrl_bb_a_ix_dus from uplink {
            source address 2a03:2260:0:157::2;
            neighbor 2a03:2260:0:157::1 as 201701;
    }

    protocol bgp ffrl_bb_b_ix_dus from uplink {
            source address 2a03:2260:0:158::2;
            neighbor 2a03:2260:0:158::1 as 201701;
    }
