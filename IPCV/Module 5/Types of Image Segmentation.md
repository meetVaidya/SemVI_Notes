Image Segmentation
1. Instance Segmentation
	 - each new object is labelled as a different instance, even within the same category.
	 - ![[Pasted image 20250430160557.png]]
2. Semantic Segmentation
	- all pixels with the same category are represented as a single segment
	- ![[Pasted image 20250430160638.png]]
3. Panoptic Segmentation
	- combines semantic and instance segmentation

![[Pasted image 20250430160754.png]]

## Things and Stuff Classification in Panoptic Segmentation
- **Things**: Things in a panoptic image segmentation technique <u>refer to countable and distinct object instances within an image, such as cars, people, animals, furniture, etc.</u> Each object and instance in a scene has **well-defined boundaries** and is identified and separated as individual instances.
- Stuff: Stuff in panoptic image segmentation refers to uncountable regions in an image, such as sky, road, grass, walls, etc. These regions do not have well-defined boundaries

## Object Localization and Detection
- With **image/object localization**, we are able to identify the location of the main subject of an image.
- **Object Detection** - the objects within an image or a video are detected, marked with a bounding box, and then labelled.

## FAQs
Q. Difference between semantic segmentation and object detection ?
Semantic segmentation focuses on identifying and classifying every
pixel in an image, while object detection focuses on identifying specific
objects and their locations.
Q. When should I choose segmentation over object detection?
Segmentation is ideal for tasks that require fine-grained information
about object boundaries and regions.
applications such as medical image analysis, manufacturing defect
detection, and robotics object localization.
Object detection is suitable for identifying specific objects and their
locations.
applications in tasks like video surveillance, agriculture for crop
monitoring, and retail analytics.