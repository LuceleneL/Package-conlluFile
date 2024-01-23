# Package conlluFile
This repository has a Python 3 package to handle a CoNNL-U file (`.conllu`) in a data structure (base).

# Contents
The files in this repository are:
- `README.md` - this read explanatory file;
- `conlluFile.py` - the Python 3 package;

# The Data Structure
This package has a class `conlluFile` that is constructed reading a `.conllu` file and creating a list of sentences (instance variable `base`), header lines of the input file (instance variable `header`), total number of sentences (instance variable  `s`), total number of tokens (instance variable `t`).

## Sentence structure
Each sentence `b` (an element of `base`) is composed by 6 pieces of information:
- `b[0]` SID - sentence ID
- `b[1]` TEXT - text of the sentence
- `b[2]` number of tokens (not including the contracted word lines)
- `b[3]` lines of the header (including, but not limited to, the '# sent_id =' and '# text' lines)
- `b[4]` token lines (including contracted word lines)
   - each token line has 10 elements of the CoNLL-U format, plus one place holder for information
- `b[5]` status of change (a place holder for information)

# The Constructor
- `__init__(self, name="", skipAg=False)`
   - The input parameter `name` is the path and file name of the `.conllu` file to be read (if absent, an empty structure is created);
   - The input parameter `skipAG` (by default False) makes the data creation to ignore CoNLL-U lines describing contracted words (e.g. `na` as the contraction of `em`+`a`).

# The Acessors Methods
- `getBase(self)`              - returns the whole base;
- `getHeader(self)`            - returns in a single string the initial lines of the `.conllu`;
- `getS(self)`                 - returns the number of sentences;
- `getT(self)`                 - returns the number of tokens (ignoring contracted words);
- `getSandT(self)`             - returns the number of sentences and tokens;
- `getSentByID(self, SID)`     - returns a sentence by its SID (string) - return `None` if absent;
- `getSentByIndex(self, ind)`  - returns a sentence by its index (int) - return `None` if absent;
- `getSentInd(self, SID)`      - returns the index (int) of the sentence with SID (string) - return -1 if absent;
- `getSentID(self, ind)`       - returns the SID (string) for the sentence indexed by ind - return -1 if absent
- `isSIDin(self, SID)`         - returns True if the SID is in the base;
- `isINDin(self, ind)`         - returns True if the index (int) is in the base;
- `isSentTagged(self, ind)`    - returns True if the sentence indexed by ind (int) has a non empty tag (`b[5]`);
- `numberSentSize(self, size)` - returns how many sentences in the base have this size;
- `sentSizeRange(self)`        - returns the smallest and largest sentence size within the base;
- `getAllSIDs(self)`           - returns the list with all sentence IDs.

# The Mutator Methods
- `addToBase(self, name)`          - adds a `.conllu` file (name) to the base considering contracted word or not (`skipAg`);
- `removeSentInd(self, s)`         - removes the sentence with id `s` from base;
- `removeSentSID(self, s)`         - removes the sentence with SID `s` (string) from base;
- `tagTokenAtSID(self,s,t,tag)`    - sets `tag` (string) for `s` is the SID (string), `t` is the token `id` (string);
- `tagTokenAtSent(self,s,t,tag)`   - sets `tag` (string) for `s` is the sentence index (int), `t` is the token `id` (string);
- `tagSent(self,s,tag)`            - sets `tag` (string) for `s` is the sentence index (int);
- `setSentTags(self)`              - sets the sentence tags (additional info) based on the tokens tags (additional info);
- `sortBase(self)`                 - sorts the base according to SID.

# The Printing Methods
- `printSent(self, ind, outfile, nodeprel=False)` - prints out a sentence by its index (int) in a outfile with all 10 fields;
- `printHeaderToo(self, outfile, nodeprel=False)` - prints out the whole base in an outfile;
- `printNoHeader(self, outfile, nodeprel=False)`  - prints out the whole base in an outfile.

# Acknowledgments
This work was carried out at the Center for Artificial Intelligence of the University of São Paulo (C4AI - [http://c4ai.inova.usp.br/](http://c4ai.inova.usp.br/)), with support by the São Paulo Research Foundation (FAPESP grant #2019/07665-4) and by the IBM Corporation. The project was also supported by the Ministry of Science, Technology and Innovation, with resources of Law N. 8.248, of October 23, 1991, within the scope of PPI-SOFTEX, coordinated by Softex and published as Residence in TIC 13, DOU 01245.010222/2022-44.
