# hse22_hw1
* Создаем ярлыки
```
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
```
* Устанавливаем сиды и выбираем сэмплы
```
seqtk sample -s514 oil_R1.fastq 5000000 > sub1.fastq
seqtk sample -s514 oil_R2.fastq 5000000 > sub2.fastq
seqtk sample -s514 oilMP_S4_L001_R1_001.fastq 1500000 > matepairs.fastq
seqtk sample -s514 oilMP_S4_L001_R2_001.fastq 1500000 > matepairs2.fastq
```
* Оцениваем качество
```
mkdir fastqc
ls sub* matepairs* | xargs -tI{} fastqc -o fastqc {}
mkdir multiqc
multiqc -o multiqc fastqc
```
* Подрезаем
```
platanus_trim sub*
platanus_internal_trim matepair*
```
* Оцениваем качество после подрезаний
```
mkdir fastqc_trim
ls sub* matepairs*| xargs -tI{} fastqc -o fastqc_trim {}
mkdir multqctrim
multiqc -o multqctrim fastqc_trim
```
* Собираем контиги
 ```
 time platanus assemble -o Poil -f sub1.fastq.trimmed sub2.fastq.trimmed 2> assemble.log
 ```
 * Собираем скаффолды 
 ```
 time platanus scaffold -o Poil -c Poil_contig.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 matepairs.fastq.int_trimmed matepairs2.fastq.int_trimmed 2> scaffold.log
 ```
 * Уменьшаем гэпы
 ```
 time platanus gap_close -o Poil -c Poil_scaffold.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 matepairs.fastq.int_trimmed  matepairs2.fastq.int_trimmed 2> gapclose.log
 ```
 * jupyter notebook - https://github.com/tsessk/hse22_hw1/blob/master/src/hw1.ipynb

![general](https://github.com/tsessk/hse22_hw1/blob/master/general.png)
![per_seq](https://github.com/tsessk/hse22_hw1/blob/master/per_seq_qs.png)
