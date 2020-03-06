# bait-design

**To design custom probes for targeted biallelic SNPs**

To target biallelic SNPs, **bait-design** creates two or four probes for each SNP target similar to that described in [Haak et al 2015](https://www.nature.com/articles/nature14317#Sec11). If the two probe option is chosen (-n 2), the two probes are centred on the SNP, and are identical except for carrying alternate alleles. If the four probe option is chosen (-n 4), two of those probes are again centered on the SNP (each carrying one of alternate alleles), and additionally, one probe ends just before the SNP, and one starts just after.

The output will be in **FASTA DNA sequence format** for [custom myBaits design](http://arborbiosci.com/wp-content/uploads/2017/11/myBaits_Sequence_Guidelines.pdf)

```
1 752565 752566 1_752566 A G

AAACAAAATTGGCAAGTAGAATTTAACTAAATGAAAGAGCTTCTGCACAGCAAGAGAAAC
                               TGAAAGAGCTTCTGCACAGCAAGAGAAACGTTTGACAGAGAATACAGACAACCTACTGAA
                               TGAAAGAGCTTCTGCACAGCAAGAGAAACATTTGACAGAGAATACAGACAACCTACTGAA
                                                             TTTGACAGAGAATACAGACAACCTACTGAATGAGAGAAACTATTTGCAAACTATGCATCT
```

## dependencies

### python packages
- [pybedtools](https://daler.github.io/pybedtools/index.html)
- numpy
- pandas
- argparse
- sys
- os

### softwares
- [bedtools](https://bedtools.readthedocs.io/en/latest/)

## options

```bash
./bait-design

-h,     --help                          "show this help message and exit"
-snp    --selectedSNPs  <filename>      "Targeted SNP information file"
-fi     --fastaFile     <filename>      "Input fasta file to bedtools"
-o      --out           <filename>      "The name to give to the output file."
-len    --ProbeLength   <INT>           "Length of probes to design [default=60]"
-n      --ProbeNumber   <INT>           "Number of probes. Must be 2 or 4 [default=4].
                                         If n=2 two probes are centred on the SNP will design
                                         If n=4 four probes for each SNP target will design"
```

## run examples

```bash
./bait-design -snp targetedSNPs.txt -fi in.fasta
```

```bash
./bait-design -snp targetedSNPs.txt -fi in.fasta -o out.fa
```

```bash
./bait-design -snp targetedSNPs.txt -fi in.fasta -o out.fa -len 52
```

```bash
./bait-design -snp targetedSNPs.txt -fi in.fasta -o out.fa -len 60 -n 2
```

**targetedSNPs.txt** is a space-delimited text file that required six fields (without header)

* *chr* - The number/name of the chromosome
* *posStart* - The starting position of the SNP.
* *posEnd* - The ending position of the SNP.
* *snpID* - unique snp IDs
* *allele1* - usually minor allele
* *allele2* - usually major allele

```
example_targetedSNPs.txt

1 752565  752566  1_752566  G A
1 776545  776546  1_776546  G A
1 832917  832918  1_832918  C T
1 842012  842013  1_842013  G T
1 869302  869303  1_869303  T C
1 891020  891021  1_891021  G A
1 893461  893462  1_893462  C T
1 896270  896271  1_896271  C T
1 903425  903426  1_903426  T C
1 949653  949654  1_949654  A G
```
