**What is Optical flow?**
- Optical flow tracks how pixels move between two consecutive images or video frames.
- It tells us the direction and speed of movement for each pixel.
- **Example**: Imagine recording a person walking. Optical flow maps how each pixel on their body shift from frame 1 to frame 2 - for instance, tracking how the pixels of a leg move forward.


| Optical Flow                                                | Semantic Flow                                                                                          |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| Tracks pixel-level movement                                 | Tracks **high level content** (like objects or body parts)                                             |
| Works best with small movements between consecutive frames. | Works even if objects change pose, shape or lighting                                                   |
| Focuses on **low-level motion**                             | Focuses on **what the object or part means**                                                           |
| Example: Tracking how pixels shift when a person runs.      | Example: Recognizing that the hand in two images belongs to the same person, even if posed differently |
