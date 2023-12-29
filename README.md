# Deep learning methods using imagery from a smartphone for recognizing sorghum panicles and counting grains at an on-farm scale


## Summary
1. [Objective](#objective)
2. [Libraries used](#libraries-used)
3. [Detecting and segmenting](#detecting-and-segmenting)
4. [Counting](#counting)
5. [Data availability](#data-availability)
6. [Acknowledgments](#acknowledgments)

---

## Objective

This study had the main objective to fill the research gap of using imagery obtained from smartphones to detect and segment sorghum panicles and also count the number of grains.It employed convolutional neural networks (CNNs)for effectively removing background under field conditions and counting sorghum grains. Therefore, the specific objectives included i) detect and segment sorghum panicles at field scale using imagery from a smartphone camera, ii) utilize segmented imagery to count the number of grains within manually segmented panicles, and iii) employ a linear model to estimate the total number of grains within a panicle based on the previous counting. Through this innovative approach, we aimed to provide the basis for the development of a mobile app to transfer this knowledge to the farm-level

----

## Libraries used 

The main libraries and frameworks used in this study includes:

* TensorFlow;
* Detectron2;
* Yolov8;
* OpenCV;
* imgaug;
* Scipy;
* Scikit-learn;
* Pandas;
* Matplotlib;
* Roboflow;
* Labelme;
* numpy;

----

## Detecting and segmenting

The first step is the detection and segmentation of sorghum panicles from smartphone imagery. The images were collected in a sorghum field at Wamego, Kansas-US during the 2022 season using an ordinary smartphone, perpendicularly to the panicles and set on automatic capture mode, against the sunlight.

The images were annotated and augmented using Roboflow software.

To perform this task, two frameworks were tested: Detectron2 and Yolov8, with Yolov8 presenting the best performance in both detection and segmentation tasks.

On the folder [DetectionPanicles]("./DetectionPanicles") is the complete algorithm were the two frameworks were trained, tested and visually validated.

---

## Counting

To count, 40 images were randomly selected from the original dataset to detect and segment. The main panicle was manually segmented and the background was extracted. The images were then cropped in 3 equal-height patches: the top, the middle, and the bottom of the panicle. Point labels were manually placed in each visible grain using labelme software. The points and the images were then augmented using imgaug library. The augmented label points dataset were converted to density maps using gaussian filter function from scipy library.

Three different architecture models were evaluated in estimating density maps step: MCNN, TCNN-Seed and Sorghum-Net (developed in this study). The models architecture were developed using TensorFlow library and can be seen in this [file]("./Counting/counting_via_AI.ipynb").

To evaluate the models' perfomance, were used the metrics: Mean Absolute Error (MAE), Main Square Error, and Mean Absolute Percentage Error (MAPE), from the scipy library.

Lastly, to estimate the amount of grains from the whole panicle, a different dataset of 198 images of sorghum panicles were obtained during the same day and using the same configurations mentioned before.The panicles were also manually segmented, the background was removed, and the imagery was patched in three again. The images were input into Sorghum-Net model and the total number of grains was estimated as the sum of the three patches.

A polynomial linear regression model was fitted using the scikit-learn library. To quantify the accuracy of the model, the scikit-learn library was employed to calculate the following metrics: coefficient of determination (R2), MSE, RMSE, and mean absolute percentage error (MAPE).

----

## Data availability

The raw data, among the labels are available upon reasonable request to gsantiago@ksu.edu.

---

## Acknowledgments

The authors would like to thank Ciampitti Lab team, specifically to all the research scholars that helped with the data collection and labeling process: Milagros Cobal, Lucas Suguiura, Brian Michiels, Oscar Lanza, Luciano Fello, and Juan Ahunchain. Sorghum Checkoff and Corteva Agriscience for providing support for field trials, investigation, data collection, and labeling process of sorghum imagery. Contribution no. 24-XYZ-J from the Kansas Agricultural Experiment Station.