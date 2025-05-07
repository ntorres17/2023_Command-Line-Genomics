(base) ntorres1@teachingserver:/media/Scratch8TB/CLG2023/ntorres1/Human_NUMTs$ cat README.txt 
1. mkdir Human_NUMTs
2. wget https://ftp.ensembl.org/pub/release-110/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
3. wget https://ftp.ensembl.org/pub/release-110/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.chromosome.MT.fa.gz
4. gzip -d Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
   gzip -d Homo_sapiens.GRCh38.dna.chromosome.MT.fa.gz    
5. makeblastdb -in Homo_sapiens.GRCh38.dna.primary_assembly.fa -dbtype nucl
6. blastn -num_threads 2 -query Homo_sapiens.GRCh38.dna.chromosome.MT.fa -db Homo_sapiens.GRCh38.dna.primary_assembly.fa -outfmt 6 -num_alignments 100 -out Mt_Hum_nuc.blast.out
7a. 183 matches;  wc -l Mt_Hum_nuc.blast.out > nuclear_mito_matches.txt
7b. 1; awk '$2=="MT"' Mt_Hum_nuc.blast.out > mito-mito_matches.txt
7c. awk '$4>=1000' Mt_Hum_nuc.blast.out |wc -l > nuclear_mito_1000bp_matches.txt
7d. awk '$3>="1000"' Mt_Hum_nuc.blast.out |wc -l > nuclear_mito_1000bp_75per_matches.txt
7e. awk '$4>="1000"' Mt_Hum_nuc.blast.out |awk '$3>="1000"' Mt_Hum_nuc.blast.out > nuclear_mito_1000bp_75per_matches_results.out
 