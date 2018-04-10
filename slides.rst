:data-transition-duration: 2000
:skip-help: true

.. title: Synchronizing files with unison

---

What is unison
==============

* File synchronizer written in Ocaml
* Works for OSX, Unix and windows
* Allows bidirection synchronization where both replicas were modified


----

History
=======

* Started in 1999 as a part of research paper
* Now in maintenance mode


----

History
=======

* Harmony -- followup project

 * synchronizing hierarchal structures expressed in XML
 * abandoned

* Boomerang -- programming language

 * well-behaved bi-direction transformation
 * on ad-hoc textual data


----

Unison - My usecase
===================

* Synchronizing two or more computers
* Only comparison between two endpoints allowed
* Use start topology with the server in the middle


----

Software setup
==============


* unison -- client/server for synchronization
* unison-gtk -- gui utility

----

Configuration
=============

Client-side configuration only, allows several profiles

Default configuration file in ~/.unison/default.prf


----

default.prf roots
=================

* local root

.. code:: ini

    root = /home/alex

* remote root

.. code:: ini

    root = ssh://unison@unison.flamy.ca//home/unison/sync

----

default.prf
===========

All synchronization paths are relative to the roots


.. code:: ini

    root = /home/alex
    root = ssh://unison@unison.flamy.ca//home/unison/sync

    path = Documents
    path = vagrant
    path = Desktop
    path = Photos

----

Synchronization command
=======================

.. code::

    $ unison --auto

----

Summary output
==============


.. code::

.. code-block:: bash

    $ unison -auto
    Contacting server...
    Connected [//sync//home/unison/sync -> //workstation//home/alex]
    Looking for changes
      Waiting for changes from server
    Reconciling changes

    local          sync
    changed  ---->            .config/sublime-text-3/Packages/TypeScript/typescript/TS.log
    changed  ---->            .config/sublime-text-3/Packages/User/Package Control.cache/01524fae79697630d0454ba3fabd9414
    changed  ---->            .config/sublime-text-3/Packages/User/Package Control.cache/01524fae79697630d0454ba3fabd9414.info
    changed  ---->            .config/sublime-text-3/Packages/User/Package Control.last-run

    Proceed with propagating updates? []

----

Batch sync
==========

In batch mode, Unison doesnt ask any questions

.. code::

    $ unison -batch


----

Sync via socket
===============

specify remote root as a socket protocol

.. code::

    socket://remotehost:portnum//absolute/path/of/root

----

Using multiple unison configurations
====================================

.. code::

    $ unison <profile_name> -auto

Where profile name is *.prf file i.e. ~/.unison/default.prf
There can be multiple profile files


----

backup option
=============

* backups/backup -- keep backup copies of all files
* it is possible to specify different file patters/exclusions for backup


----

fastcheck
=========

Checking for differences:
* default  behaviour on linux -- compare timestamps
* default behaviouur on windows -- examining the file

Options to control check behaviour

.. code::

    - fastcheck true|false|auto

----

prefer
======

Automatic reconciliation preference

- prefer <root> newer/older

----

Caveats
=======

* Files compared by inode number and modtime
* No understanding of hard links


----

Issues
======

* Synchronization between different versions of unison is iffy
* Requires lots of ram to sync the changes.
 * Up to 2GB of RM for large diffs