## fasta format
在生物信息学中，**FASTA格式**是用来记录核酸序列或者肽序列的文本格式，其中的核酸或氨酸均以单个字母编码呈现。

#### 格式
FASTA格式中的一条完整序列，包含开头的单个名称描述行和多个序列数据行。每一行字符数通常不超过80字符。

#### 描述行
行首以`>`开头，用于和数据行区分。`>`后面为序列标识符，该行剩余部分为描述部分。
序列标识符SeqID在`NCBI FASTA`定义的行的格式：
数据库|格式
------|-----
GenBank|gb\|accession\|locus
EMBL Data Library|emb\|accession\|locus
DDBJ, DNA Database of Japan|dbj\|accession\|locus
NBRF PIR|pir\|\|entry
Protein Research Foundation|	prf\|\|name
SWISS-PROT|sp\|accession\|entry name
Brookhaven Protein Data Bank|pdb\|entry\|chain
Patents|pat\|country\|number
GenInfo Backbone Id|bbs\|number
General database identifier|gnl\|database\|identifier
NCBI Reference Sequence|ref\|accession\|locus
Local Sequence identifier|lcl\|identifier

  
#### 数据行
序列可以表示蛋白质序列或者核酸序列，以标准的IUB/IUPAC氨酸和核酸编码表达：
* 核酸编码：
  * A 腺嘌呤(Adenine)
  * C 胞嘧啶(Cytosine)
  * G 鸟嘌呤(Guanine)
  * T 胸腺嘧啶(Thymine)
  * U 尿嘧啶（Uracil)
  * R 嘌呤(puRine)即A、G
  * Y 嘧啶(pYrimidines)即C、T、U
  * K 酮基(Kntones) 即G、T、U
  * M 氨基(aMino) 即A、C
  * S 强(Strong)结合力 即C、G
  * W 弱(Weak)结合力 即A、T、U
  * B 非A（如C、G、T、U)(A后边为B)
  * D 非C (如A、G、T、U)(C后边为D)
  * H 非G (如A、C、T、U)(G后边为H)
  * V 非T非U(如A、C、G)(U后边为V)
  * N 即A、C、G、T、U (任意核酸Nucleic acid)
  * \- 不定长度空白占位符   
* 氨酸编码：
  * A 丙氨酸（Alanine）
  * B 天冬氨酸（Aspartic acid，D）或天冬酰胺（Asparagine，N）
  * C 半胱氨酸（Cysteine）
  * D 天冬氨酸（Aspartic acid）
  * E 谷氨酸（Glutamic acid）
  * F 苯丙氨酸（Phenylalanine）
  * G 甘氨酸（Glycine）
  * H 组氨酸（Histidine）
  * I 异亮氨酸（Isoleucine）
  * J 亮氨酸（Leucine，L）或异亮氨酸（Isoleucine，I）
  * K 赖氨酸（Lysine）
  * L 亮氨酸（Leucine）
  * M 甲硫氨酸（Methionine）
  * N 天冬酰胺（Asparagine）
  * O 吡咯赖氨酸（Pyrrolysine）
  * P 脯氨酸（Proline
  * Q 谷氨酰胺（Glutamine）
  * R 精氨酸（Arginine）
  * S 丝氨酸（Serine）
  * T 苏氨酸（Threonine）
  * U 硒半胱氨酸（Selenocysteine
  * V 缬氨酸（Valine）
  * W 色氨酸（Tryptophan）
  * Y 酪氨酸（Tyrosine）
  * Z 谷氨酸（Glutamic acid，E）或谷氨酰胺（Glutamine，Q）
  * X 任意
  * \* 翻译终止
  * \- 不定长度空白占位符

#### 扩展名
扩展名|含义|备注
------|----|----
fasta (.fas)|普通FASTA|任意普通的FASTA文件；此类扩展名还有fa、seq、fsa
fna|核酸FASTA|普遍用于表示核酸序列的FASTA文件
ffn|核酸编码区FASTA|包含基因组编码区的FASTA文件
faa|氨酸FASTA|包含表示氨酸序列的FASTA文件。含有多种蛋白质序列的FASTA文件还可使用更具体的mpfa扩展名
frn|非编码RNA FASTA|包含以DNA字母编码表示的基因组非编码RNA区（如tRNA、rRNA）的FASTA文件