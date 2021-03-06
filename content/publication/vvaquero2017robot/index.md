+++
title = "Low resolution lidar-based multi-object tracking for driving applications"
date = 2017-08-15T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Iván del Pino", "Victor Vaquero", "Beatrice Masini", "Joan Solà", "Francesc Moreno-Noguer", "Alberto Sanfeliu", "Juan Andrade-Cetto"]

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
publication = "*Robot 2017: Third Iberian Robotics Conference, Vol 694 of Advances in Intelligent Systems and Computing*"
publication_short = "In *ROBOT*"

# Abstract and optional shortened version.
abstract="Vehicle detection and tracking in real scenarios is a key component to develop assisted and autonomous driving systems. Lidar sensors are specially suitable for this task, as they bring robustness to harsh weather conditions while providing accurate spatial information. However, the resolution provided by point cloud data is very scarce in comparison to camera images. In this work we explore the possibilities of Deep Learning (DL) methodologies applied to low resolution 3D lidar sensors such as the Velodyne VLP-16 (PUCK), in the context of vehicle detection and tracking. For this purpose we developed a lidar-based system that uses a Convolutional Neural Network (CNN), to perform point-wise vehicle detection using PUCK data, and Multi-Hypothesis Extended Kalman Filters (MH-EKF), to estimate the actual position and velocities of the detected vehicles. Comparative studies between the proposed lower resolution (VLP-16) tracking system and a high-end system, using Velodyne HDL-64, were carried out on the Kitti Tracking Benchmark dataset. Moreover, to analyze the influence of the CNN-based vehicle detection approach, comparisons were also performed with respect to the geometric-only detector. The results demonstrate that the proposed low resolution Deep Learning architecture is able to successfully accomplish the vehicle detection task, outperforming the geometric baseline approach. Moreover, it has been observed that our system achieves a similar tracking performance to the high-end HDL-64 sensor at close range. On the other hand, at long range, detection is limited to half the distance of the higher-end sensor."
abstract_short = "We explore the possibilities of Deep Learning (DL) methodologies applied to low resolution 3D lidar sensors such as the Velodyne VLP-16 (PUCK), in the context of vehicle detection and tracking. For this purpose we developed a lidar-based system that perform point-wise vehicle detection using a Convolutional Neural Network (CNN) feeded by PUCK data only, and estimate the actual position and velocities of the detected vehicles by means of a Multi-Hypothesis Extended Kalman Filters (MH-EKF). Comparative studies between the proposed lower resolution (VLP-16) tracking system and a high-end system, using Velodyne HDL-64, were carried out on the Kitti Tracking Benchmark dataset. The results demonstrate that the proposed low resolution Deep Learning architecture is able to successfully accomplish the vehicle detection task. Moreover, it has been observed that our system achieves a similar tracking performance to the high-end HDL-64 sensor at close range."

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
url_pdf = "http://www.iri.upc.edu/files/scidoc/1924-Low-resolution-lidar-based-multi-object-tracking-for-driving-applications.pdf"
url_preprint = ""
url_code = ""
url_dataset = ""
url_project = "/publication/vvaquero2017robot/"
url_slides = ""
url_video = ""
url_poster = ""
url_source = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
url_custom = [{name = "SPRINGER", url = "https://link.springer.com/chapter/10.1007/978-3-319-70833-1_24"},
              {name = "IRI", url = "http://www.iri.upc.edu/publications/show/1924"}]

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





![robot17_thumbnail](/publication/vvaquero2017robot/ROBOT_17_DeepLidarPuck.jpg "ROBOT_17_thumbnail")




## **Paper Summary**

In this paper we expand the possibilities of the [Deep Lidar](../ecmr_17_deeplidar) segmentation approach, applying it to lower resolution lidar data, such as the provided by
the Velodyne VLP-16 (PUCK). We use the Kitti Tracking Benchmark dataset, decimating the Velodyne HDL-64 point clouds to match the PUCK sensor
descriptions. The resulting low resolution information is used to train a new convolutional architecture for detecting vehicles which outputs 
are feed into a multi-hypothesis tracker module. The tracking results are finally evaluated using the Kitti evaluation server. 
We study how the sensor resolution affects the overall system performance by performing a comparative study using both mentioned sensors.


### **Sensor and Lidar Data Representation**


{{< figure src="/publication/vvaquero2017robot/robot_17_sensor_comp.png" 
title="HDL-64 and VLP-16 specifications and its Kitti dataset effective FOV " >}}


![robot17_fig2](/publication/vvaquero2017robot/robot_17_fig2.png "ROBOT_17_fig2")

Left: Comparison between total Ground-Truth (GT) objects and True Positives 
(TP) obtained with both systems using the whole training set filtered at different
maximum distances. Right: Kitty training samples exemplifying the scarcity of data of
lidar-based methods when compared to image ones. From top to bottom, RGB Camera
image, HDL-64 and simulated VLP-16 range images.


### **Results**

## Qualitative results. 
![robot17_results](/publication/vvaquero2017robot/robot_17_results.jpg "ROBOT_17_results")

In columns, images show the raw input, the Deep detector
output with vehicle points in red, the final tracked vehicles and the RGB projected
bounding boxes submitted for evaluation. The first three rows illustrate different PUCK
results, while the fourth and fifth are a comparison between the simulated VLP-16 and
the HDL-64 resolution systems. As can be seen, the performance is similar in the near
field but the detection distance is shorter in the first case.


## Quantitative results. 

{{< figure src="/publication/vvaquero2017robot/robot_17_results_table1.png" 
caption="Point-wise vehicle classification modules evaluation over the Kitti tracking dataset. We compare the final tracker performance with both sensors, the HDL-64 and VPL-16. " >}}



We performed different experiments to gain an insight into the maximum detection distance that our low resolution system can manage.
Attending to the results, two distance performance metrics have been defined. On one hand, the effective detection distance, 
which we defined as the maximum distance at which the system recall $(TP /  (TP + FN ))$ remains over a $90\%$. 
On the other hand, the maximum detection distance, a less restrictive measure to obtain the distance at which at least
a third of the new vehicles are correctly tracked. To calculate it, we set an incremental 
recall metric $(\Delta TP / (\Delta TP + \Delta FN))$ that computes the recall with the
$TP$ and $FN$ increments produced due to an increase of the distance threshold.


{{< figure src="/publication/vvaquero2017robot/robot_17_results_table2.png" 
title="Point-wise vehicle classification modules evaluation" >}}

It can be appreciated that systems based on both high-end and low resolution
lidar sensors have similar performances in near field. We can also observe that
the HDL-64 version achieves a maximum detection distance (incremental recall $>\ 33.3\%$)
 of 60 meters and an effective detection distance (recall $>\ 90\%$) of 40
meters, whereas the simulated VPL-16 low resolution version scores a half in the
two metrics, 30 meters of maximum and 20 meters of effective detection distance.




