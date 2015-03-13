Description
===========

This repository contains small utilities for use on cloud developers' local
machines. Scripts in this repository aim to be self-contained to the point
where checking it out and and adding its bin/ directory to $PATH should be
sufficient to run them. If they do have run-time dependencies beyond what can
reasonably expected to be present on a modern unixoid system those are listed
below.

Scripts
=======

merge_classes
-------------

### SYNOPSIS

`merge_classes --data-dir <dir> <topic> [<topic> ...]`

This script builds a Hiera classes array from a list of configuration topics in
sys11-config. It uses Hiera's array merge to resolve duplicate entries. It can
generate such an array from any hieradata directory following the same naming
convention as sys11-config (hieradata contains a classes.d directory with topic
subdirectories). It's primary purpose is composing node or node type
configurations for use in a project configuration repository.
