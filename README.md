## RoadMap

1. I firstly implement the code in python, however, the random generator of `random` or `numpy` does not behave coincidentally with the counter part of g++.
c.f., https://stackoverflow.com/questions/57154268/different-pseudo-random-numbers-between-c-and-python-implementations.
2. Then I turn to use the hybrid `c` and `python` (public_key_generator(deprecated).py), It's fairly slow as well.
3. At last, I implement the code in `c`. 

## Features
1. I tune the code carefully for generating the same result as `profanity` does, such there are lots of test code in the source file.
2. Hardcode, such that you should modify the arguments in the source file.
3. The **base** private key and the public key are ordered as <public, private>, and the iterator and the public key are ordered as <private, public>,
such that the `PublicKey = k*G = (BasePrivateKey + Iterator)*G` can work smoothly, in the meantime, the iterator is sorted by `leveldb` as the strategy of the iterator generation of `profanity`.

## Misc
1. 500Gb storage is required to build the database.
2. Theoretically, 8Gb memory is needed to perform the search task, however, at least 64Gb memory is required in practice. 

## HowTo
For a clean ubuntu box, you should:
1. apt-get update
2. sudo apt-get install libleveldb-dev
3. sudo apt-get install libssl-dev

The iterator generator takes ~48 hours to generate 100 round <private, public> key pairs (100 * 0x400000) with 2 threads, and the database takes ~40 Gb.
The base generator takes ~48 hours to generate 0x100000000 <private, public> key pairs with 16 threads, and the database takes ~400 Gb.

## An example
