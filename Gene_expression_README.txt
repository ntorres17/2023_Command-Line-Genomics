
(base) ntorres1@teachingserver:/media/Scratch8TB/CLG2023/ntorres1/Danio_expression$ cat README.txt 
1. mkdir Danio_expression, touch README.txt
  #This project will explore gene expression variation during Zebrafish development. We will
compare gene expression at the 2 cell embryo (ca. 45 minutes post fertilization) vs. the gastrula
stage embryo (harvested at 6 hours) stages.
#some of the ideas behind this example project and the RNA-seq data derive from -
https://www.ebi.ac.uk/training/online/course/ebi-next-generation-sequencing-practical-
course/rna-sequencing/rna-seq-analysis-transcriptome
   mkdir Danio_gene ##anio_genome ## this will store the genome, annotations, and star-index files for searching
   mkdir Danio_2cell_RNA ## this will store the Illumina F+R RNA-seq files for the 2cell stage embryo
data.
   mkdir Danio_6hr_RNA ## this will store the Illumina F+R RNA seq files for the 6h embryo (gastrula)

2. cd Danio_Genome 
   wget https://ftp.ensembl.org/pub/release-110/fasta/danio_rerio/dna/Danio_rerio.GRCz11.dna.primary_assembly.fa.gz
   gzip -d Danio_rerio.GRCz11.dna.primary_assembly.fa.gz
   mv Danio_rerio.GRCz11.dna.primary_assembly.fa GRCz11.fa
#Questions related to Fasta file   
   1) grep ">" GRCz111.fa | wc - l #993
   2) grep -v ">" GRCz111.fa | wc -l #22891687
   3)  grep "^>" GRCz11.fa| sort | uniq -c #chromosomes and scaffolts
3. wget https://ftp.ensembl.org/pub/release-110/gtf/danio_rerio/Danio_rerio.GRCz11.110.chr.gtf.gz
   gzip -d Danio_rerio.GRCz11.110.chr.gtf.gz
 # 1) 9 columns; seqname, source, feature, start, end, score, strand, frame, attributes 
 # 2) grep -v "#" Danio_rerio.GRCz11.110.chr.gtf | wc -l #1153784
 # 3) grep -v "#" Danio_rerio.GRCz11.110.chr.gtf | cut -f3| sort | uniq -c
 # 419352 CDS
 # 481079 exon
 # 48633 five_prime_utr
 # 32057 gene
 # 55 Selenocysteine
 # 39561 start_codon
 # 39242 stop_codon
 # 34515 three_prime_utr
 # 59290 transcript#
4. 
#Danio_2cell_RNA
   wget    ftp://ftp.ebi.ac.uk/pub/training/Train_online/RNA-seq_exercise/2cells*
  # How many reads in each: 159524654
  # They are paired-end reads per their names .1 and .2. for Forward/Reverse 
#Danio_6hr_RNA   
   wget   ftp://ftp.ebi.ac.uk/pub/training/Train_online/RNA-seq_exercise/6*
   #How many reads in each: 169444913
   #They are also paired end reads. 
5. 
STAR --runThreadN 2 --genomeDir Danio_genome/ --readFilesIn Danio_2cell_RNA/2cells_1.fastq
Danio_2cell_RNA/2cells_2.fastq --outSAMtype BAM SortedByCoordinate --outFileNamePrefix 2cell

STAR --runThreadN 2 --genomeDir Danio_genome/ --readFilesIn Danio_6hr_RNA/6h_1.fastq
Danio_6hr_RNA/6h_2.fastq --outSAMtype BAM SortedByCoordinate --outFileNamePrefix 6hr

6. 2cell: 
#Attempt to reads: 786742
#Uniquely mapped 95.24%
#Percent of unmapped reads: 3.91%

6hr 
##Attempt to reads: 835648
#Uniquely mapped 90.14%
#Percent of unmapped reads: 5.32%

#It appears that the 2cell has better data from the % of uniquely mapped reads. Meaning more reads were matched or mapped to the genome. And there was only a 3.91% of unmapped reads. 

 
7. stringtie 2cellAligned.sortedByCoord.out.bam -G Danio_genome/Danio_rerio.GRCz11.110.chr.gtf -o stringtie2cell.gtf -p 1
   stringtie 6hrAligned.sortedByCoord.out.bam -G Danio_genome/Danio_rerio.GRCz11.110.chr.gtf -o stringtie6hr.gtf -p 1

8. nano gtf_paths.txt
   stringtie2cell.gtf
   stringtie6hr.gtf

stringtie --merge -p 1 -o stringtie_merged.gtf -G Danio_genome/Danio_rerio.GRCz11.110.chr.gtf gtf_paths.txt

#Lession 11 - RNA-seq

#cufflink: 
cuffdiff  --library-type  fr-unstranded -o  Cuffdiffout  -L  2cell,6hour   stringtie_merged.gtf  2cellAligned.sortedByCoord.out.bam   6hrAligned.sortedByCoord.out.bam

HOw many genes were considered in this comparison (one gene per line in file)? wc -l gene_exp.diff #32,199
How many genes returned a significant result (they are reported as differently expressed) in this file #grep "yes" gene_exp.diff