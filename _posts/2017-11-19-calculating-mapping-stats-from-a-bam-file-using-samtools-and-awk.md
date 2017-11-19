---
layout: single
title: "Calculating Mapping Stats from a BAM file using SAMtools and awk"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Bioinformatics
  - AWK
tags:
  - mapping
  - SAMtools
  - awk
  - bioinformatics
---

A ```BAM``` file is the binary version of a ```SAM``` file, a tab-delimited text file that contains sequence alignment data. Mapping tools, such as ```Bowtie 2``` and ``BWA``, generate ```SAM``` files as output when aligning sequence reads to large reference sequences. A snippet of a ```SAM``` file takes the following form:

```
@HD	VN:1.5	SO:coordinate
@SQ	SN:ref	LN:45
r001  99  ref	7   30	8M2I4M1D3M	=	37	39	TTAGATAAAGGATACTG	*
r002	0   ref	9   30	3S6M1P1I4M	*	0	  0	  AAAAGATAAGGATA	  *
r003	0	  ref	9	  30	5S6M        * 0   0   GCCTAAGCTAA	      *	SA:Z:ref,29,-,6H5M,17,0;
r004	0	  ref	16  30	6M14N5M	    *	0	  0	  ATAGCTTCAGC	      *
``` 

The header section is denoted by the character ```@``` followed by one of the two-letter header record type codes. The table below describes the available predefined tags in the header section of a ```SAM``` file:


| Tag | Description |
| --- | --- |
| ```@HD``` | The header line. The first line if present. |
| ```@SQ``` | Reference sequence dictionary. The order of ```@SQ``` lines defines the alignment sorting order. | 
| ```@RG``` | Read group. Unordered multiple ```@RG``` lines are allowed. | 
| ```@PG``` | Program |
| ```@CO``` | One-line text comment. Unordered multiple ```@CO``` lines are allowed. |  

<!-- readmore -->

The alignment section, on the other hand, has 11 mandatory fields, as well as a variable number of optional fields:


| Col | Field | Type | Description |
| --- | --- | --- | --- |
| 1 | QNAME | String | Query template NAME |
| 2	| FLAG | Int | Bitwise FLAG |
| 3 | RNAME | String | References sequence NAME |
| 4 | POS | Int| 1- based leftmost mapping POSition |
| 5 | MAPQ | Int | MAPping Quality |
| 6 | CIGAR | String | CIGAR String |
| 7 | RNEXT | String | Ref. name of the mate/next read |
| 8 | PNEXT | Int | Position of the mate/next read |
| 9 | TLEN | Int | Observed Template LENgth |
| 10 | SEQ | String | Segment SEQuence |
| 11 | QUAL | String | ASCII of Phred-scaled base QUALity+33 |
