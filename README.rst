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

TODO


Reconciliation
==============

To be done manually, mention the other projects Harmony (Synchronize hierarchical XML structure), Boomerang -- a programming language for well-behaved bidirectional transformations on text data.


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