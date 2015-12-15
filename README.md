Description
===========

This repository contains small utilities for use on cloud developers' local
machines. Scripts in this repository aim to be self-contained to the point
where checking it out and and adding its bin/ directory to $PATH should be
sufficient to run them. If they do have run-time dependencies beyond what can
reasonably expected to be present on a modern unixoid system those are listed
below.

Setup
=====

Add this repository's bin/ subdirectory to your shell's search path, e.g. if
you checked it out to ~/autostrap-utils, do a

  `$ PATH=$PATH:~/autostrap-utils/bin`

To make the scripts available permanently, add this command to your shell's
initialization file (e.g. ~/.bashrc if you use bash).

Scripts
=======

compare_yaml_hash
-----------------

### SYNOSIS

  `compare_yaml_hash -k <key> [-a] <file> [ <file> ... ]`

This script recursively compares all occurences of the YAML hash *key* in a
directory tree. It outputs all keys whose values differ across multiple
occurences of this YAML hash, along with the names of the files where these
deviations occured. It will return 1 if any differing keys occur and 0
otherwise.

heat_doclint
------------

### SYNOPSIS

  `heat_doclint file <file ...>`

This script checks the heat templates passed as command line parameters for
missing `description` fields. Currently only heat templates in YAML format are
supported.

heat2adoc
---------

### SYNOPSIS

  `heat2adoc [-o <outfile>] [-p [name space prefix>] <file>`

This script generates asciidoc documentation from a heat template's
`description` fields. By default it prints the generated documentation to
stdout. It can optionally prefix a name space component to the heat template's
resource name. This name space component is supplied as argument of the `-p`
option. Currently only heat templates in YAML format are supported.


hiera_tree
----------

### SYNOPSIS

  `hiera_tree <dir> [<topic> ...]`

This script generates a hiera.yaml file with a hierarchy containing all yaml
files found in *<dir>*. It is used by `merge_classes`. By default it includes
all topic directories under *<dir>*, but those can be filtered to include only
these specified as optional command-line arguments.

merge_classes
-------------

### SYNOPSIS

  `merge_classes --data-dir <dir> <topic> [<topic> ...]`

This script builds a Hiera classes array from a list of configuration topics in
sys11-config. It uses Hiera's array merge to resolve duplicate entries. It can
generate such an array from any hieradata directory following the same naming
convention as sys11-config (hieradata contains a classes.d directory with topic
subdirectories). It's primary purpose is composing node or node type
configurations for use in a project configuration repository. It uses
`hiera_tree`, so ensure you've got the bin/ subdirectory in your PATH.
