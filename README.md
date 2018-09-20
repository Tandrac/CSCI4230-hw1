Tommy Olney
9/19/18
Cryptography and Network Security 1
CSCI 4230
Homework 1 writeup

	I wrote this program using Python 3.5, with Spyder. The code for my project can be be broken into four major sections.
	
	
	The first major section is the main encrypt/ decrypt functions. They handle the initial permutation of the text, where the initial eight bits of text are scrambled into the  two, six, three, one, four, eight, five, seven permutation. From there, the eight bit permutation is split into two four-bit lists.
	
  
	Next, we generate the values for K1 and K2. I did this by inventing a ten digit initial key (one, one, zero, zero, one, zero, one, one, one, zero in my case), and then mostly just followed the diagrams provided, as I permuted the ten digit key as instructed, then split it into the left five bits and the right five bits. I then left shifted them once, by dropping the leading binary digit, and them appending a zero to the back of the list. Then, I combined the left shifted right and left digits to get K1, permuting (and dropping the first and second digits) as instructed. I then left shifted the right and left bits again, then recombined in the same way that K1 was made to get K2.
	
  
	Using the newly make keys, I use my Ffunct (F function) method to generate the next part of the encryption. My Ffucnt works by taking in a four-bit binary list, expands it to an eight bit list through the specified permutations, then xor it with the previously generated K1. After the xor, the newly made list is then split into two parts, the left four bits and the right four bits. Then, both lists are put in their respective substitution matrices. I put the left bits in the function called lSub, and the right bits in the function called rSub. These functions work by generating the respective matrices for their side, then by using the second and third, and first and four bits to find the indices for the column and row. The value found in the matrix is then converted to binary, and returned back. The lSub and the rSub are probably some of the more hacky sections of my code, as they work almost identically, other than the initiated values of the matrix being different. On top of that, the way I converted the integers to binary was pretty bad, as I generated the four binary representation of the possible numbers (zero to three), then used a couple if statements to determine which pre generated binary list would be returned. After the substitutions, the two two-bit lists are combined, then permutated as specified, then the final list is returned. 
  
  
	Finally, after another xor and F function, the list is once again permuted, and the final encrypted list is created. After that list is created, it is then run through my decrpyto function to decrypt it. Decrpyto is almost identical to the main crypro function, except it has the positions of K1 and K2 reversed so that the program can decrypt the files back to their original state.
