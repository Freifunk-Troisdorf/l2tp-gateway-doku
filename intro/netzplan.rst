.. _netzplan:

Netzplan
========

Freifunk Troisdorf ist ein IP Netz aus dem IPv4 Bereich ``10.188.0.0/16``.

Wir haben unser IP Netz in Segmente eingeteilt um eine bessere Überischt zu haben. 

IPv4
----

Wir haben für unserer Freifunk folgende Netze zugewiesen bekommen:

* Troisdorf - ``10.188.0.0/16`` = **188**

Datenpakete aus diesem Adressbereich werden innerhalb des Freifunks vermittelt, im großen weiten Internet aber nicht geroutet (Hintergrundinformationen dazu `gibt es hier`_).

.. _gibt es hier: http://de.wikipedia.org/wiki/Private_IP-Adresse#Adressbereiche

Unser großes ``10.188.0.0/16`` (mit 65536 Adressen) teilen wir uns ein wenig ein:

``10.188.0.0/16`` wird nicht komplett genutzt, um in Zukunft noch was auf Halde zu haben. Wachsen ist immer einfacher als schrumpfen.

=================== ================== ================= =============== ===========
Netz                (bis)              Verwendung        verteilt durch  status
=================== ================== ================= =============== ===========
``10.188.1.0/24``   ``10.188.1.255``   Services          fix             in Betrieb
``10.188.2.0/24``   ``10.188.2.255``   Static IP Leases  Github/DHCP     Geblockt
``10.188.100.1``    ``10.188.103.255`` Client DHCP-Range troisdorf1      frei
``10.188.104.1``    ``10.188.107.255`` Client DHCP-Range troisodrf2      frei
``10.188.108.1``    ``10.188.111.255`` Client DHCP-Range troisdorf3      frei
``10.188.112.1``    ``10.188.115.255`` Client DHCP-Range troisdorf4      fre
``10.188.116.1``    ``10.188.119.255`` Client DHCP-Range troisodrf5      in Betrieb
``10.188.120.1``    ``10.188.124.255`` Client DHCP-Range troisdorf6      in Betrieb
``10.188.125.1``    ``10.188.128.255`` Client DHCP-Range troisdorf7      frei
``10.188.255.0/24`` ``10.188.255.255`` Gateway IPs       fix             Geblockt
=================== ================== ================= =============== ===========

NEU:

Wir teilen das /16 in 8 /19 Netze ein.

Sub-Domäne 1 - Troisdorf

IPv4: ``10.188.0.0/19``

=================== ================== ================= =============== ===========
Netz                (bis)              Verwendung        verteilt durch  status
=================== ================== ================= =============== ===========
``10.188.0.0/21``   ``10.188.7.255``   Netz Intern       fix             in Betrieb
``10.188.8.0/21``   ``10.188.15.255``  Client DHCP-Range -               in Betrieb
``10.188.16.0/21``  ``10.188.23.255``  Client DHCP-Range -               backup
``10.188.24.0/21``  ``10.188.31.255``  frei              -               frei
=================== ================== ================= =============== ===========

IPv6: ``2a03:2260:121:0001::/64`` wird per Radvd announced

Sub-Domäne 2 - Troisdorf City
IPv4: ``10.188.32.0/19``

=================== ================== ================= =============== ===========
Netz                (bis)              Verwendung        verteilt durch  status
=================== ================== ================= =============== ===========
``10.188.32.0/18`` ``10.188.39.255``   Freie Verwenung   fix             in Betrieb
``10.188.40.0/18`` ``10.188.47.255``   Client DHCP-Range -               Geblockt
``10.188.48.0/18`` ``10.188.55.255``   Client DHCP-Range -               frei
``10.188.56.0/18`` ``10.188.63.255``   Netz              -               frei
=================== ================== ================= =============== ===========

IPv6: ``2a03:2260:121:0002::/64`` wird per Radvd announced

Sub-Domäne 3 - Flüchtlinge
IPv4: ``10.188.64.0/19``

=================== ================== ================= =============== ===========
Netz                (bis)              Verwendung        verteilt durch  status
=================== ================== ================= =============== ===========
``10.188.64.0/18`` ``10.188.71.255``   Freie Verwendung  fix             frei
``10.188.72.0/18`` ``10.188.79.255``   Client DHCP-Range -               frei
``10.188.80.0/18`` ``10.188.87.255``   Client DHCP-Range -               frei
``10.188.88.0/18`` ``10.188.95.255``   Client DHCP-Range -               frei
=================== ================== ================= =============== ===========

