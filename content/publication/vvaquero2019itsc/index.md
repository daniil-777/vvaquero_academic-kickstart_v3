+++
title = "Improving Map Re-localization with Deep ‘Movable’ Objects Segmentation on 3D LiDAR Point Clouds"
date = 2019-10-10T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Victor Vaquero", "Kai Fischer", "Francesc Moreno-Noguer", "Alberto Sanfeliu", "Stefan Milz"]

# Publication type.
# Legend:
# 0 = Uncategorized
# 1 = Conference paper
# 2 = Journal article
# 3 = Manuscript
# 4 = Report
# 5 = Book
# 6 = Book section
publication_types = ["1"]

# Publication name and optional abbreviated version.
publication = "In *International Transportation Systems Conference (ITSC)*."
publication_short = "In *ITSC*"

# Abstract and optional shortened version.
abstract = "Localization and Mapping is an essential component to enable Autonomous Vehicles navigation, and requires an accuracy exceeding that of commercial GPS-based systems. Current odometry and mapping algorithms are able to provide this accurate information. However, the lack of robustness of these algorithms against dynamic obstacles and environmental changes, even for short time periods, forces the generation of new maps on every session without taking advantage of previously obtained ones. In this paper we propose the use of a deep learning architecture to segment movable objects from 3D LiDAR point clouds in order to obtain longer-lasting 3D maps. This will in turn allow for better, faster and more accurate re-localization and trajectory estimation on subsequent days. We show the effectiveness of our approach in a very dynamic and cluttered scenario, a supermarket parking lot. For that, we record several sequences on different days and compare localization errors with and without our movable objects segmentation method. Results show that we are able to accurately re-locate over a filtered map, consistently reducing trajectory errors between an average of 35.1% with respect to a non-filtered map version and of 47.9% with respect to a standalone map created on the current session."
abstract_short = "We propose the use of a deep learning architecture to segment movable objects from 3D LiDAR point clouds in order to obtain longer-lasting 3D maps. This allows for better, faster and more accurate re-localization and trajectory estimation on subsequent days."

# Is this a selected publication? (true/false)
selected = false

# Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects = []

# Tags (optional).
#   Set `tags = []` for no tags, or use the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []

# Links (optional).
#url_pdf = "http://www.iri.upc.edu/files/scidoc/2018-Deep-Lidar-CNN-to-Understand-the-Dynamics-of-Moving-Vehicles.pdf"
url_preprint = "https://arxiv.org/abs/1910.03336"
#url_code = ""
#url_dataset = ""
url_project = "/publication/vvaquero2018itsc/"
#   url_slides = "https://docs.google.com/presentation/d/1uRa97XRmTf57wvDiMR_cmLE4yKcFCh61CMz19X4Y260/present?usp=sharing"
#url_video = "https://youtu.be/9jn0A_AwX_I"
#url_poster = "https://drive.google.com/file/d/1DB8Q03xKdo7_XGZy4CMFIosp8WFmfyI5/view?usp=sharing"
#url_source = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
url_custom = [{name = "IRI", url = "http://www.iri.upc.edu/publications/show/2229"}]

# Digital Object Identifier (DOI)
doi = ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++




![itsc19_thumbnail](/publication/vvaquero2019itsc/ITSC_19_SLAM.jpg "ITSC_19_thumbnail")


<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe src="//www.youtube.com/embed/BJU3cRpkYcM" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border:0;" allowfullscreen title="YouTube Video"></iframe>
</div> 
   
   

## **Paper Summary**

In this paper we propose the creation
of longer lasting 3D LiDAR maps with state of the art
localization and mapping algorithms by eliminating from
the source the possible dynamic components of the scene.
For that, we take advantage of deep learning techniques
and introduce the use of two different convolutional neural
networks which, having respectively as input a front and a
bird’s eye view projections of the 3D LiDAR point cloud,
segment the movable objects from the scene. To demonstrate
our approach, we build 3D maps of a very dynamic environ-
ment such as a parking lot with and without our segmentation
applied and use it to assist for locating ourselves at different
times and days, showing a consistent reduction of the average
trajectory estimation error. Moreover, we show how our
approach can also be employed for building a full map of
an area covered in several days.



{{< figure src="/publication/vvaquero2019itsc/ITSC_1.png" 
title="We propose to segment movable objects from 3D LiDAR point clouds to build longer lasting maps that can assist on trajectory estimation for subsequent days. For that we employ two deep networks processing respectively a front and a bird’s eye view projection of the LiDAR input frames. By retaining mostly static elements on the scene, we are able to accurately estimate our position and trajectory on subsequent days by additionally re-localizing on the map. " >}}


## **Approach**

The main objective of this paper is to demonstrate how,
by pre-filtering possibly moving objects from the scene,
we are able to accurately locate during longer periods of
time in standard 3D maps such as the ones generated with
common SLAM or LiDAR odometry and mapping (LOAM)
algorithms. Our approach has two main modules, which are
detailed in this section: A) deep-learning based segmentation
of movable objects in 3D LiDAR point clouds; B) accurate
re-localization at different days over a map built from a
cluttered dynamic scenario using standard LeGO-LOAM
algorithm. This can also be employed to build a full map
over several days or in a multi agent way.


### Movable Objects Segmentation 


![itsc19_net](/publication/vvaquero2019itsc/ITSC_2.png "ITSC_19_net")

We model the moving objects segmentation task as a refined encoder-decoder architecture. As the inputs are quite big (500 × 600) we apply five
contractive and five expansive levels. To get richer features at each level, we insert customized fire modules that capture
local and context information from the previous feature maps. These modules first reduce the number of feature channels
and apply two parallel sets of convolutional filters on them to finally concatenate the results, obtaining local and context
aware features. Intermediate losses are computed in this network, merging predictions at different resolutions.


### Vehicle Localization

To locate inside an already built map our system uses
just Velodyne LIDAR data and, if available, information
from low-cost car GPS.
We first create a ground truth map at day zero against which we aim
to locate on the subsequent days. Then we detail our
localization approach, which consist on obtaining an coarse
initial guess followed by the final accurate localization (see paper).

{{< figure src="/publication/vvaquero2019itsc/ITSC_3.png" 
title="Comparison of the extracted features (blue) from the full point cloud and the one with removed movable objects respectively. By providing an unfiltered point cloud the feature extraction mechanism selects a vast amount of points from dynamic objects which can be compensated by applying our proposed movable object detection algorithm. " >}}



## **Experiments**

To show the effectiveness of the proposed approach, we
have recorded 7 different sequences of a cluttered and
dynamic urban environment, i.e. a supermarket parking lot,
on different days and at diverse hours. 
We show our re-localization capacities in this highly unsteady
scenario using as GT-Map a recording from a different day,
which would be useless if it were not for our approach, as it
will not last more than the session for which it was created.
In the paper we additionally show additional application of our approach
for building a map through different days, which can also
extrapolated to a multi-agent map building task.

{{< figure src="/publication/vvaquero2019itsc/ITSC_5.png" 
caption="Qualitative results comparing the performances of 'Reloc. Full' and 'Reloc. Filtered' on the Map Extension experiment. In red we display the estimated trajectories along the days and in blue the ground truth. For 'Reloc. Full' the resulting map shows blurry and doubled map contents caused by drift from the ground truth due to incorrect feature matching which are clearly compensated by our approach." >}}


### Results

{{< figure src="/publication/vvaquero2019itsc/ITSC_tab1.png" 
caption="Re-Localization results comparing LeGO-LOAM, Reloc. Full and Ours (Reloc. Filtered)." >}}











___
      

