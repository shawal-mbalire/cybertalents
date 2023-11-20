# Hide Data

Category: Cryptography
Level: easy
Points: 50

## Description

I used to hide my data with a classic cypher, can you get the flag hidden inside? gur synt vf 2w68lsudym Vg vf cerggl rnfl gb frr gur synt ohg pna lbh frr vg v gbbx arneyl 1 zvahgr gb rapbqr guvf jvgu EBG13 tbbq yhpx va fbyivat gung

It looks as if the letters were shifted to create an encrypted file thus we try shift cipher algorithms like rot13

```echo "gur synt vf 2w68lsudym Vg vf cerggl rnfl gb frr gur synt ohg pna lbh frr vg v gbbx arneyl 1 zvahgr gb rapbqr guvf jvgu EBG13 tbbq yhpx va fbyivat gung" | tr '[A-Za-z]' '[N-ZA-Mn-za-m]' ```
we swap the alphabet A to Z with N to Z A to M, essentially shifting letters by 13.
we get 

```the flag is 2j68yfhqlz It is pretty easy to see the flag but can you see it i took nearly 1 minute to encode this with ROT13 good luck in solving that```