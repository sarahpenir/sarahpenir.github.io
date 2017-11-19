---
layout: single
title: "Calculating Mapping Statistics from a BAM file using SAMtools and awk"
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

A ```BAM``` file is the binary version of a ```SAM``` file, a tab-delimited text file that contains sequence alignment data. Mapping tools, such as ```Bowtie 2``` and ``BWA``, generate ```SAM``` files as output when aligning sequence reads to large reference sequences. The ```head``` of a ```SAM``` file takes the following form:

```
@HD	VN:1.5	SO:coordinate
@SQ	SN:ref	LN:45
r001	99	ref	7	30	8M2I4M1D3M	=	37	39	TTAGATAAAGGATACTG	*
r002	0	ref	9	30	3S6M1P1I4M	*	0	0	AAAAGATAAGGATA	*
r003	0	ref	9	30	5S6M	*	0	0	GCCTAAGCTAA	*	SA:Z:ref,29,-,6H5M,17,0;
r004	0	ref	16	30	6M14N5M	*	0	0	ATAGCTTCAGC	*
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

The mean read depth, breadth of coverage of the reference genome, and the proportion of the reads that mapped to the reference genome can be obtained from a ```BAM``` file using the combination of ```awk```, and the ```SAMtools 1.3.1```  utilities ```depth``` and ```flagstat```.

## Mean Read Depth

```sh
samtools depth -a file.bam | awk '{c++;s+=$3}END{print s/c}'
```

1. ```samtools depth -a file.bam```: Computes the depth at each position or region. The ```-a``` flag indicates that the depth must be calculated at all positions, including at those with zero depth. This command yields the following:

	```
	chr1    249231316   7
	chr1    249231317   2
	chr1    249231318   2
	chr1    249231319   2
	chr1    249231320   1
	```

   The three columns describe the reference sequence name, the 1-based leftmost mapping position, and the depth at the specified position, respectively.

2. ```awk '{c++;s+=$3}END{print s/c}'```: The pipe passes the output from ```samtools -depth``` to ```awk```, which calculates two variables: ```c``` (the total number of positions), and ```s``` (the cumulative depth across all positions). The mean read depth is ```s/c```.

## Breadth of Coverage

```sh
samtools depth -a file.bam | awk '{c++; if($3>0) total+=1}END{print (total/c)*100}'
```

1. ```samtools depth -a file.bam```: Computes the depth at each position or region. The ```-a``` flag indicates that the depth must be calculated at all positions, including at those with zero depth.

2. ```awk '{c++; if($3>0) total+=1}END{print (total/c)*100}```: The pipe passes the output from ```samtools -depth``` to ```awk```, which calculates two variables: ```c``` (the total number of positions), and ```total``` (which receives an increment of 1 when the depth is greater than 0 ```if($3>0) total+=1```). The breadth of coverage is ```(total/c)*100```.

## Proportion of the Reads that Mapped to the Reference

```sh
samtools flagstat file.bam | awk 'NR == 3 {split($5,a,"("); split(a[2],b,"%"); print b[1]}'
```

1. ```samtools flagstat file.bam```: Does a full pass through the input file to calculate and print pertinent stats to standard output. ```samtools flagstat``` provides these statistics:

	```
	6874858 + 0 in total (QC-passed reads + QC-failed reads)
	90281 + 0 duplicates
	6683299 + 0 mapped (97.21%)
	6816083 + 0 paired in sequencing
	3408650 + 0 read1
	3407433 + 0 read2
	6348470 + 0 properly paired (93.14 No value assigned)
	6432965 + 0 with itself and mate mapped
	191559 + 0 singletons (2.81 No value assigned)
	57057 + 0 with mate mapped to a different chr
	45762 + 0 with mate mapped to a different chr (mapQ>=5)
	```
2. ```awk 'NR == 3```: Captures the third line which contains the desired mapping statistic.

3. ```split($5,a,"(")```: Captures the fifth column of the third line and splits it into two fields:
	```
	a[1] = ""
	a[2] = "97.21%)"
	```
4. ```split(a[2],b,"%")```: Captures the second element of array ```a``` and splits it into two fields:
	```
	b[1] = "97.21"
	b[2] = ""
	```
5. ```print b[1]```: Prints the proportion of the reads that mapped to the reference.

Ultimately, these three code snippets can be called in a single shell file to automate the process of calculating mapping statistics from a ```BAM``` file.
