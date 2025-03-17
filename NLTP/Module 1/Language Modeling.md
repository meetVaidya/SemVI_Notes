## Definition of Language Model
- Any model that computes probability of the sentences or probability of new words when probability of other words are given.

## N-gram model
- It says that instead of computing the probability of a word given its entire history, we can approximate the history by just the last few words.
- For Example, bigram
- The bigram model, for example, approximates the probability of a word given all the previous words P(wn|w1:n−1)
- by using only, the conditional probability of the preceding word P(wn|wn−1).


> [!NOTE] Bigram Model Note
> The assumption that the probability of a word depends only on the previous word is called a Markov assumption

![[Pasted image 20250311083131.png]]

![[Pasted image 20250311083216.png]]

