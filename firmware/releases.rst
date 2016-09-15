.. _releases:

v1.0
====

.. seealso:: `Github site.conf <https://github.com/Freifunk-Troisdorf/site/>`_

- Erstes Gluon Release nach dem Netsplit

v1.0.2
======

.. seealso:: `Github site.conf <https://github.com/Freifunk-Troisdorf/site/>`_

- Anpassung der IPv6 Adressen in den neuen netzen

v1.0.3
======

.. seealso:: `Github site.conf <https://github.com/Freifunk-Troisdorf/site/>`_

Autoupdater Bugfix

v1.0.5
======

.. seealso:: `Github site.conf <https://github.com/Freifunk-Troisdorf/site/>`_

- Bugfixes

v1.0.7
======

.. seealso:: `Github site.conf <https://github.com/Freifunk-Troisdorf/site/>`_

- Fehlerbehebungen im Reboot und Wifi Restart Script

v1.0.8
======

.. seealso:: `Github site.conf <https://github.com/Freifunk-Troisdorf/site/>`_

- Update auf Gluon Master wegen Wifi Problemen

v1.1
======

.. seealso:: `Github site.conf <https://github.com/Freifunk-Troisdorf/site/>`_

- Gluon 2016.1.6 Release

Improves the reception by about 20dB.
ar71xx-generic: switch default WAN/LAN assignment on Ubiquiti UAP Pro (#764)

Switch to the usual “PoE is WAN/setup mode, secondary is LAN” scheme. This only affects new installations; the assignment won’t be changed on updates unless the configuration is reset.
ar71xx-generic: fix ath10k memory leak (#690)
ar71xx-generic: add support for new TP-Link region codes (#860)

TP-Link has started providing US- and EU-specific firmwares for the Archer C7 v2. To generate Gluon images installable from these new firmwares, the GLUON_REGION variable must be set to eu or us in site.mk or on the make command line (the images will still be installable from all old firmwares without region codes).

- Added Wifi-Restart Script 
.. seealso:: `Github <https://github.com/Freifunk-Troisdorf/packages/blob/v2016.1/netwatch/files/lib/tro/netwatch/wifi-restart.sh>`_

v1.1.3
======

- Added Nightswitch Script to turn off the Client Wifi between 22-06.
- Added Reboot and Wifi Restart Scripts

