(base) ntorres1@teachingserver:/media/Scratch8TB/CLG2023/ntorres1/Blasr_Blast$ cat README.txt 
1. mkdir Blasr_Blast
2. cd /media/Scratch8TB/CLG2023/ntorres1/DeNovoAssembly/K35
   cp k35run.scafSeq.fasta /media/Scratch8TB/CLG2023/ntorres1/Blasr_Blast
3. cd /media/Scratch8TB/CLG2023/Course_files 
   cp unknown.fasta  /media/Scratch8TB/CLG2023/ntorres1/Blasr_Blast
4. 
6. blasr --header unknown.fasta k35.run.scafSeq.fasta > blasr_output.txt
7. copy and paste into excel "Data -> Text to Columns"; Copy, select 2 rows in excel and select "Data-> Text to Columns", select space delimited and space. 
9. The unknown sequence fell squarely within out known (reference) genome. 

Blast: 
1. makeblastdb -in k35run.scafSeq.fasta -dbtype nucl
3. blastn -query unknown.fasta -db k35run.scafSeq.fasta -outfmt 6 -num_alignments 100 -out blast_output.txt 
4.	1) qseqid: query or source (gene) sequence ID						
	2) sseqid: subject or target (reference genome) sequence ID					
	3) pident: Percentage of identical positions 
	4) length: alignment length (sequence overlap)						
	5) mismatch: number of mismatches 
	6) gapopen: number of gap openings 
	7) qstart: start of alignment in query						
	8) qend: end of alignment in query						
	9) sstart: start of alignment in subject
	10) send: end of alignment in subject 
	11) evalue: expect value
	12) bitscore: bit score

 Some of the differences between Blasr and Blast, number of columns. Blasr has 13 whereas Blast as 12. 
 Other differences include the score vs. bitscore, those figures  are opposite. Other differences include the order of the reads. Blasr seems easier than Blast to read and understand. 