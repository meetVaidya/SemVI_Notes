## 1. What Is a Context-Free Grammar?  
- A CFG is a **formal system** for modeling constituent (phrase) structure in natural (and programming) languages .  
- Also known as a **Phrase-Structure Grammar**, a CFG underlies many NLP tasks—parsing, grammar checking, machine translation, etc.—because it balances expressivity with efficient parsing algorithms .

---

## 2. Formal Definition  
A CFG **G** is a 4-tuple  
```
G = (N, Σ, R, S)
```  
where:  
- **N** is the set of **non-terminal** symbols (abstract categories like NP, VP, S)  
- **Σ** is the set of **terminal** symbols (actual words, e.g. “the”, “flight”)  
- **R** is the set of **production rules**  
- **S** ∈ N is the **start symbol**, typically interpreted as the sentence node .

---

## 3. Terminals vs. Non-terminals  
- **Terminals** (Σ) correspond to the words of the language.  
- **Non-terminals** (N) express abstractions over terminals (e.g., NP for noun phrase) .

---

## 4. Production Rules  
- Each rule in **R** has the form  
  ```
  A → α
  ```  
  where **A** ∈ N and **α** is a sequence of terminals and/or non-terminals.  
- Rules can be **hierarchically embedded**, allowing rich recursive structures .

### **Example Rules**  
- **Sentence** → Noun Phrase + Verb Phrase  
  ```
  S → NP VP
  ```  
- **Verb Phrase** → Verb + Noun Phrase  
  ```
  VP → Verb NP
  ```  
- **Verb Phrase** → Verb + Noun Phrase + Prepositional Phrase  
  ```
  VP → Verb NP PP
  ```  
- **Prepositional Phrase** → Preposition + Noun Phrase  
  ```
  PP → Preposition NP
  ```  


---

## 5. Two Perspectives on CFGs  
1. **Generator:** Starting from **S**, repeatedly rewrite non-terminals using rules until only terminals remain—this produces valid sentences.  
2. **Recognizer (Parser):** Given a sentence, assign it a structure (a **parse tree**) showing how rules combine to yield the sentence.  
   - A **derivation** is the specific sequence of rule-applications.  
   - A **parse tree** graphically represents that derivation, with the root at **S** and leaves as the terminals .

---

## 6. Start Symbol & Language  
- **Start symbol** **S** designates where generation/parsing begins.  
- The **language** of **G** is the set of all strings of terminals derivable from **S** .

---

## 7. Why “Context-Free”?  
- A rule’s left side is always a **single non-terminal** (i.e., its application doesn’t depend on surrounding context).  
- Enables efficient parsing algorithms (e.g., CYK) because each rewrite step is locally governed by one non-terminal .

