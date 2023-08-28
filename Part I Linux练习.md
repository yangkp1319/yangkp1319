## Part I Linux练习

+ 2.1

  1. 对于示例文件（test_command.gtf），尝试使用相关命令或命令组合分别统计文件的行数以及字符数。

     **`wc -l test_command.gtf`**

     > ​	8 test_command.gtf

     **`wc -m test_command.gtf`**

     > ​	636 test_command.gtf

  2. 利用 `grep` 等命令尝试筛选并输出示例文件中以 chr_ 起始，并且基因id为 YDL248W 的行。

     **`grep chr_ test_command.gtf | grep YDL248W`**
     
     >chr_IV  ensembl gene    1802    2953    .       +       .       gene_id "YDL248W"; gene_version "1";
     >chr_IV  ensembl transcript      802     2953    .       +       .       gene_id "YDL248W"; gene_version "1";
     >chr_IV  ensembl start_codon     1802    1804    .       +       0       gene_id "YDL248W"; gene_version "1";

  3. 利用 `sed` 等命令将示例文件中的 chr_ 替换为 chromosome_ 并输出每行的第1，3，4，5列。（无需改动原文件，只输出结果）

     **`sed 's/chr_/chromosome_/g ' test_command.gtf | awk '{print $1,$3,$4,$5}'`**
     
     > chromosome_IV gene 1802 2953
     >chromosome_IV transcript 802 2953
     > chromosome_IV exon 1802 2953
     > chromosome_IV CDS 1802 950
     > chromosome_IV start_codon 1802 1804
     > chromosome_IV stop_codon 2951 2953
     > chromosome_IV gene 762 3836
     > chromosome_IV transcript 3762 836

  4. 通过`man`命令以及更多的资料学习简单的 `awk` 命令，尝试互换示例文件的第2列和第3列，并且对输出结果利用 `sort` 命令依照第4和第5列数字大小排序，将最终结果输出到result.gtf文件中。

     **`awk '{temp=$2;$2=$3;$3=temp;print $0}' test_command.gtf | sort -n -k 4 -k 5 > result.gtf`**
     
     > chromosome_IV gene ensembl 762 3836 . + . gene_id "YDL247W-A"; gene_version "1";
     >chr_IV transcript ensembl 802 2953 . + . gene_id "YDL248W"; gene_version "1";
     > chromosome_IV CDS ensembl 1802 950 . + 0 gene_id "YDL248W"; gene_version "1";
     > chr_IV start_codon ensembl 1802 1804 . + 0 gene_id "YDL248W"; gene_version "1";
     > chr_IV gene ensembl 1802 2953 . + . gene_id "YDL248W"; gene_version "1";
     > chromosome_IV exon ensembl 1802 2953 . + . gene_id "YDL248W"; gene_version "1";
     > chromosome_IV stop_codon ensembl 2951 2953 . + 0 gene_id "YDL248W"; gene_version "1";
     > chr_IV transcript ensembl 3762 836 . + . gene_id "YDL247W-A"; gene_version "1";

  5. 更改示例文件的权限，使得文件所有者及所在用户组用户可读、写、执行而其他用户只可读，展示权限修改前后的权限变化。

     **`ls -lh test_command.gtf`**
     
     > -rwxrwxrwx 1 test test 636 Aug 24 09:33 test_command.gtf   
     
     **`chmod 774 test_command.gtf`**
     
     **`ls -lh test_command.gtf`**
     
     > -rwxrwxr-- 1 test test 636 Aug 24 09:33 test_command.gtf

  

