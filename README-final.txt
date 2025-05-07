Final Project: 

Lotus japonicus
Reference genome(contains MT and Chloro)(aka Target): Lj3.0_pseudomol.fna
contains: 
Chr0 - 6, chloroplast (chr C) and MT (chr M)
Annotation file: Lj3.0_gene_models.gff3
Plastids: Lj3.0_cDNA.ffn

MT (Query): Mito_genome.fasta
Ch (Query): Chloro_genome.fasta

########Answering questions if there are Mito  within nucleus - YES; Double insertion? ############
3) grep "^>" Lj3.0_pseudomol.fna > Fasta_seq.txt
   cat Fasta_seq.txt
4) grep ">Lj3.0_chrM Mitochondria"  Fasta_seq.txt > mito.name.txt 
5) sed  's/^>//g' mito.name.txt >  mito.name_tmp.txt
   mv mito.name_tmp.txt mito.name.txt
   #remove the > 
   cat mito.name.txt 
6) seqtk subseq Lj3.0_pseudomol.fna mito.name.txt > Lotus_mito_genome.fasta
   #if cat, let it run. 
7) makeblastdb -in Lj3.0_pseudomol.fna -dbtype nucl
8) blastn -query Lotus_mito_genome.fasta -db Lj3.0_pseudomol.fna -outfmt 6 -num_alignments 100 -out Lotus_NUMTs_blast.out 
9) awk '$2!="Lj3.0_chrM Mitochondria"' Lotus_NUMTs_blast.out | wc -l > Lotus_mito_result.txt #3218
 cat Lotus_mito_result.txt
 #gives results on number of hits excluding MT to MT; 3218
10) grep "Lj3.0_chrM" Lotus_NUMTs_blast.out | cut -f2 |sort | uniq -c >> Lotus_mito_result.txt
 cat Lotus_mito_result.txt
  #Mostly concentrated on Chr0; 1439
13) awk '$2=="Lj3.0_chr0" {sum+=$4} END {print sum;}' Lotus_NUMTs_blast.out >> Lotus_mito_result.txt 
 cat Lotus_mito_result.txt  
#Ok isolated the row of data for Chr0 and added up lengths then added that to Lotus_result.txt; 605854; This is the number
  #of MT bases in Chromosome 0. Now to compare against MT genome we created!
14) grep -v ">" Lotus_mito_genome.fasta | tr -d '\n' | wc -m >> Lotus_mito_result.txt
 cat Lotus_mito_result.txt
  #380861; Again similar to its legit size of Mito_genome.fasta using ll
15) 159%

###############Lets Visualize in IGV for MT##############
1) mkdir Chr0
2) cp Fasta_seq.txt Chr0
3) grep ">Lj3.0_chr0 Chr0" Fasta_seq.txt >> Chr0_sequence_name.txt
   sed 's/^>/ /g' chr0.name.txt > temp.txt
   mv temp.txt chr0.name.txt
4)seqtk subseq Lj3.0_pseudomol.fna Chr0_seq.name.txt > Chr0.fasta
5) cp Lotus_mito_genome.fasta Chr0
6) makeblastdb -in Lotus_mito_genome.fasta -dbtype nucl
7) blastn -query Chr0.fasta -db Lotus_mito_genome.fasta -outfmt 6 -num_alignments 100 -out Chr0_matches.mito.out
8) awk '$2=="Lj3.0_chrM" {sum+=$4} END {print sum;}' Chr0_matches.mito.out 
9) cut -f2,9-10 Chr0_matches.mito.out >> Chr0_matches.mito.out.bed
10) cp Lotus_mito_genome.fasta Lotus_mito_genome.for.IGV.fasta
11) Review of results from IGV, kinda helpful. Can see a thinner and thicker bar superimposed over another but can't 
    see more detail. Will show results live in class on Tuesday.


########Answering questions if there are organelle plastid Chloroplast within nucleus - YES############
3) grep "^>" Lj3.0_pseudomol.fna > Fasta_seq.txt
   cat Fasta_seq.txt
4) grep ">Lj3.0_chrC Chloroplast" Fasta_seq.txt > Chloro.name.txt  
5) sed  's/^>//g' Chloro.name.txt >  Chloro.name_tmp.txt
   mv Chloro.name_tmp.txt Chloro.name.txt
   cat Chloro.name.txt
6) seqtk subseq Lj3.0_pseudomol.fna Chloro.name.txt > Lotus_chloro_genome.fasta
  #if cat, let it run. 
7) makeblastdb -in Lj3.0_pseudomol.fna -dbtype nucl
8) nohup blastn -query Lotus_chloro_genome.fasta -db Lj3.0_pseudomol.fna -outfmt 6 -num_alignments 100 -out Lotus_NUPTs_blast.out &
  #taking a while, start other one 
9)awk '$2!="Lj3.0_chrC"' Lotus_NUPTs_blast.out | wc -l > Lotus_Chloro_result.txt
  cat Lotus_Chloro_result.txt  
  #gives results on number of hits excluding Chloro to Chloro; 2336 (will use this number in step 9) 
