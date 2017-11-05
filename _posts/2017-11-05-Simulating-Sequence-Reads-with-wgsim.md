---
layout: single
title: "Simulating Sequence Reads from a Reference Genome with wgsim"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Bioinformatics
tags:
  - wgsim
  - read simulation
  - FASTQ
---

wgsim is a tool included in the SAMtools software package that allows the simulation of FASTQ sequence reads from a FASTA reference genome. It can simulate diploid genomes with single nucleotide polymorphisms (SNP) and insertion/deletion, and create reads with uniform substitution sequencing errors. It is particularly useful when a FASTA file needs to be included in a mapping pipeline that expects FASTQ files (e.g. variant calling with closed genomes).

<!-- readmore -->

The various flags used by wgsim are as follows:

```
-e FLOAT      base error rate [0.02]
-d INT        outer distance between the two ends [500]
-s INT        standard deviation [50]
-N INT        number of read pairs [1000000]
-1 INT        length of the first read [70]
-2 INT        length of the second read [70]
-r FLOAT      rate of mutations [0.001]
-R FLOAT      fraction of indels [0.15]
-X FLOAT      probability an indel is extended [0.30]
-S INT        seed for random generator [-1]
-A FLOAT      disgard if the fraction of ambiguous bases higher than FLOAT [0.05]
-h            haplotype mode
```
