# Construction of Semantic Topological Map for Domestic Environment
---
#### Abstract:
We propose a new method for constructing semantic topological maps. The semantic topological map is represented by a directed graph. The nodes of the graph indicate the type of objects, and the edge between the two nodes shows their relative relations. We performed instance segmentation with the Mask-RCNN network, used a mapping algorithm to estimate the relative positions, and update the map through each observation in a probabilistic model. We tested our method in an indoor environment. The results showed that our map could effectively reflect the relative positions of various objects in the domain.

#### Environment configuration:
- Anaconda3

- python3.6 / 3.7

- pycharm (IDE)

- pytorch 1.6 (pip package)

- torchvision 0.7.0 (pip package)

- tensorflow 2.4 (pip package)

  

#### Object Localization Algorithm:
1. Establishing the Subject:
   1. Iterate through [class_ids] to detect objects such as tables, chairs, etc.
   2. If a table is detected, set it as the subject, and so on.
      1. If there are multiple tables, select the one with the largest [roi] as the subject.
2. Iterate through [rois] and compare them with the subject's [roi]:
   1. If there is no overlap between [rois] and the subject's [roi]:
      1. Determine the relative position (left/right) of the object based on [rois].
   2. If there is an overlap between [rois] and the subject's [roi]:
      1. Complete overlap, meaning [rois] is inside the table's [roi]: Front/above.
      2. Partial overlap, Determine the occlusion relationship using [mask] and [rois]: Objects that are occluded are behind/below.
3. Save the relationships as an .svg file.
4. Generate a topology map.
   
Note: The occlusion relationship is determined by comparing the difference in the edge pixels between the bounding box and the mask. If the difference exceeds a certain threshold, it indicates that the object is occluded.
