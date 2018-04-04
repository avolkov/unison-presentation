Synchronizing data with unison
==============================

Unison File synchronizer written in Ocaml (and not Unison-Code something-something implemented in haskell that performs register allocation and instruction scheduling).

Works for OSX, Unix and Windows. It allows two replicas to be stored on different hosts, modified separately then brought up to date by propagating the changes.


History
========

Started in 1999, mention the paper on file sync.


Setup
=====

Configure profile
Unison GUI (find it!)


More interesting setup
======================

IONODE sync (look at the python demo file in the project)


Issue
=====

* Anecdotally, synchronization for different versions of unison is iffy.
* Uses a lot of ram for synchronizing lots of changes. I had to dedicate a VM with 2GB of RAM, otherwise the program would crash when things haven't been synchronized for a while.