+ 2.2

  1. 列出1.gtf文件中 XI 号染色体上的后 10 个 CDS （按照每个CDS终止位置的基因组坐标进行sort）。

     **`awk '$1=="XI" && $3=="CDS"{print $0}' 1.gtf | sort -n -k 5 | tail -10`**

     > XI      ensembl CDS     631152  632798  .       +       0       gene_id "YKR097W"; gene_version "1"; transcript_id "YKR097W"; transcript_version "1"; exon_number "1"; gene_name "PCK1"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "PCK1"; transcript_source "ensembl"; transcript_biotype "protein_coding"; protein_id "YKR097W"; protein_version "1";
     > XI      ensembl CDS     633029  635179  .       -       0       gene_id "YKR098C"; gene_version "1"; transcript_id "YKR098C"; transcript_version "1"; exon_number "1"; gene_name "UBP11"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "UBP11"; transcript_source "ensembl"; transcript_biotype "protein_coding"; protein_id "YKR098C"; protein_version "1";
     > XI      ensembl CDS     635851  638283  .       +       0       gene_id "YKR099W"; gene_version "1"; transcript_id "YKR099W"; transcript_version "1"; exon_number "1"; gene_name "BAS1"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "BAS1"; transcript_source "ensembl"; transcript_biotype "protein_coding"; protein_id "YKR099W"; protein_version "1";
     > XI      ensembl CDS     638904  639968  .       -       0       gene_id "YKR100C"; gene_version "1"; transcript_id "YKR100C"; transcript_version "1"; exon_number "1"; gene_name "SKG1"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "SKG1"; transcript_source "ensembl"; transcript_biotype "protein_coding"; protein_id "YKR100C"; protein_version "1";
     > XI      ensembl CDS     640540  642501  .       +       0       gene_id "YKR101W"; gene_version "1"; transcript_id "YKR101W"; transcript_version "1"; exon_number "1"; gene_name "SIR1"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "SIR1"; transcript_source "ensembl"; transcript_biotype "protein_coding"; protein_id "YKR101W"; protein_version "1";
     > XI      ensembl CDS     646356  649862  .       +       0       gene_id "YKR102W"; gene_version "1"; transcript_id "YKR102W"; transcript_version "1"; exon_number "1"; gene_name "FLO10"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "FLO10"; transcript_source "ensembl"; transcript_biotype "protein_coding"; protein_id "YKR102W"; protein_version "1";
     > XI      ensembl CDS     653080  656733  .       +       0       gene_id "YKR103W"; gene_version "1"; transcript_id "YKR103W"; transcript_version "1"; exon_number "1"; gene_name "NFT1"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "NFT1"; transcript_source "ensembl"; transcript_biotype "protein_coding"; protein_id "YKR103W"; protein_version "1";
     > XI      ensembl CDS     656836  657753  .       +       0       gene_id "YKR104W"; gene_version "1"; transcript_id "YKR104W"; transcript_version "1"; exon_number "1"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "YKR104W"; transcript_source "ensembl"; transcript_biotype "protein_coding"; protein_id "YKR104W"; protein_version "1";
     > XI      ensembl CDS     658719  660464  .       -       0       gene_id "YKR105C"; gene_version "1"; transcript_id "YKR105C"; transcript_version "1"; exon_number "1"; gene_name "VBA5"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "VBA5"; transcript_source "ensembl"; transcript_biotype "protein_coding"; protein_id "YKR105C"; protein_version "1";
     > XI      ensembl CDS     661442  663286  .       +       0       gene_id "YKR106W"; gene_version "1"; transcript_id "YKR106W"; transcript_version "1"; exon_number "1"; gene_name "GEX2"; gene_source "ensembl"; gene_biotype "protein_coding"; transcript_name "GEX2"; transcript_source "ensembl"; transcript_biotype "protein_coding"; protein_id "YKR106W"; protein_version "1";

  2. 统计 IV 号染色体上各类 feature （1.gtf文件的第3列，有些注释文件中还应同时考虑第2列） 的数目，并按升序排列。

     **`awk '$1=="IV"{print $3}' 1.gtf | sort | uniq -c | sort -n -k 1`**
     
     >​    853 start_codon
     >​    853 stop_codon
     >​    886 gene
     >​    886 transcript
     >​    895 CDS
     >​    933 exon

  3. 寻找不在 IV 号染色体上的所有负链上的基因中最长的2条 CDS 序列，输出他们的长度。

     **`awk '$1!="IV" && $7=="-" && $3=="CDS"{print $5-$4+1}' 1.gtf | sort -n | tail -2`**
     
     >12276
     >14730

  4. 寻找 XV 号染色体上长度最长的5条基因，并输出基因 id 及对应的长度。

     **`awk '$1=="XV" && $3=="gene"{gsub("\"","",$10);print $10,$5-$4+1}' 1.gtf | sort -n -k 2 | tail -5`**
     
     > YOR142W-B; 5269
     >YOR192C-B; 5314
     > YOR343W-B; 5314
     > YOR396W; 5391
     > YOL081W; 9240

  5. 统计1.gtf列数

     **`awk 'END{print NF}' 1.gtf`**
     
     > 28

+ 2.3 

  1. 参考和学习本章内容，写出一个 bash 脚本，可以使它自动读取一个文件夹（例如bash_homework/）的内容，将该文件夹下文件的名字输出到 filenames.txt, 子文件夹的名字输出到 dirname.txt 。

     **`vi scan.sh`**

     > #!/bin/bash
     > #自动读取一个文件夹的内容，将该文件夹下文件的名字输出到 filenames.txt, 子文件夹的名字输出到 dirname.txt
     >
     > #查看文件夹结果并保存变量中
     > dir=`ls`
     > for val in $dir;do
     >         if [ -f $val ];then #判断是否为文件
     >                 echo $val >> /home/test/linux/filenames.txt
     >         elif [ -d $val ];then #判断是否为文件夹
     >                 echo $val >> /home/test/linux/dirname.txt
     >         fi
     > done
     > exit 0

     *运行脚本 *

     **`/home/test/linux/scan.sh`**

     **`cat filenames.txt`**

     >a1.txt
     >a.txt
     >b1.txt
     >bam_wig.sh
     >b.filter_random.pl
     >c1.txt
     >chrom.size
     >c.txt
     >d1.txt
     >dir.txt
     >e1.txt
     >f1.txt
     >human_geneExp.txt
     >if.sh
     >image
     >insitiue.txt
     >mouse_geneExp.txt
     >name.txt
     >number.sh
     >out.bw
     >random.sh
     >read.sh
     >test3.sh
     >test4.sh
     >test.sh
     >test.txt
     >wigToBigWig

     **`cat dirname.txt`**

     > news
     > a-docker
     > app
     > backup
     > bin
     > biosoft
     > c1-RBPanno
     > datatable
     > db
     > download
     > e-annotation
     > exRNA
     > genome
     > git
     > highcharts
     > home
     > hub29
     > ibme
     > l-lwl
     > map2
     > mljs
     > module
     > mogproject
     > node_modules
     > perl5
     > postar2
     > postar_app
     > postar.docker
     > RBP_map
     > rout
     > script
     > script_backup
     > software
     > tcga
     > test
     > tmp
     > tmp_script
     > var
     > x-rbp

+ 