IPv6: ``2a03:2260:121:0003::/64`` wird per Radvd announced

Subdomäne 4 - Reserve
IPv4: ``10.188.96.0/19

=================== ================== ================= =============== ===========
Netz                (bis)              Verwendung        verteilt durch  status
=================== ================== ================= =============== ===========
``10.188.96.0/18``  ``10.188.103.255`` Freie Verwendung  fix             frei
``10.188.104.0/18`` ``10.188.111.255`` Client DHCP-Range -               frei
``10.188.112.0/18`` ``10.188.119.255`` Client DHCP-Range -               frei
``10.188.120.0/18`` ``10.188.127.255`` Client DHCP-Range -               frei
=================== ================== ================= =============== ===========

IPv6: ``2a03:2260:121:0004::/64`` wird per Radvd announced

IPv6
----

Wir nutzen das uns vom FFRL zugewiesene Public IPv6 Netz ``2a03:2260:121::/48``

IPv6 Subnetze haben immer eine Prefix-Länge von *64 Bit*. Durch das /48 Subnetz stehen uns also 2^16 = 65536 /64 IPv6 Subnetze zur Verfügung.

.. _interface_bezeichnung:

Interface Bezeichnung
---------------------

Wir vergeben unsere Interface-Bezeichnungen einheitlich!

+-----------+------+-----------------------------+--------------+-------------------+---------------+
|           | eth0 | Mesh - Bridge (Nodes)       | B.A.T.M.A.N  | Inter Gateway VPN | Exit VPN      |  
+-----------+------+-----------------------------+--------------+-------------------+---------------+
|           |      | br-[SUB Name tdf, inn, flu] | bat[SUB NAME]| l2tp-*            | gre-bb-*      |
+-----------+------+-----------------------------+--------------+-------------------+---------------+ 

Namenskonvention
----------------

Unsere Gateways sind durchnummeriert. Angefangen bei **troisdorf0** bis zu **troisdorf9**.

.. _next_node:

Next Node Adressen
------------------

Die Next Node Adressen sind dafür da, um sich im Fehler- oder Troubleshootingfall mit einem Freifunk Knoten zu verbinden.

Diese Adressen sind auf jedem Knoten gleich. Der Freifunker muss sich nur diese Adresse(n) merken und seine Netzwerkkarte für ein Subnetz konfigurieren, in dem diese Adresse(n) liegt um auf seinen Knoten zuzugreifen.

Wir nutzen dazu die jeweils niedrigsten Adressen

* Troisdorf:
    * IPv4: ``10.188.0.1``
    * IPv6: ``2a03:2260:121::1``

    ..

.. _gateway_schema:

Gateway-Schema
--------------

Bevor wir ein Gateway aufsetzen definieren wir einen Namen, dessen Nummer auch gleichzeitig in vielen Scripten genutzt wird.

Mit den uns zugewiesenen Netznummern sowie der Gateway-Nummer und dem Gateway-Namen werden alle benötigten Informationen abgeleitet:

* IPv4
    * Für Gateways wird das Subnetz ``10.188.255.0/24`` verwendet. Die Adressen sind bereits definiert. Beispiel troisdorf1: ``10.188.255.1``

* MAC-Adresse
    * Privates Prefix (``0a2:8c:ae:6f:f6:**``) + Gatewaynummer

    * Beispiele:
        * 10.188.255.1 -> ``a2:8c:ae:6f:f6:01``
        * 10.188.255.2 -> ``a2:8c:ae:6f:f6:02``

* IPv6
    * Range-Prefix (``2a03:2260:121::255:``) + Gatewaynummer

    * Beispiele:
        * troisdorf1 -> ``2a03:2260:121::255:1/64``
        * troisodrf2 -> ``2a03:2260:121::255:2/64``

* DNS
    * ``troisdorf[1-9].freifunk-troisorf.de`` -> A- + AAAA-Record
    * ``[1-9].fftdf.de`` -> CNAME auf s.o.
    * Reverse DNS Eintrag korrekt setzen für Haupt DNS Namen: ``troisdorf[1-9].freifunk-mwu.de``

Beispiel
--------

Gateway: **troisdorf5** - Nummer: **5**

=========== ================================= 
troisdorf5  Mainz                             
=========== ================================= 
IPv4        ``10.188.255.5``                    
IPv6        ``2a03:2260:121::255:5``     
MAC         ``a2:8c:ae:6f:f6:05``             
DNS1        ``troisdorf5.freifunk-troisdorf.de``  
DNS2        ``5.fftdf.de``          
=========== =================================
