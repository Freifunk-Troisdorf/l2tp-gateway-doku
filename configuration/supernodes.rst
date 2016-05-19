.. _supernodes:

Supernodes
===================

Wir haben 4 Supernodes im Freifunk Troisdorf Netz. Es ist geplant das jeder Supernode in jedem Subnetz hängt.

Im Normalbetrieb spielt immer ein Supernode Backup für einen anderen.

Die Supernodes sind nach den vom FFRL zugewiesenen Adressen nummeriert. tdf4, 5, 6, und 7

Supernode Liste
---------------

TBD

Backup Plan
-----------

+-----------+-------------------+-------------------+-------------------+
|           |Netz: tdf          |Netz: inn          | Netz: flu         |
+-----------+-------------------+-------------------+-------------------+
|tdf4       |**default**        |                   |backup             |
+-----------+-------------------+-------------------+-------------------+
|tdf5       |backup             |**default**        |                   |
+-----------+-------------------+-------------------+-------------------+
|tdf6       |                   |backup             |**default**        |
+-----------+-------------------+-------------------+-------------------+ 
|tdf7       |                   |                   |                   |
+-----------+-------------------+-------------------+-------------------+ 