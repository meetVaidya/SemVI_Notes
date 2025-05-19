## Graph Construction for WSD
Graph‑based methods model senses and their relations as a graph \(G = (V, E)\):

- **Vertices (\(V\))**: Candidate sense nodes for all ambiguous words in the input.  
- **Edges (\(E\))**: Semantic relations between senses, such as:  
  - Synonymy  
  - Hypernymy/Hyponymy  
  - Meronymy  
  - Gloss overlap connections  
- **Edge weights** can reflect relation strength (e.g., frequency of co‑occurrence in gloss overlaps).

*(Image context: A small graph with nodes for *drink*₁, *drink*₂, *milk*₁, *milk*₂ connected by relation edges.)*

---

## Random Walk & PageRank for Sense Scoring
Random walk algorithms identify the most “central” sense node in the graph:

1. **Initialization**  
   - Assign uniform initial probability \(p_0(v) = 1/|V|\) to each node \(v\).  
2. **Transition Matrix**  
   - Derive from edge weights, normalized so each row sums to 1.  
3. **Power Iteration**  
   - Repeatedly multiply the probability vector by the transition matrix until convergence:  
     \[
       p_{t+1} = \alpha \,T^\top p_t + (1 - \alpha)\,p_0
     \]  
   - \(\alpha\) is the damping factor (often 0.85).  
4. **Sense Selection**  
   - For each ambiguous target word, select the sense whose node has the highest steady‑state probability \(p_\infty(v)\). :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  

---

## Benefits & Limitations
| Aspect                   | Advantages                                                  | Limitations                                           |
|--------------------------|-------------------------------------------------------------|-------------------------------------------------------|
| **Global context**       | Considers all sense relations jointly                       | Graph can be large; computation can be expensive      |
| **Unsupervised**         | No annotated corpora required                               | Quality dependent on resource coverage & relation accuracy |
| **Flexibility**          | Incorporates diverse relation types (lexical, gloss, syntactic) | Requires carefully tuned edge weights and damping factor |

---

## Practical Considerations
- **Graph pruning**: Remove low‑weight edges to reduce noise.  
- **Edge weighting**: Experiment with relation‑specific weights (e.g., gloss overlap vs. WordNet hierarchy).  
- **Computational efficiency**: Use sparse matrix representations and efficient solvers for PageRank.  
