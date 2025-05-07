(base) ntorres1@teachingserver:/media/Scratch8TB/CLG2023/ntorres1/Oryza_NUMTs/Chromosome_12$ cat README.txt 
2a. mkdir Chromosome_12
    nano README.txt
2b. cp fasta_sequence_names.txt Chromosome_12/
    grep ">12 dna:chromosome chromosome:IRGSP-1.0:12:1:27531856:1 REF" fasta_sequence_names.txt >> Chr12_sequence_name.txt
    sed 's/^>/ /g' chr12.name.txt > temp.txt
    mv temp.txt chr12.name.txt   
2c. cp Mito_genome.fasta Chromosome_12
2d. cd Chromosome_12
2e. makeblastdb -in Mito_genome.fasta -dbtype nucl
2f. blastn -query chromosome12.fasta -db Mito_genome.fasta -outfmt 6 -num_alignments 100 -out chromo12_matches_mito.out
3. (awk '$2=="Mt" {sum+=$4;}END{print sum;}' chromo12_matches_mito.out) #443637    
4. 443637
5b. cut -f2,9-10 chromo12_matches_mito.out >> chromo12_matches_mito.out.bed
6. cp Mito_genome.fasta Mito_genome.for.IGV.fasta 
7. done and done
8. works!
9. It is definitely present, its peppered around the entire length and although there are gaps it still isn't difficult to find.
