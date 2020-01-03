# Code-breaking

Youâ€™ve intercepted a secret message that is encrypted using both of two techniques. In Replacement, each letter of the alphabet is replaced with another letter of the alphabet. (For example, all aâ€™s may have been replaced with fâ€™s, bâ€™s with zâ€™s, etc.) Unfortunately, we donâ€™t know the mapping that was used. In Rearrangement, the order of the characters is scrambled. For each consecutive sequence of n characters, the characters are reordered according to a function that maps character indices to character indices. For example, if n = 4 and the mapping function is f(0) = 2,f(1) = 0,f(2) = 1,f(3) = 3, then the string test would be rearranged to be estt (because the character at index 0 was moved to index 2, index 1 was moved to index 0, etc). We donâ€™t know the mapping function that the encoder used, but we do know that n = 4.
## Algorithm Used

```
Initial Probabilities :  Created a table representing probability of each letter occuring first using the given corpus.
Transition Probabilities : Created a table representing all the transitions a combination of letters can take by joining the given corpus.

Both the probabilities were computed by taking the log form

1. Start with a guess about the encryption tables. Call the guess T

2. Modify T to produce a new guess, Tâ€². This modification was done using a uniform distribution value, if the value from the distribution is greater than 0.5, then switch 2 numbers in rearrangement table else switch 2 letters in replace table

3. Decrypt the encoded document using T to produce document D, and decrypt the document using Tâ€²
to produce Dâ€²

4. If P(Dâ€²) > P(D), then replace T with Tâ€². Otherwise, with probability P(Dâ€²)-P(D), replace T with Tâ€². Computed the probability using uniform distribution with np.exp(P(D') - P(D)) 

5. Go to step 2.

After various runs, we concluded that the algorithm fairly converges in 20,000 iterations

```

## Sample Outputs

```
./break_code.py encrypted-text-1.txt corpus.txt output-encrypted-text-1.txt

hen in the ourse of human events it becomes necessary for one people to dissolve the political bands which have connected them with another and to assume among the powers of the earth the separate and equal station to which the aws....

```

```
./break_code.py encrypted-text-2.txt corpus.txt output-encrypted-text-2.txt

onures as the term is used by aviculturists include only the genera ratings and yrrhura as well as several single species genera and one double species genus these other genera are listed below....

```

```
./break_code.py encrypted-text-3.txt corpus.txt output-encrypted-text-3.txt

o  union is more profound than marriage for it embodies the highest ideals of love fidelity devotion sacrifice and family n forming a marital union two people become something greater than once they were s some of the petitioners in.....

```

```
./break_code.py encrypted-text-4.txt corpus.txt output-encrypted-text-4.txt

he illy ibrary located on the campus of ndiana niversity in loomington ndiana is an important rare book and manuscript library in the nited tates t its dedication on ctober   the library contained a collection of  books  manuscripts more than fifty oil paintings and  prints urrently the illy ibrary has.....

```
The entire output is uploaded in  with its respective names. The algorithm gives the right output 6 out of 10 times we run.
