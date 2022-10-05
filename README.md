# hse22_hw1
* Создание ярлыков 
```
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
```
* Установка сида и выбор сэмплов
```
seqtk sample -s514 oil_R1.fastq 5000000 > sub1.fastq
seqtk sample -s514 oil_R2.fastq 5000000 > sub2.fastq
seqtk sample -s514 oilMP_S4_L001_R1_001.fastq 1500000 > matepairs.fastq
seqtk sample -s514 oilMP_S4_L001_R2_001.fastq 1500000 > matepairs2.fastq
```