10)grep "Lj3.0_chrC" Lotus_NUPTs_blast.out | cut -f2 |sort | uniq -c >> Lotus_Chloro_result.txt
  cat Lotus_Chloro_result.txt   
  #again on Chr0 at 919
13) awk '$2=="Lj3.0_chr0" {sum+=$4} END{print sum;}' Lotus_NUPTs_blast.out >> Lotus_Chloro_result.txt
  cat Lotus_Chloro_result.txt
  #Ok isolated the row of data for Chr0 and added up lengths then added that to Lotus #278517
14) grep -v ">" Chloro_genome.fasta | tr -d '\n' | wc -m >> Lotus_Chloro_result.txt
  cat Lotus_Chloro_result.txt 
  #278517/150519 = 184.72%
15) 185% of chloroplast, more than the MT. 


###############Lets Visualize in IGV for Chloroplast##############
1) Use same directory as theyre both in Chr0 concentration 
2) cp Fasta_seq.txt Chr0
3) grep ">Lj3.0_chr0 Chr0" Fasta_seq.txt >> Chr0_sequence_name.txt
   sed 's/^>/ /g' chr0.name.txt > temp.txt
   mv temp.txt chr0.name.txt
4)seqtk subseq Lj3.0_pseudomol.fna Chr0_seq.name.txt > Chr0.fasta
5) cp Lotus_mito_genome.fasta Chr0
6) makeblastdb -in Chloro_genome.fasta -dbtype nucl
7) blastn -query Chr0.fasta -db Chloro_genome.fasta  -outfmt 6 -num_alignments 100 -out Chr0_matches.chloro.out
8) awk '$2=="Lj3.0_chrM" {sum+=$4} END {print sum;}' Chr0_matches.chloro.out
9) cut -f2,9-10 Chr0_matches.chloro.out >> Chr0_matches.chloro.out.bed
10) cp Chloro_genome.fasta Chloro_genome.for.IGV.fasta
11) Review of results from IGV, kinda helpful. Can see a thinner and thicker bar superimposed over another but can't
    see more detail. Will show results live in class on Tuesday.



#########################################################################################################################
#########################################################################################################################


Vicia faba
Reference genome:  GCA_948472305.1_Hedin2_genome_v1_genomic.fna
Annotation file: genomic.gff 
MT Genbank KC189947.1: KC189947.1.fna
Plastids Genbank KF042344.1: sequence.fasta

7) makeblastdb -in  GCA_948472305.1_Hedin2_genome_v1_genomic.fna -dbtype nucl
8) nohup blastn -query KC189947.1.fna -db  GCA_948472305.1_Hedin2_genome_v1_genomic.fna -outfmt 6 -num_alignments 100 -out VF_NUMTs_blast.out &
9) awk '$2=="KC189947.1" {sum+=$4} END{print sum;}' VF_NUMTs_blast.out > Vf_mito_result.txt
   cat Vf_mito_result.txt
   #0, none are in the same file so none to exclude as "MT!=MT"
10) grep "KC189947.1" VF_NUMTs_blast.out | cut -f2 |sort | uniq -c >> Vf_mito_result.txt
    cat Vf_mito_result.txt
   #Large concentration on 2389 OX451739.1 aka Chromosome 4, aka most with MT.
13) awk '$2=="KC189947.1" {sum+=$4} END{print sum;}' VF_NUMTs_blast.out >> Vf_mito_result.txt 
    cat Vf_mito_result.txt
   #Reviewing .out file there are NO hits under field 2.
14) grep -v ">" Vf_Mito_genome.fasta | tr -d '\n' | wc -m >> Vf_mito_result.txt
   cat Vf_mito_result.txt
   #Final results 0% which are consistent with previous steps/findings. This did not migrate into nucleus partially or completely. 0%
   #0 

########Do it again with Chloro!############

7) makeblastdb -in  GCA_948472305.1_Hedin2_genome_v1_genomic.fna -dbtype nucl
8) nohup blastn -query sequence.fasta -db  GCA_948472305.1_Hedin2_genome_v1_genomic.fna -outfmt 6 -num_alignments 100 -out VF_NUPTs_blast.out &
9) awk '$2=="KF042344.1" {sum+=$4} END{print sum;}' VF_NUPTs_blast.out >> Vf_chloro_result.txt
   #0, none are in the same file so none to exclude as "MT!=MT"
   cat Vf_chloro_result.txt
10) grep "KF042344.1" VF_NUPTs_blast.out | cut -f2 |sort | uniq -c >> Vf_chloro_result.txt
   cat Vf_chloro_result.txt
   #Large concentration on 1212 OX451739.1 aka Chromosome 4, aka most with MT.
13) awk '$2=="KF042344.1" {sum+=$4} END{print sum;}' VF_NUPTs_blast.out >> Vf_chloro_result.txt
   cat Vf_chloro_result.txt   
    #Reviewing .out file there are NO hits under field 2.
14) grep -v ">" Vf_Mito_genome.fasta | tr -d '\n' | wc -m >> Vf_chloro_result.txt
   cat Vf_chloro_result.txt
   #Final results 0% which are consistent with previous steps/findings. This did not migrate into nucleus partially or completely. 0%
   #0 
