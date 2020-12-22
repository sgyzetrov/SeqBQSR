# SeqBQSR
A Re-implementation of GATK's Base Quality Score Recalibration Tool in Seq Programming Language

Base quality score recalibration (BQSR) is a data pre-processing step that detects systematic errors made by the sequencing machine when it estimates the accuracy of each base call<sup>[1]</sup>.

This project is implemented using [Seq](https://seq-lang.org/index.html) (version 0.9.11).

## Arguments Implemented

- BAMInput (.bam): BAM file that needs recalibration
- referenceFASTA (.fasta): FASTA Reference file needed for BQSR
- knownSitesVCF (.vcf): Known site of variants, only support 1 database input
- outSeqFileName (.txt): Recalibrated sequence file from BAMInput

## Event Implemented

Only event 'M' is supported (e.g. M(ism)atch case), event 'I' or 'D' is not here (yet?).

## Covariates Implemented

- [x] sequence context
- [x] machine cycle (position in read)

## Features Tabulated

- read group the read belongs to
- quality score reported by the machine
- machine cycle producing this base (Nth cycle = Nth base from the start of the read) 
- current base + previous base (dinucleotide)

## Tables Generated (print to console)

- [x] Arguments Table -- a table with all the arguments and its values 
- [x] Quantization Table
- [x] ReadGroup Table
- [x] Quality Score Table
- [x] Covariates Table

## Testing Example

```sh
$> cd src
$> seqc -d SeqBQSR.seq ../testCase/NA12878.chr17_69k_70k.dictFix.bam \
../testCase/human_g1k_v37.chr17_1Mb.fasta \
../testCase/dbsnp_132.b37.excluding_sites_after_129.chr17_69k_70k.vcf \
../testOut/recal_seq.txt > out.txt
```

Existing example outputs can be found in `testOut` folder.

## Reference

[1] [GATK Base Quality Score Recalibration (BQSR) Technical Documentation](https://gatk.broadinstitute.org/hc/en-us/articles/360035890531-Base-Quality-Score-Recalibration-BQSR-)

## LICENSE

Copyright (c) 2020 Yang (Simon) Guo

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.