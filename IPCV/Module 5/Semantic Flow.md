## 1. Semantic Flow: Big-Picture Consistency

**Definition:**  
Semantic flow tracks _meaningful_ entities (objects, body parts, etc.) across images or frames, preserving their identity even under changes in pose, illumination, or appearance.

### 1.1 In NLP

- **Role:** Keeps a conversation coherent by carrying forward context and intent from one sentence to the next.
    
- **Example:** Recognizing that “it” in sentence two still refers to “the car” mentioned in sentence one.
    

### 1.2 In Computer Vision

- **Role:** Matches and follows semantically rich features—like a hand, face, or car—across two images or video frames.
    
- **Example:** Aligning the cat’s ears, face, and paws between a “sitting” shot and a “jumping” shot, even though its shape and orientation change.
    

---

## 2. Optical Flow: Pixel-Level Motion

**Definition:**  
Optical flow computes how _individual pixels_ move between two consecutive images, yielding a vector field of per-pixel velocities.

- **What it tells you:** Direction & speed for each pixel.
    
- **When it shines:** Small, continuous motions (e.g., background panning, smooth object motion).
    
- **Example:** Mapping how leg-pixels shift forward as a person takes a step.
    

---

## 3. Side-by-Side Comparison

|Aspect|Optical Flow|Semantic Flow|
|---|---|---|
|**Level of focus**|Low-level (pixels)|High-level (objects, body parts)|
|**Robust to appearance**|No — only works for small, consistent moves|Yes — works across pose/lighting changes|
|**Primary output**|Motion vectors for every pixel|Matched semantic regions across frames|
|**Ideal use cases**|Fine-grained motion estimation|Object tracking, action/body analysis|

---

## 4. How Semantic Flow Actually Works

1. **Feature Extraction**
    
    - A deep model (e.g. ResNet, MoveNet, OpenPose) processes each image and learns to detect abstract patterns (edges, textures → “this looks like a hand”).
        
2. **Building Feature Maps**
    
    - Each image is converted into a grid of _feature vectors_.
        
    - Every grid cell encodes high-level concepts (e.g., hand, face, motion hint), not raw RGB.
        
3. **Comparing Feature Vectors**
    
    - For each candidate region in Image A, compute similarity with regions in Image B.
        
    - **Cosine similarity** (focus on direction of vectors) or **Euclidean distance** (magnitude + direction) gauge how “alike” two patches are in meaning.
        
4. **Alignment & Tracking**
    
    - High-similarity pairs get linked: the model “knows” this patch in Frame 1 and that patch in Frame 2 are the same object.
        
    - Output: a mapping that shows—despite movement or deformation—the same semantic part is tracked.
        

---

## 5. Choosing Your Similarity Metric

- **Cosine Similarity**
    
    - Best when _direction_ (feature pattern) matters most and scale (vector length) is irrelevant.
        
- **Euclidean Distance**
    
    - Use when both _direction_ and _magnitude_ (strength of activation) carry meaning.
        

---

## 6. Typical Applications

- **Object Tracking:** Continuously follow a vehicle, animal, or person across frames.
    
- **Body Movement Analysis:** Map joints over time to analyze gait, sports motion, or gesture.
    

---

## 7. Concrete Example: Tracking a Hand

1. **Input:** Two photos of someone moving their hand.
    
2. **Features:** A model outputs feature maps where one cell “lights up” for the hand region in each frame.
    
3. **Similarity:** The hand-patch vectors have cosine similarity ≈ 0.98, so they’re matched.
    
4. **Result:** Even though the hand changed pose, semantic flow aligns “Hand_A” in Frame 1 with “Hand_B” in Frame 2.


## 8. How a Deep Network Extracts High-Level Features
- Layer 1: Detects edges (like boundaries between objects)
- Layer 2: Combines edges to detect shapes (like circles, curves or rectangles).
- Layer 3: Detects specific objects or body parts (e.g. an eye, nose or hand)
- Layer 4: Recognizes the relationship between parts (e.g. "this is a person with a raised hand")

At the higher layers, the network recognizes semantic meaning - it understand what the image or part of the image represents.