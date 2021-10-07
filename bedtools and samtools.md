# Homework
根据我们给出的exon.bed进行合并，对Shape01.bam进行排序并提取比对质量高的reads，然后计算BAM文件在的exon.bed上对齐计数，并输出前10行。

```
bedtools merge -i exons.bed -c 1,4 -o count,collapse | head -10

chr1    11873   12227   1       NR_046018_exon_0_0_chr1_11874_f
chr1    12612   12721   1       NR_046018_exon_1_0_chr1_12613_f
chr1    13220   14829   2       NR_046018_exon_2_0_chr1_13221_f,NR_024540_exon_0_0_chr1_14362_r
chr1    14969   15038   1       NR_024540_exon_1_0_chr1_14970_r
chr1    15795   15947   1       NR_024540_exon_2_0_chr1_15796_r
chr1    16606   16765   1       NR_024540_exon_3_0_chr1_16607_r
chr1    16857   17055   1       NR_024540_exon_4_0_chr1_16858_r
chr1    17232   17368   1       NR_024540_exon_5_0_chr1_17233_r
chr1    17605   17742   1       NR_024540_exon_6_0_chr1_17606_r
chr1    17914   18061   1       NR_024540_exon_7_0_chr1_17915_r
```

```
samtools sort -@8 Shape01.bam > Shape01.sort.bam
```

```
samtools view -q 1 -O bam -o Shape01.highQual.bam Shape01.bam
```

```
bedtools multicov -bams Shape01.bam -bed exon.bed | head -10
```
