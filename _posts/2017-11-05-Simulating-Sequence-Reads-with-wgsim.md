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

```wgsim``` is a tool within the SAMtools software package that allows the simulation of FASTQ reads from a FASTA reference. It can simulate diploid genomes with single nucleotide polymorphisms (SNP) and insertion/deletion (indels), and create reads with uniform substitution sequencing errors. It is particularly useful when a FASTA file needs to be included in a mapping pipeline that expects FASTQ files (e.g. variant calling with closed genomes).

<!-- readmore -->

The various flags used by ```wgsim``` are as follows:

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
This is how I used ```wgsim``` on the reference genomes that I wanted to include in my variant calling pipeline:

```wgsim -1 300 -2 300 -r 0 -R 0 -X 0 -e 0 reference.fasta reference_1.fastq reference_2.fastq```

1. ```wgsim -1 300 -2 300```: Instructs wgsim to create paired reads of length 300 bp. The use of 300/300 read length is consistent with my other samples' read lengths (sequenced using MiSeq Reagent Kits v3 2x300).
2. ``` -e 0 -r 0 -R 0 -X 0```: No errors, mutations, or indels were introduced.
3. ```reference.fasta```: the reference genome.
4. ```reference_1.fastq reference_2.fastq```: file names of the output simulated FASTQ reads.
