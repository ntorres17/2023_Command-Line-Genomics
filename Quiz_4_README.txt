(base) ntorres1@teachingserver:/media/Scratch8TB/CLG2023/ntorres1/Quiz_4$ cat README.txt 
1. mkdir Quiz_4
2. touch README.txt 
3. cp Quiz4_Blast_output.out /media/Scratch8TB/CLG2023/ntorres1/Quiz_4
4+ 5. awk '$3 >=75' Quiz4_Blast_output.out && awk '$4>750' Quiz4_Blast_output.out > Quiz4_Blast_output_75ID_750bp.out

Part II: 
1. touch my_for_loop.sh
2. nano my_for_loop.sh 
3.# for i in "I love quizzes in command line genomics" 
  #      do echo $i 
#done 
4. chmod u+x my_for_loop.sh 
5. ./my_for_loop.sh