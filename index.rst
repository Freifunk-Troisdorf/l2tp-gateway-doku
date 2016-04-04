Freifunk Troisdorf Gateway Doku
==================

In dieser Doku beschreiben wir unser Gluon/Linux Gateway Setup. Diese Daten stammen aus unserem Netz in Troisdorf, weshalb auch unsere IP Netze in den Config dateien zu finden sind.

Dieses Setup ist in mehreren Monaten entstanden, und kann dennoch noch einige Fehler enthalten. Wir versuchen unsere Gedankengänge hier so gut es geht zu umschreiben.

Intro
-----

.. toctree::
   :maxdepth: 2

   intro/prerequisites
   intro/netzplan
   intro/gluon

Konfiguration
-------------

.. toctree::
   :maxdepth: 2

   configuration/basics
   configuration/interfaces
   configuration/policyrouting
   configuration/daemons/ddi
   configuration/daemons/fastd
   configuration/daemons/alfred
   configuration/daemons/apache
   configuration/daemons/icvpn
   configuration/internetexit
   configuration/cleanup

Betrieb
-------

.. toctree::
   :maxdepth: 2

   operations/tests
   operations/workflows
   operations/scripts

Mitwirken
---------

Du hast eine Stelle entdeckt, die Schreibfehler enthält, was unsauber oder falsch erklärt, nicht existiert aber sollte, oder veraltet ist?

Gerne nehmen wir sinnvolle Vorschläge und Ergänzungen mit auf, über den `Issue-Tracker <http://github.com/freifunk-mwu/technik-meta/issues>`_ (mit dem `Label 'Doku' <https://github.com/freifunk-mwu/technik-meta/labels/Doku>`_) oder am besten gleich per Pull Request.
