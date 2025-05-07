(base) ntorres1@teachingserver:/media/Scratch8TB/CLG2023/ntorres1/Quiz-final$ cat README.txt 
#Part A:

#1: Other options to access Linux command line for research: Cyverse, amaazon (costs money) and NMSU - discovery/joker servers 
#2: Tools to check quality of fastq: Trimmomatic or fastqc
#3: How to check data provided by Illumina are correct: Check their total reas, both files should have the same number of reads 
#4: What does Trimmomatic solve?: Removal of adapters and filters for quality

#Part B: 
#1: 
#HQ659643 HQ659644 HQ197392 HQ197396 HQ197395 HQ197391 HQ197390 HQ659647 HQ659645  HQ659646 HQ659649 HQ659648 HQ659650 HQ197386 HQ197387 HQ197388 HQ197389 HQ197394 HQ197393 HQ197397 HQ659653 HQ659652 HQ659651

for i in HQ659643 HQ659644 HQ197392 HQ197396 HQ197395 HQ197391 HQ197390 HQ659647 HQ659645  HQ659646 HQ659649 HQ659648 HQ659650 HQ197386 HQ197387 HQ197388 HQ197389 HQ197394 HQ197393 HQ197397 HQ659653 HQ659652 HQ659651
 
        do curl "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=n>
done

#2. Got stumped on this one! I know its something but couldn't isolate the column, below are my attempts. 

awk '$8=="^RAxML_bestTree.STRG."' space_delimited_table.txt > file_names_extracted.txt 

grep ^RAxML space_delimited_table.txt | cut -f8 space_delimited_table.txt > file_names_extracted.txt

seqtk subseq space_delimited_table.txt RAxML_bestTree.STRG.36640.1 > test.txt 