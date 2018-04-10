Synchronizing data with unison
==============================

Unison File synchronizer written in Ocaml (and not Unison-Code something-something implemented in haskell that performs register allocation and instruction scheduling).

Works for OSX, Unix and Windows. It allows two replicas to be stored on different hosts, modified separately then brought up to date by propagating the changes.


History
========

Started in 1999, by Benjamin C Pierce based on his research paper. It is written in Ocaml and uses rsync algorithm to reconcile the changes.


Overview
========

Unison is a bi-directional synchronizer that can resolve conflicts when both replicas were modified.

In practice it means that the software uses client-server model that reconcile changes between server and any number of clients one at a time.


Server profile
==============



Setup
=====

Configure profile

Packages:
unison -- client/server for synchronization
unison-gtk -- gui utility


Running Unison
==============

Create a configuration file ~/.unison/default.prf

* Configure remote and local roots

Local root
----------

root = /home/alex


Remote root
-----------

Uses ssh protocol

root = ssh://unison@unison.flamy.ca//home/unison/sync

The files are copied to /home/unison/sync folder over ssh
synchronization information is stored in ~/.unison folder, but no configuration is kept on the server

Folders to synchronize
----------------------

path = Documents
path = vagrant
path = Desktop
path = Photos
path = .config

Full configuration file
-----------------------

.. code-block:: ini

    root = /home/alex
    root = ssh://unison@unison.flamy.ca//home/unison/sync

    path = Documents
    path = vagrant
    path = Desktop
    path = Photos


Synchronization via command line
================================


.. code-block:: bash

    $ unison --auto


Command output
==============

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

Other synchronization options
=============================

    * batch -- batch mode, don't ask any questions

.. code-block:: bash

    $ unison -batch


Synchronizing via socket
========================

specify remote root as a socket protocol

socket://remotehost:portnum//absolute/path/of/root

Using multiple unison configurations
====================================

default shortcut

.. code-block:: bash

    unison default -auto

where default is the default.prf file in ~/.unison directory


Other interesting options
==========================

    - backups/backup -- keep backup copies of all files
    - fastckeck false -- disable fastcheck
    - prefer -- choose this replica version for conflicting changes

fastcheck
=========

Default behaviour -- fast checking on unix and slow checking on windows (Examining the files)


prefer
======

Automatic preference resolution

prefer <root> newer/older

Batch output options
====================

.. code-block:: bash

    $ unison -batch
    Contacting server...
    Connected [//sync//home/unison/sync -> //workstation//home/alex]
    Looking for changes
      Waiting for changes from server
    Reconciling changes
    changed  ---->            .config/sublime-text-3/Packages/TypeScript/typescript/TS.log
    local        : changed file       modified on 2018-04-07 at 12:16:44  size 82        rw-r--r--
    sync         : unchanged file     modified on 2018-04-05 at 19:54:25  size 82        rw-r--r--
    changed  ---->            .config/sublime-text-3/Packages/User/Package Control.cache/01524fae79697630d0454ba3fabd9414
    local        : changed file       modified on 2018-04-07 at 12:16:49  size 3262924   rw-r--r--
    sync         : unchanged file     modified on 2018-04-05 at 19:54:36  size 3262924   rw-r--r--
    changed  ---->            .config/sublime-text-3/Packages/User/Package Control.cache/01524fae79697630d0454ba3fabd9414.info
    local        : changed file       modified on 2018-04-07 at 12:16:49  size 91        rw-r--r--
    sync         : unchanged file     modified on 2018-04-05 at 19:54:36  size 91        rw-r--r--
    changed  ---->            .config/sublime-text-3/Packages/User/Package Control.last-run
    local        : changed file       modified on 2018-04-07 at 12:16:48  size 10        rw-rw-rw-
    sync         : unchanged file     modified on 2018-04-05 at 19:54:35  size 10        rw-rw-rw-
    Propagating updates
    UNISON 2.48.4 started propagating changes at 21:33:08.34 on 09 Apr 2018
    [BGN] Updating file .config/sublime-text-3/Packages/TypeScript/typescript/TS.log from /home/alex to //sync//home/unison/sync
    [BGN] Updating file .config/sublime-text-3/Packages/User/Package Control.cache/01524fae79697630d0454ba3fabd9414 from /home/alex to //sync//home/unison/sync
    [BGN] Updating file .config/sublime-text-3/Packages/User/Package Control.cache/01524fae79697630d0454ba3fabd9414.info from /home/alex to //sync//home/unison/sync
    [BGN] Updating file .config/sublime-text-3/Packages/User/Package Control.last-run from /home/alex to //sync//home/unison/sync
    [END] Updating file .config/sublime-text-3/Packages/TypeScript/typescript/TS.log
    [END] Updating file .config/sublime-text-3/Packages/User/Package Control.last-run
    [END] Updating file .config/sublime-text-3/Packages/User/Package Control.cache/01524fae79697630d0454ba3fabd9414.info
    [END] Updating file .config/sublime-text-3/Packages/User/Package Control.cache/01524fae79697630d0454ba3fabd9414
    UNISON 2.48.4 finished propagating changes at 21:33:08.55 on 09 Apr 2018
    Saving synchronizer state
    Synchronization complete at 21:33:08  (4 items transferred, 0 skipped, 0 failed)



Reconciliation
==============

To be done manually, mention the other projects Harmony (Synchronize hierarchical XML structure), Boomerang -- a programming language for well-behaved bidirectional transformations on text data.


Caveats
=======

* Files compared by inode number and modtime
* No understanding of hard links





More interesting setup
======================

IONODE sync (look at the python demo file in the project)


Issue
=====

* Anecdotally, synchronization for different versions of unison is iffy. (though it is possible to run multiple versions of unison side-by-side)
* Uses a lot of ram for synchronizing lots of changes. I had to dedicate a VM with 2GB of RAM, otherwise the program would crash when things haven't been synchronized for a while.



References
==========

Unison home page -- https://www.cis.upenn.edu/~bcpierce/unison/
unison debian page -- https://wiki.debian.org/Unison
unison arch page -- https://wiki.archlinux.org/index.php/unison

unison wiki article that's been deleted for some reason -- https://web.archive.org/web/20151125022816/https://en.wikipedia.org/wiki/Unison_%28file_synchronizer%29