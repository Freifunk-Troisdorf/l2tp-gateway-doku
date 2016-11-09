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

With the Setting "Node-Role" you can disable the Client Wifi on the Node between 22 and 6h. Set the Node Roke in the Config Mode to "nightswitch" to activate this feature.

- Added Reboot and Wifi Restart Scripts

v1.2.1
======

- Gluon 2016.2.1 Release

Bugfixes
~~~~~~~~

* Make status page work with disabled cookies/local storage
  (`#912 <https://github.com/freifunk-gluon/gluon/pull/912>`_)

* Update kernel to 3.18.44

  Fixes CVE-2016-5195 and CVE-2016-7117. It is unlikely that these issues pose
  a threat to usual Gluon setups, but installing additional packages may make a
  system vulnerable. In any case, updating is highly recommended.

* Downgrade mac80211 to an earlier state

  Unfortunately, a mac80211 update that was done shortly before the release of
  Gluon v2016.2 (that seemed necessary to properly support ath10k devices) had
  again caused severe ath9k stability issues that remained unreported until v2016.2
  was out.

  We have now reverted mac80211 to an earlier state that was reported to be very
  stable (while keeping the ath10k-specific changes); in addition, some patches
  that were reported to cause connection or performance issues with certain clients
  have been reverted. While is it still not perfectly stable, is should be at least
  as good as (and probably better than) the v2016.1.x release series.

