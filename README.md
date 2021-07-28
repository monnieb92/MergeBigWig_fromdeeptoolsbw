# MergeBigWig_fromdeeptoolsbw
### Create and activate a conda enviornment 
```{bash}
conda create --name Deeptools_envir
```
```{bash} 
conda activate Deeptools_envir
```
### Install deeptools: https://anaconda.org/bioconda/deeptools 
```{bash}
conda install -c bioconda deeptools 
```
### Install bigwigmerge: https://anaconda.org/bioconda/ucsc-bigwigmerge
```{bash}
conda install -c bioconda ucsc-bigwigmerge 
```
### Install  bedgraphtobigwig: https://anaconda.org/bioconda/ucsc-bedgraphtobigwig
```{bash}
conda install -c bioconda ucsc-bedgraphtobigwig 
```

#### Example: 
 
```{bash}
bamCoverage -b ../4617_bam/4617-MB-5.hg19.32020.sorted.F4q10.bam -bs 20 -p 6 -of 'bigwig' -o Kas_flag_S5_minusdT.A.normTC.bs20.bw --scaleFactor 1.43

bamCoverage -b ../4617_bam/4617-MB-6.hg19.32120.sorted.F4q10.bam -bs 20 -p 6 -of 'bigwig' -o Kas_flag_S5_minusdT.B.normTC.bs20.bw --scaleFactor 0.9587

```
 
```{bash}
bigWigMerge Kas_flag_S5_minusdT.A.normTC.bs20.bw Kas_flag_S5_minusdT.B.normTC.bs20.bw Kas_flag_S5_minusdT.merged.normTC.bedGraph
```
 
```{bash}
sort -k1,1 -k2,2n Kas_flag_S5_minusdT.merged.normTC.bedGraph > Kas_flag_S5_minusdT.merged.normTC.sorted.bedGraph
```

 
```{bash}
bedGraphToBigWig Kas_flag_S5_minusdT.merged.normTC.sorted.bedGraph /Users/monicabomber/bin/homer/data/genomes/hg19/chrom.sizes Kas_flag_S5_minusdT.merged.normTC.bw
```
*** for computeMatrix make sure to include --missingDataAsZero when preparing to plotHeatmaps with merged bigwig files *** 
