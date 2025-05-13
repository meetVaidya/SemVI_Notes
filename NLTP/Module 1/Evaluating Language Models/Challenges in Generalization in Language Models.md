N-gram language models learn probabilities of word sequences directly from the training corpus. This leads to a couple of significant challenges when the model encounters new, unseen data.

#### 1. Dependency on Training Corpus & The Need for Generalization 

- **The Problem:** N-gram models are fundamentally "data-driven." The probabilities they learn (e.g., the probability of "York" following "New") are based only on how many times that sequence appeared in the specific text they were trained on. This means the model encodes facts and patterns specific to that training corpus.
    
- **The Challenge:** Real-world language is vast and diverse. A test set (or any new text the model encounters) will likely contain word sequences or even individual words that weren't in the training data. If the test corpus is very different from the training corpus, the model's performance will suffer because its learned "facts" might not apply.
    
- **The Goal: Generalization:** We need our models to be **robust**. This means they should be able to make reasonable predictions even for sequences they haven't seen before. They need to generalize from the patterns learned in the training data to new, unseen data.
    

#### 2. The "Zeros Problem": Unseen N-grams 

This is a direct consequence of the dependency on the training corpus.

- **What are "Zeros"?** These are n-grams (e.g., a bigram like "students opened" or a trigram like "students opened their") that were **never observed** in the training corpus.
    
- **Why is this a Problem?**
    
    1. **Underestimation of Probability:** If an n-gram never occurred, its raw count is 0. This means its probability, calculated as Count(n-gram) / Count(prefix), will be 0. This isn't quite right; just because we haven't seen it doesn't mean it's impossible. It might just be rare.
        
    2. **Zero Probability for Entire Sentences:** Language models calculate the probability of a sentence by multiplying the probabilities of its constituent n-grams (e.g., P(S) = P(w1|<s>) * P(w2|w1) * ... * P(</s>|wn) for a bigram model). If any single n-gram in that sentence has a probability of 0, the entire sentence's probability becomes 0.
        
        - **Impact on Perplexity:** Perplexity is calculated as P(TestSet)^(-1/N). If P(TestSet) is 0, perplexity becomes infinite, making it impossible to compare models or assess performance meaningfully.
            

#### 3. "Unknown Words" (Out-Of-Vocabulary - OOV) 

This is a specific type of "zero" problem, but at the individual word level rather than the n-gram sequence level.

- **The Issue:** What happens if a word appears in our test set that was never in our training vocabulary? For example, if our training data was all about finance, and our test sentence contains the word "photosynthesis."
    
- **The Solution: The <UNK> Token:**
    
    - We introduce a special pseudo-word, often called <UNK> (for "unknown"), into our vocabulary.
        
    - **Handling <UNK> during Training Data Preparation:**
        
        1. **Frequency-based Replacement:**
            
            - Option A: Choose a threshold n (e.g., n=1 or n=2). Any word in the training data that appears fewer than n times is replaced by the <UNK> token. This helps because very rare words are hard to model well anyway.
                
            - Option B: Define a fixed vocabulary size V (e.g., 50,000 most frequent words). All words in the training data that are not among these top V words are replaced by <UNK>.
                
        2. **Training the Model:** After this replacement, the language model is trained as usual. The <UNK> token is treated just like any other word. The model will learn probabilities like P(<UNK> | "the") or P("cat" | <UNK>).
            
    - **Handling <UNK> during Testing:** If a word encountered in the test set is not in the model's (now fixed) vocabulary, it is replaced by <UNK>, and the model uses its learned probabilities for <UNK>.
        

This <UNK> strategy helps manage OOV words, but it doesn't solve the problem of unseen sequences of known words (the n-gram "zeros problem"). For that, we need [[Smoothing Techniques|smoothing]]