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
  
v1.2.6
======

- Gluon 2016.2.4 Release

Bugfixes
~~~~~~~~

* Fix batman-adv (compat 15) not being able to transmit packages of specific sizes (`b7eeef9 <https://github.com/freifunk-gluon/gluon/commit/b7eeef9b04b44a70b2a953c4efe35a3fdceba2db>`_)

  We suspect that this issue was also the reason for the autoupdater/wget hangs observed by many communities.
  Non-Gluon nodes like gateways should be updated to batman-adv 2017.0.1 to get the fix.

* Fix build after ftp.all.kernel.org discontinuation (`#1059 <https://github.com/freifunk-gluon/gluon/issues/1059>`_)

* Fix high load because of frequent calls of the respondd initscript (`9a0aeb9 <https://github.com/freifunk-gluon/gluon/commit/9a0aeb9b7482df4e4515e61356b9d393e3a7eacb>`_)

  The respondd restart triggers added in v2016.2.3 ran a significant portion of the respondd initscript for each router advertisement
  received. This was fixed by a backport of a netifd patch.

* x86 sysupgrade fixes (`41fd50d <https://github.com/freifunk-gluon/gluon/commit/41fd50d20ba31d73c4796c5b2d4eb44ad2258b90>`_,
  `ad37e2b <https://github.com/freifunk-gluon/gluon/commit/ad37e2b6b43b2c3389356d892b04f3873d8f6b93>`_)

  This fixes sysupgrade on mmcblk and similar devices.

Other changes
~~~~~~~~~~~~~

* The manifest generator has been extended to generate SHA256 checksums in addition to SHA512 ones
  (`f9d59be <https://github.com/freifunk-gluon/gluon/commit/f9d59be731efd31a26c59e049ccbdc4b1762f6b1>`_)

  We have recently switched the autoupdater to SHA256 in the Gluon master to avoid mixing two different
  lengths of hashes for no good reason. This makes the manifests of Gluon v2016.2.x compatible with the
  new autoupdater so it doesn't prevent backports or downgrades.

  **Note:** Downgrades of major Gluon versions are generally unsupported and will often lead to
  broken configurations.

Known Issues
~~~~~~~~~~~~

* x86 sysupgrade (sometimes) loses config when kernel partition grows (`#1010 <https://github.com/freifunk-gluon/gluon/issues/1010>`_)

  This issue affects upgrades from v2016.2.x and older to the Gluon master only, we hope to fix it before the next
  major release.

* Default TX power on many Ubiquiti devices is too high, correct offsets are unknown (`#94 <https://github.com/freifunk-gluon/gluon/issues/94>`_)

  Reducing the TX power in the Advanced Settings is recommended.

* The MAC address of the WAN interface is modified even when Mesh-on-WAN is disabled (`#496 <https://github.com/freifunk-gluon/gluon/issues/496>`_)

  This may lead to issues in environments where a fixed MAC address is expected (like VMware when promicious mode is disallowed).

* Inconsistent respondd API (`#522 <https://github.com/freifunk-gluon/gluon/issues/522>`_)

  The current API is inconsistent and will be replaced eventually. The old API will still be supported for a while.

