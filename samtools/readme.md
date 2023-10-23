### 231023
## mapping -> sort -> markdup
```
samtools - dedup 방법
/TBI/Share/HumanTeam/BioPipeline/gatk4_pipeline/Tools/bwa-0.7.17/bwa mem -aM -R '@RG\tID:TN2308D1240\tSM:TN2308D1240\tPL:illumina' -t 8 -k 45 /TBI/Share/HumanTeam/BioResource/hg19/hg19.fa test_1.fastq.gz test_2.fastq.gz | samtools view -Sb -F 0x100 - | samtools sort -n - > test_sort.bam
samtools fixmate -m test_sort.bam - | samtools sort -o positionsort.bam -
samtools markdup -r -s -f markdup_stat.txt positionsort.bam markdup.bam


fixmate 까지 한 줄로
/TBI/Share/HumanTeam/BioPipeline/gatk4_pipeline/Tools/bwa-0.7.17/bwa mem -aM -R '@RG\tID:TN2308D1240\tSM:TN2308D1240\tPL:illumina' -t 8 -k 45 /TBI/Share/HumanTeam/BioResource/hg19/hg19.fa test_1.fastq.gz test_2.fastq.gz | samtools view -Sb -F 0x100 - | samtools sort -n - | samtools fixmate -m - - | samtools sort -o positionsort.bam -


markdup 까지 한 줄로
/TBI/Share/HumanTeam/BioPipeline/gatk4_pipeline/Tools/bwa-0.7.17/bwa mem -aM -R '@RG\tID:TN2308D1240\tSM:TN2308D1240\tPL:illumina' -t 8 -k 45 /TBI/Share/HumanTeam/BioResource/hg19/hg19.fa test_1.fastq.gz test_2.fastq.gz | samtools view -Sb -F 0x100 - | samtools sort -n - | samtools fixmate -m - - | samtools sort -o - - | samtools markdup -r -s -f markdup_stat.txt - markdup.bam
```  
### <br/><br/><br/>
