## BIOINFORMATICS 

#### genome file format
* FASTA format: assembled genomes.
* FASTQ format: sequencing datasets.

#### [ncbi genomes/refseq/](https://ftp.ncbi.nlm.nih.gov/genomes/all/README.txt)
其中的内容包含：组装基因序列和RefSeq的注释。所有的原核生物和真核生物基因都被注释。其中包含以下几项：
* archaea 古生菌
* bacteria 细菌
* fungi 真菌
* invertebrate 无脊椎动物
* metagenomes 宏基因组（所有微生物菌群基因组的总和）
* other - this derectory includes synthetic genomes 包含合成基因
* plant 植物
* protozoa 无脊椎原生动物
* vertebrate_mammalian 有脊椎哺乳动物
* vertebrate_other 有脊椎其他动物
* viral 病毒

#### 通过assembly得到的基因序列或者其他数据的文件文件命名规则：
assemblyAccession.version_assemblyName_contentType.optional.format
其中文件格式和内容如下：
* *.genomic.fna.gz file 有关组装基因序列的FASTA format文件。有关真核生物的重复基因内容标记为小写字母。序列题目包含：sequence accession, version和description。genomic.fna.gz文件包含所有的顶级组装序列：
  * chromosomes 染色体
  * plasmids 质粒
  * organelles 细胞器
  * unlocalized scaffolds 未本地化的（蛋白质）支架
  * unplaced scaffolds 未定位的（蛋白质）支架
  * any alternate loci or patch scaffolds 任意可替换基因位点或补丁支架
  其中为染色体的一部分的蛋白质支架不在文件中，因为已经是染色体的冗余部分了。对于已经定位了的支架序列在assembly_structure/目录下。