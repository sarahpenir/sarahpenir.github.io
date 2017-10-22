---
layout: single
title: "How to Run a Process as a Background Task"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Linux
tags:
  - linux
  - nohup
  - server
  - terminal
  - pgrep
  - ps
  - top
---

To my disappointment, much of my experience in wrangling DNA sequences involves short bacterial genomes. My workstation, which features a 4.0-Ghz 8-core processor and 32 Gb RAM, had been sufficient for my purposes, but only until I encountered the problem of aligning 147 whole-genome sequences prior to tree building. Even though <a href="https://mafft.cbrc.jp/alignment/software/">MAFFT</a> allows multithreading, my workstation would have taken weeks to complete the process. For fear of not graduating in time, using our project-based server suddenly became compulsory.

<!-- readmore -->

In my initial attempts of using our server, my processes either ended up being in a sleep (requires some resource that is currently not available) or zombie state (dead process that hasn't been cleaned up properly). Here's how to keep a process running as a background task in a Linux server:

```sh
nohup command >command.log 2>command.err &
```

1. ```nohup```: Intercepts hangup (HUP) signal that is normally sent to a process to inform that the user has logged off, allowing the process to continue running
2. ```command```: User-provided command (e.g. ```mafft in > out```)
3. ```>command.log```: File that captures the standard output
4. ```2>command.err```: File that captures the standard error. To redirect the standard error to the same output file which contains the standard output, use ```2>&1```.
5. ```&```: Runs the command as a background task

```pgrep``` can be used to monitor the process even after the original terminal that accepted the command was closed. ```pgrep``` lists the process IDs that match the selection criteria (pattern) to standard output. For example:

```sh
pgrep -u root mafft
```

will only list the processes that are called ```mafft``` and owned by ```root```.

Using the process identifier (PID) listed by ```pgrep```, keep tabs on the parent and child processes of the command using the ```ps``` command:

```sh
ps PID
```

A quick snapshot of the absolute paths of the processes running in the server can be obtained with:

```sh
top -c
```
