> [!NOTE] Definition
> ""Perplexity measures the confidence model has in its (next word) predictions. The concept of perplexity measures how confused the model is in predicting the next word in a sequence. Lower perplexity indicates that the model is more certain about its predictions.""

- Perplexity is a key metric used to evaluate the performance of language models. 
- It quantifies how well a model predicts a sequence of words or tokens, essentially measuring the model's uncertainty or "confusion" when generating or interpreting language


- **Lower perplexity** means the model is more confident and accurate in its predictions.
    
- **Higher perplexity** means the model is less certain, considering many possible next words or tokens

![[Pasted image 20250513181840.png]]

#### **Why Use Perplexity?**

- It provides a single, interpretable number to summarize model performance: lower is better.
    
- It is widely used for comparing language models on the same dataset.
    
- It is directly related to information theory concepts like entropy and cross-entropy, offering a bridge between probability and practical model evaluation

---
### Perplexity as a Branching Factor

- **Perplexity** in language modeling can be intuitively understood as the _weighted average branching factor_ of a language model
- This interpretation connects the mathematical definition of perplexity to a concrete idea: how many plausible next words the model considers at each prediction step.

#### **What Is Branching Factor?**
- The **branching factor** of a language is the number of possible next words that can follow any given word
- In a simple, uniform model (e.g., predicting random digits 0–9), the branching factor is 10: every digit is equally likely, so at each step, there are 10 equally probable choices
#### **How Perplexity Relates to Branching Factor**
- **Perplexity** is the exponentiated average negative log-likelihood (or cross-entropy) of the predicted sequence
- It can be interpreted as the _effective number of choices_ the model is considering at each step-the "average number of equally likely next words" the model is uncertain between
- If a model's perplexity is 6, it means that, on average, the model is as uncertain as if it had to choose uniformly among 6 options for each word