(base) ntorres1@teachingserver:/media/Scratch8TB/CLG2023/ntorres1/Phylogeny$ cat README.txt 
Linux Lesson 12 - 

1. touch README.txt
4. nano accessions_table.txt, copied from PDF, pasted into file
7. sed 's/ AB/\tAB/g' accessions_table.txt | cut -f2 > identifiers_column.txt
8. sed -z 's/\n/ /g' identifiers_column.txt > identifiers_space.txt
   cp identifiers_space.txt our_first_shell_script.sh   
9. for i in "list of accessions.."
	do
	curl "http:.." copied and pasted
	done
	\n #newline
11. chmod u+x our_first_shell.script.sh
12. ./our_first_shell_script.sh
14. cat AB*.fa >>candida_dataset.fasta
15. muscle -in candida_dataset.fasta -out candida_dataset_aligned.fasta 
18. sed 's/.1.1 /g' candida_dataset_aligned.fasta | sed 's/Candida /Candida /g' > candida_dataset_aligned_names.fasta
19. Programs/Fasta2phylip.pl candida_dataset_aligned_names.fasta candida_dataset_aligned_names.phy #in reality it only works on ...names.fasta and adds .phy so that file name
20. Comparing fasta and phylip formats, the format for the fasta file is bunched together in sections with alot of newlines whereas the phylips format is in a continuous format.
21. raxmlPHC -p 12345 -s candida_dataset_aligned_names.fasta.phy -m GTRCAT -o AB040656.1_Malassezia -n candida 
26. The genus Candida is the most commonly occuring fungal infection worldwide, narrowing down to Candida dublinensis through various online resources  wikipedia and national institute of health) its apparent this species can produce germ tubes and chlamydospores and is opportunistic. Particularly in HIV patients. 
cite: Sullivan D, Coleman D. Candida dubliniensis: characteristics and identification. J Clin Microbiol. 1998 Feb;36(2):329-34. doi: 10.1128/JCM.36.2.329-334.1998. PMID: 9466736; PMCID: PMC104537.
cite: wikipedia https://en.wikipedia.org/wiki/Candida_(fungus)