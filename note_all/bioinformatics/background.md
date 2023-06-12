# background for bioinformatics

## key words
### [Resolving the complexity of the human genome using single-molecule sequencing](https://www.nature.com/articles/nature13907)
* single-molecule, real-time (SMRT) 
    * average mapped read length = 5.8 kb
    * human GRCh37 reference genome
* haploid human genome (CHM1) 

## biological replicates VS technical replicates
Arised from SRA dump tool: fastq-dump --skip-technical optional

实验重复还可以进一步细分为生物重复(biological replicates)和技术重复(technical replicates):  
生物重复：指对同一个处理组中独立来源的重复样本分别进行独立分析，是整个实验的完全重复，如将具有同一基因型的多个细胞株进行独立地测定。由于遗传和环境等因素的影响会引起有机体的个体差异，因此需要采用生物重复的实验设计方法来消除该差异。目前都以3次生物学重复实验设计为主，要求严格的实验可以做5次重复。  

技术重复：指对同一样本进行重复地检测分析，例如同一份细胞中抽提的蛋白质进行三次质谱检测，或者对同一RNA-seq样本测序3次。与生物学重复相比，技术重复的测量变异程度较小，从而可以减少实验中的分析变异，将对同一份样本产生高重复性的测量结果 。
简单来讲，生物重复是生物级别的重复，一般都是生物样本的重复。而技术重复，更多的是参数测定环节的重复，一般是对同一生物样本进行多次测定。
[reference](https://www.jianshu.com/p/8ebda3495c4a)

## SRA数据下载（通过EBI-ENA数据库，使用ASpera）
NCBI SRA 数据库，全称(Sequence Read Archive)数据库，是测序数据（一般为fastq格式）文件的一种二进制压缩格式，可以通过SRA tools `prefetch` 下载，然后通过 `fastq-dump`格式化成为fastq格式的序列文件。具体的SRA tools 软件包下载地址为：[SRA toolkit](https://github.com/ncbi/sra-tools/wiki/01.-Downloading-SRA-Toolkit)

除了通过SRA tools下载SRA数据库，还可以通过Aspera工具通过EBI-ENA数据库直接下载相关的fastq格式文件。
因为Aspera connect 可以有更好的下载带宽 [aspera download case](https://www.jianshu.com/p/2987843d97e3)。

Aspera工具的安装方法见:[install Aspera](https://www.jianshu.com/p/fed19a8821eb), 个人尝试了使用conda安装比较简单，从官方网站下载的安装包，安装完成后没有公钥文件(asperaweb_id_dsa.openssh)。

通过Aspera 下载SRA fastq文件的具体操作参照：[download fastq by Aspera](https://blog.csdn.net/weixin_44616693/article/details/113923881)。

## fast5 和 fastq格式的区别
* fast5：原始电信号文件，以.fast5为文件结尾。此文件既有测序得到的序列信息，还有甲基化修饰信息。经过basecall，MinKNOW2.2软件包中的Guppy软件可以将fast5文件转换得到fq文件，测序仪本身是带有这个basecall功能的。
* fastq：由fast5文件转换而来，以.fastq或.fq结尾，与二代格式一样，四行为一个单位，只不过序列要长很多，这是三代的一个优势。

参考链接：[fast5和fastq格式](https://zhuanlan.zhihu.com/p/137069950)