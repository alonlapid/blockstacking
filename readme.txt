A program in Python that solves the Block stacking problem. 

Files: 
blocks.py the Python code for the Block stacking problem.
readme.txt - this documentation file 

To run  the program  execute from a command line:  python block.py  <infile.txt> <outfile.txt>

Algorithm: The main idea is that a block can be placed on top of another block only if the base area of the upper block is strictly smaller than the base area of the lower block. This means that the block with the largest base area has to be on the bottom if it is part of the optimal solution. 

Assume the blocks 1 2 … i are sorted in decreasing order of their base area. We define Si as the optimal solution to the problem where block i is at the top of the stack (which means that blocks with smaller base area are not part of the solution). The Si+1 solution is  constructed by placing  the  i+1  block on top of  one the previous solutions  S1 ... Si ,or having a stack containing only the Si block, whatever option gives the maximum height. Recall that the Si+1 block cannot be inserted in the middle of the previous solutions because its base is smaller then the bases of all previous blocks. The solution to the original problem is the solution Si that has the maximum height where  1 >= i  <= n. 

The program first reads the input file and generates the full list of blocks after creating 3 different blocks from each block type corresponding to the significant possible rotations (Boxes list in the code). Next the program sorts the list of blocks in decreasing order of their base area and begins constructing the array with solutions Si described above for 1 <= i <= n.  It starts from i=1 which is the base case and computes S1 which is a stack containing only the first block (with the largest base area). For i=2 it considers if the second block should be placed on top of S1 or be in its own stack. For S3 it considers if the third block should have its own stack or be placed on top S1 or S2. The process continues until i = the number of blocks and then the stack with the maximum height is chosen as the solution to the problem. For each solution Si the program captures the solution's height and the link to the stack that block i is placed on top of. This is done using 2 different arrays called optHeight and stacking.

Runtime – The runtime cost is Θ(n^2) as for each solution Si  1 <= i <= n  we have to evaluate i-1 options each with constant cost. The linear time of finding the best stack has no impact on the asymptotic runtime.

Design consideration – At the beginning, I wanted  to follow the patterns of the ski rental problem or the change problem but the recursive pattern was not as simple. The next step could not be constructed just by looking a single step back. Then I figured out that if I sort the blocks by their base area I could construct the solution for the next step by looking at ALL previous solutions. This has a runtime cost of  Θ(n^2)  with Θ(n) storage cost which I believe is good enough. 

I tested the program against simple test cases I could verify manually – for example 
3
1 2 3
4 5 6 
7 8 9

Gave 
The tallest tower has 6 blocks and a height of 30

6
8 9 7
7 8 9
5 6 4
4 5 6
2 3 1
1 2 3
