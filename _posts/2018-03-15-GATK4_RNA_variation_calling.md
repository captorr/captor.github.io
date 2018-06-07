---
layout: post
title: "GATK4 RNAseq SNP calling"
date: 2018.03.15 15:37
categories: scripts
tag: scripts
---
* content
{:toc}


GATK4。用转录组测序数据做SNP calling的测试流程。

全部流程基于GATK官网的某个best practice：[GATK Calling variants in RNAseq](https://software.broadinstitute.org/gatk/documentation/article.php?id=3891)

GATK 3.x版本和GATK4有差别，做了部分修改。

## Mapping to the reference

比对用STAR软件，RNA测序数据的特点简单点说断点太多太散，所以这里采用了用STAR软件比对后得到的junction结果重建参考序列进行二次比对以提高精度的思路。<font color='#FF3333'>（卧槽这句子好长，然而确实是自己造的中文句子，怎么会有好几个定语从句的英文翻译过来的既视感。）</font>

先建个STAR需要的参考基因组INDEX

	STAR --runMode genomeGenerate --genomeDir 'genome_dir_path' --genomeFastaFiles hg38.fa --runThreadN <int>

	cd 'run_dir_path' `

第一次比对

	STAR --genomeDir 'genome_dir_path' --readFilesIn fq_1.fq fq_2.fq --runThreadN <int> 

得到的结果中有一个'SJ.out.tab'文件，加进参考基因组重新做一下INDEX。

	STAR --runMode genomeGenerate --genomeDir 'genome_dir_path_new' --genomeFastaFiles hg38.fa --sjdbFileChrStartEnd 'SJ.out.tab' --sjdbOverhang 75 --runThreadN <int>

第二次比对
	
	` cd 'run_dir_path_new' 

	STAR --genomeDir 'genome_dir_path_new' --readFilesIn fq_1.fq fq_2.fq --runThreadN <int> 

生成.SAM文件，下面要用。

## Add read groups, sort, mark duplicates, and create index

需要使用picard软件，GATK4已整合picard功能。

不过老爷车上装了picard，就这么废弃了多可惜，我决定用原版的picard。

	java -jar picard.jar AddOrReplaceReadGroups I=STAR_output.sam O=rg_added_sorted.bam SO=coordinate

	RGID=id RGLB=library RGPL=platform RGPU=machine RGSM=sample

这步生成1个文件：

* rg\_added\_sorted.bam

	java -jar picard.jar MarkDuplicates I=rg_added_sorted.bam O=dedupped.bam CREATE_INDEX=true

	VALIDATION_STRINGENCY=SILENT M=output.metrics

这步生成3个文件：

* dedupped.bam

* dedupped.bai

* output.metrics


这两步干啥的看字面意思也能理解吧，不然可以看看文首的原博。

## Split 'N' Trim and reassign mapping qualities

接下来用GATK中的SplitNCigarReads工具。

用之前需要对hg38.fq做INDEX处理。使用samtools和GATK4中的CreatSequenceDictionary工具。

<font color='#FF3333'><del>玛德好久前的笔记了，当时竟然没写这段。懒得找了，当个坑回头填吧。</del></font>

好了~就当无事发生~可以直接用GATK了~

	GATK4 SplitNCigarReads -R hg38.fa -I dedupped.bam -O split.bam

生成2个文件：

* split.bam

* split.bai

## Variant calling

	GATK4 HaplotypeCaller -R hg38.fa -I split.bam --dont-use-soft-clipped-bases true -stand-call-conf 20.0 -O output.vcf 

生成2个文件：

* output.vcf

* output.vcf.idx

好了，省了一个结果过滤步骤，到这就结束了。

## Annovar注释

后续可以配合Annovar软件对VCF结果文件做注释，大概是这两下。

	perl ./annovar/convert2annovar.pl -format vcf4 output.vcf > res.avinput 

	perl ./annovar/table_annovar.pl res.avinput ./annovar/humandb/ -buildver hg38 -out res.note -protocol refGene -operation g

简单的注释就完成了。

更多内容参见[Annovar官网](http://annovar.openbioinformatics.org/en/latest/)。

##

对应的写了流程脚本，翻了半天终于找到了，不知道还能不能用。

不足之处还请指出，欢迎互相学习交流。

我的邮箱：[zhangchengsheng1@qq.com](http://mail.qq.com)。
