## Lesk’s Algorithm
Lesk (1986) introduced an overlap‐based method using dictionary glosses.

1. **Sense Gloss Extraction**  
   - For each candidate sense \(s\) of the target word, collect its gloss words from an MRD (e.g., WordNet).  
2. **Context Window Extraction**  
   - Collect surrounding words in a fixed‐size window around the target occurrence.  
3. **Overlap Scoring**  
   - Compute the number of shared words between the gloss bag and the context bag.  
4. **Sense Selection**  
   - Choose the sense whose gloss has the highest overlap with the context. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  

### Example
> Sentence: “The bank raised its interest rates.”  
> - Gloss(*bank*₁ “financial institution”): {“financial”, “institution”, “funds”,…}  
> - Gloss(*bank*₂ “river edge”): {“land”, “along”, “river”,…}  
> - Context bag: {“raised”, “interest”, “rates”}  
> - Overlap: 1 with *bank*₁ (interest), 0 with *bank*₂ → selects financial sense. :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  

---

## Enhanced Gloss Methods
- **Extended Lesk:** Include glosses of related senses (hypernyms, hyponyms) to enrich overlap set.  
- **Contextual Gloss Expansion:** Augment gloss with example sentences and usage notes.  

---

## Thesaurus‐Based (Walker’s) Algorithm
Walker et al. (1997) leverage thesaurus categories for disambiguation.

1. **Map Gloss Words to Thesaurus Categories**  
   - Use Roget’s or another thesaurus to associate each gloss word with one or more categories.  
2. **Map Context Words to Categories**  
   - Similarly map each context word.  
3. **Category Overlap Scoring**  
   - Count matching categories between gloss and context maps.  
4. **Sense Selection**  
   - Choose the sense with maximum category overlap. :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}  

---

## Resources: MRDs and WordNet
- **Machine‐Readable Dictionaries (MRDs):**  
  - Provide glosses, example usages, sometimes semantic relations.  
  - Coverage varies; often lacks modern or domain‐specific terms.  
- **WordNet:**  
  - Organized into **synsets**: sets of synonyms sharing a single sense.  
  - Encodes multiple semantic relations: hypernymy, hyponymy, meronymy, antonymy.  
  - APIs available for programmatic access. :contentReference[oaicite:6]{index=6}:contentReference[oaicite:7]{index=7}  

---

*Image context:*  
- Diagram showing gloss overlap: context words “dog,” “bark,” “tree” overlapping with glosses of *bark*₁ (sound) vs. *bark*₂ (tree covering).  
