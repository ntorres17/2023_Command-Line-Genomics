(base) ntorres1@teachingserver:/media/Scratch8TB/CLG2023/ntorres1/Oryza_NUMTs$ cat README.txt 
#Rice NUMTs
2. copy address from website, wget https://ftp.ebi.ac.uk/ensemblgenomes/pub/release-51/plants/fasta/oryza_sativa/dna/Oryza_sativa.IRGSP-1.0.dna.toplevel.fa.gz
   gzip -d Oryza_....gz
3. grep "^>" Oryza_sativa.IRGSP-1.0.dna.toplevel.fa > fasta_sequence_names.txt
4. grep ">Mt dna:chromosome chromosome:IRGSP-1.0:Mt:1:490520:1 REF"  fasta_sequence_names.txt > mito.name.txt
   sed 's/^>//g' mito.name.txt > mito.name.txt 
5. seqtk subseq Oryza_sativa.IRGSP-1.0.dna.toplevel.fa mito.name.txt > Mito_genome.fasta 
6. cat Mito_genome.fasta
7. makeblastdb -in Oryza_sativa.IRGSP-1.0.dna.toplevel.fa -dbtype nucl
8. blastn -query Mito_genome.fasta -db Oryza_sativa.IRGSP-1.0.dna.toplevel.fa -outfmt 6 -num_alignments 100 -out Rice_NUMTs_blast.out
9. awk '$2!="Mt"' Rice_NUMTs_blast.out | wc -l > result.txt #4192
10. grep "Mt" Rice_NUMTS_blast.out | cut -f2 |sort | uniq -c >> result.txt
13. (awk '$2==12 {sum+=$4;}END{print sum;}' Rice_NUMTS_blast.out >> result.txt
14. grep -v ">" Mito_genome.fasta | tr -d '\n' | wc -m >> result.txt 
15. 91% but seems really high? 