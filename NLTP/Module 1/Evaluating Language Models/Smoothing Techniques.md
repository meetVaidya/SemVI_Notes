Smoothing techniques are designed to solve the "zeros problem" for n-grams by ensuring that no n-gram ever gets a strictly zero probability.

### 1. Introduction to Smoothing

- **Purpose:** To prevent the language model from assigning a zero probability to n-grams that were simply not seen in the limited training data.
    
- **Mechanism (The Core Idea):**
    
    - "Shave off" a small amount of probability mass from the n-grams that were seen (the frequent ones).
        
    - Re-distribute this "shaved off" probability mass to the n-grams that were never seen (the zero-count events).
        
- **Alternative Term:** This process is also called **discounting**, because we are discounting the counts/probabilities of observed events to save some probability for unobserved ones.
    

### 2. Laplace Smoothing (Add-1 Smoothing)

This is the simplest smoothing technique.

- **The Basic Idea:** Before calculating probabilities, **add one to the count of every possible n-gram**.
    
- **Effect on Counts:**
    
    - N-grams that had a count of 0 will now have a count of 1.
        
    - N-grams that had a count of 1 will now have a count of 2, and so on.
        
- **Intuition:** It's like pretending we saw every conceivable n-gram at least one extra time than we actually did.
    
#### Laplace Smoothing for Unigrams:
    
- **Unsmoothed Maximum Likelihood Estimate (MLE):**
    $$ P(w_i) = \frac{c_i}{N} $$
    where:
    
    - $c_i$: count of word $w_i$
    - $N$: total number of word tokens in the training data
    
- **Laplace Smoothed Probability:**
    $$ P_{\text{Laplace}}(w_i) = \frac{c_i + 1}{N + V} $$
    where:
    
    - $V$: vocabulary size (the number of unique word types).
            
    - **Why $(N + V)$ in the denominator?** We added 1 to the count of each of the $V$ unique words in our vocabulary. So, the total count of all words effectively increases by $V$. To ensure probabilities still sum to 1, the denominator must reflect this increase.
            
#### Laplace Smoothing for Bigrams:

- **Unsmoothed MLE:**
    $$ P(w_n | w_{n-1}) = \frac{C(w_{n-1}w_n)}{C(w_{n-1})} $$
    where:
    
    - $C(w_{n-1}w_n)$: count of the bigram (sequence) $w_{n-1}w_n$
    - $C(w_{n-1})$: count of the unigram prefix $w_{n-1}$ (how many times $w_{n-1}$ appeared)
            
- **Add-one Smoothed Bigram Probability:**
    $$ P_{\text{Laplace}}(w_n | w_{n-1}) = \frac{C(w_{n-1}w_n) + 1}{C(w_{n-1}) + V} $$
    where:
    
    - $V$: vocabulary size.
            
    - **Why $(C(w_{n-1}) + V)$ in the denominator?** For a given preceding word $w_{n-1}$, there are $V$ possible words that could follow it (one for each word in the vocabulary). By adding 1 to the count of each of these $V$ possible bigrams starting with $w_{n-1}$, the total count of bigrams starting with $w_{n-1}$ effectively increases by $V$.
            

### 3. Add-k Smoothing

Laplace (Add-1) smoothing is simple, but it often overestimates the probability of unseen n-grams and significantly reduces the probability of seen n-grams.

- **Critique of Add-1 Smoothing:**
    
    - It can cause very large changes to the original counts and probabilities. For example, if $C(\text{want to})$ was 608, Add-1 smoothing might effectively reduce its influence significantly (as seen by the adjusted count of 238 on slide 20).
        
    - It often moves too much probability mass from frequent events to all the zero-count events. In a large vocabulary, there are many, many more unseen n-grams than seen ones.
        
    - The probability $P(\text{to} | \text{want})$ decreasing from 0.66 to 0.26 (slide 21) shows how much it can alter probabilities of frequent, reliable n-grams.
        
- **Alternative: Add-k Smoothing:**
    
    - Instead of adding a full count of 1, we add a smaller, fractional count $k$.
        
    - $k$ is a positive value, typically $0 < k < 1$ (e.g., $k = 0.5, k = 0.1, k = 0.01$).
        
- **Formula for Add-k Smoothed Bigram Probability:**
    $$ P_{\text{Add-k}}(w_n | w_{n-1}) = \frac{C(w_{n-1}w_n) + k}{C(w_{n-1}) + kV} $$

    - Notice the denominator: we add $k$ to the numerator (for the specific bigram) and $k \times V$ to the denominator (because we've added $k$ to each of the $V$ possible bigrams that could follow $w_{n-1}$).
        
- **$k$ as a Hyperparameter:** The value of $k$ is not fixed. It's a hyperparameter that usually needs to be **tuned** by trying different values and seeing which one performs best on a separate dataset called a **development set** (or validation set).
    
- **Goal:** To be less aggressive than Add-1 smoothing. It still gives some probability mass to unseen events but tries to preserve more of the original distribution of seen events.
    