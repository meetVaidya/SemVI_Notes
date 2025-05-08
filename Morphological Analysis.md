#### Definition
- studies the structure of words or formation of words.
- understand how are words **built from smaller pieces**.

#### It comprises of:
- **identification**
- **analysis of root words**
- **affixes (suffixes and prefixes)**
- Example: 
	- `washing -> wash + ing`
	- `browser -> browse + er`
	- `incomplete -> in + complete`

#### Techniques for pre-processing
1. **Tokenization**
	- Eg: John ate the pizza !
		- `John`, `ate`, `the`, `pizza`, `!`
2. **Stop Word Removal**
	- removal of words that occur commonly across the documents and do not provide much meaning to the text.
3. **[[Stemming and Lemmatization|Stemming & Lemmatization]]**
	- **Stemming**: a simpler approach that involves removing prefixes and suffixes to obtain the stem. However, stemming can result in incorrect or nonsensical stems.
		- `running` -> `run`
		- `happiness` -> `happi`
	- **Lemmatization**: a more advanced approach that uses a dictionary or vocabulary to map words to their base or root form (the lemma).
		- `running` -> `run`
		- `happiness` -> `happy`
4. **[[N-Gram Language Model]]**
	- Continuous sequence of N-terms from a given sample text
	- ![[Pasted image 20250508163819.png]]
