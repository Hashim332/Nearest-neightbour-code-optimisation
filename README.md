# Nearest-neightbour-code-optimisation
Task was to optimise inefficient code that was finding nearest neighbour of N particles in a periodic unit cube. 

A random number of N points were generated in a periodic unit cube (a constant seed state was used to replicate this 'random' cube)
The goal of the legacy code was to find the shortest displacement vector from one point to another, for every single point in this cube.
Only lines 18-67 were allowed to be edited.

LEGACY CODE:
The legacy file was looping through ranges of N (the number of points) to compare two random points and used multiple if statements to check and calculate the displacement vector bewteen these two points. 
The loop was run thrice for each dimension and then the displacement vectors magnitude was computed and stored in an N x N matrix (2D array).
Next, the code checked for the smallest displacement vector element in each row of the matrix. Each row comprised of all the displacement vectors for the number of points generated.
Once the smallest vector was found, its index was stored in another array and this was stored to a txt file. 

OPTIMISED CODE:
The goal for this optimisation was to use NumPy's vectorisation to remove inner loops as well as if statements to produce a more streamlined, readable and efficient code after understanding basic O notation for code efficiency.

The optimised code uses NumPy array broadcasting to allow the CPU to compute operations of entire arrays in parallel. Since positional data was stored in the position matrix defined at the start of the code, indexing allowed for the code to compute the smallest distance to the nearby point by comparing the straight line vector within the cube and the straight line vector of the point in an adjacent cube which is thought to be 'imaginary' (documents attached explain this concept in detail).
After finding the shortest displacement vector to the point, instead of calculating its square root within a loop, the size of the vector is directly proportional to its magnitude so it is stored. 
Due to the nature of the code, it will choose the same points and compare their displacement therefore this matrix of displacement is a symmetrical matrix with the comparision of the same point present in the diagonal (which produces a displacement of 0 since it is taking the displacement from it to itself). Since this cannot be avoided, all diagonal elements are set to be extremely large numbers, so that when the minimum is computed, the 0 element is ignored.
Next, the numpy.argmin() function returns the index of the smallest element of each row which is stored in an array and compared to the array generated by the legacy code. If the indices are the same, the optimised code is correct. If the match fails, there is a bug.

Nearest neighbour in periodic lattice in 2D which was used to model the 3D variation:
[Finding the nearest neighbour in 2D.pdf](https://github.com/Hashim332/Nearest-neightbour-code-optimisation/files/10013777/Finding.the.nearest.neighbour.in.2D.pdf) 
