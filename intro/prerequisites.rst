.. _voraussetzungen:

Voraussetzungen
===============

* voller Root Zugriff für alle Admins
* öffentliche IPv4 Adresse
* öffentliche IPv6 Adresse
* voller Kernelzugriff
    * Linux direkt installiert,
    * oder als KVM-Instanz (OpenVZ o.ä. nicht möglich)
* Hier genutzt: Debian 8

Betrieb und Zugang
------------------

Unsere Server werden momentan von 2 Personen Privat betriben. In unserem Setup ist immer nur 1 Server Aktiver Supernode, um unter anderem den Inter Gateway Traffic zu sparen. Dies funktioniert mit L2TP sehr gut, da die vorhandene Performance mit 1 Server ausreichend ist.

Wir installieren unsere Gateways per Ansible, was uns ein Identisches Setup per Server ermöglicht und uns neue Gateways innerhalb weniger Minuten ausrollen lässt. Die Ansible Config findet Ihr hier: [LINK EINFÜGEN]

Schema
------

Wie unser Netz aufgebaut ist seht ihr am einfachsten an dieser Darstellung:

.. image:: fftdf-gw-schema.png
    :alt: Gateway - schematische Darstellung
    :scale: 85%
    :align: center

Funktionen & dafür benötigte Software
-------------------------------------

Momentan kommen auf allen Gateways Debian 8 (jessie) zum Einsatz.

Für viele der Gate-Funktionen wird weitere Software benötigt, die alle aus den Debian Repositories nachinstalliert werden können.

.. seealso::
    - :ref:`packages`

Verbindung der Server und Nodes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Die Nodes bauen ihr Freifunk mit dem Mesh-Protokoll *B.A.T.M.A.N* selbständig auf.

Da das Netz aber noch nicht dicht genug ist, dass alle Nodes sich über ihre Funk-Interfaces erreichen können, helfen wir über eine VPN-Verbindung über das Internet nach, um einzelne Wolken zu überbrücken.

So wie über ihre Funk-Interfaces, sprechen die Nodes das *B.A.T.M.A.N* Protokoll auch über ihre VPN-Verbindungen.

Die Gateways sind die VPN Server für unsere Nodes. Die Nodes bauen alle einen L2TP Tunnel zu diesen auf.

Alle Gateways verbinden sich für das VPN auch vollständig untereinander. So entsteht eine Multi-Stern-Architektur. Alle Sternmittelpunkte sind untereinander voll vermascht.

Auf den Gateways wird hierzu **L2TP** sowie das Kernel Modul **batman_adv** benötigt.

.. seealso::
    - :ref:`packages`
    - :ref:`l2tp`

DHCP für die Clients
^^^^^^^^^^^^^^^^^^^^

Nodes, Clients und Gateways sind über ein Layer-2-Netz miteinander verbunden (*B.A.T.M.A.N*, s. o.).

Die Gateways halten auch als DHCP-Server für die Clients her.

Verfügbare IPv4-Ranges, aus denen der DHCP-Server vergeben darf, müssen innerhalb bzw. mit der Admin-Gruppe abgestimmt werden.

Hierfür wird **isc-dhcp-server** genutzt. Für das vorbereitende Ausrollen von IPv6 Adressen benötigen wir hier auch **radvd**.

.. seealso::
    - :ref:`dhcp`
    - :ref:`radvd`

Übergang ins restliche Internet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Die Verbindung ins Internet wird über den Freifunk Rheinland e.V. realisiert. Wir verbinden uns hierzu per **GRE** in das Backbone des FFRL und bekommen von hier auch Public IPv4 und IPv6 Adressen.

.. seealso::
    - :ref:`packages`
    - :ref:`interfaces`
    - :ref:`routing_tables`
    - :ref:`policyrouting`
    - :ref:`internetexit`

Datenschutz auf dem Gateway
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Unsere Gateways loggen keinen Traffic! Es werden lediglich Statistiken für die Bewertung der Auslastung unserer Gateways gespeichert. 

Alles was existiert sind die zur Laufzeit benötigten Verbindungsdaten. DHCP-Leases, Batman Protokolldaten und die ARP-Tabelle.

Diese werden nur im Arbeitsspeicher vorgehalten, ist das Gateway aus (z.B. die Herren in Grün nehmen den Server mit), sind diese i.d.R. weg.

.. seealso::
    - :ref:`logging`
