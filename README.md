# Lab-5-MLPR


AIM:

The aim of this project was to detect faces in an image of the plaksha faculty and compare the face features of Shashi tharoor with the faulty's by extracting color based features (Hue and Saturation), clustering the detected faces using K-Means, and classifying Shashis Sirs face based on the learned clusters.


This is the original Photo oF the Plaksha Faculty:

![Plaksha_Faculty](https://github.com/user-attachments/assets/be4b6887-aee1-435d-aef8-aac29e7b8d59)


This is the template image of Sir Shashi Tharoor:

![Dr_Shashi_Tharoor](https://github.com/user-attachments/assets/27f0802b-ff77-4fa1-8691-2f00b00f74d6)


<br><br><br><br>




METHODOLOGY:

1. Face Detection
I started by converting image to grayscale for less computational power. I used Haar Cascade (haarcascade_frontalface_default.xml) which is a cascade of filters and classifiers that detects faces using things like edge detection and pixel intensities. This data is then compared with a threshold to classify if the region is a face or not. I then proceeded to detect face bounding boxes using detectMultiScale().


2. Feature Extraction
For Feature extraction, i first converted the colour space from BGR to HSV as we wanted to work with hue, saturation and value (intensity of colour) to make better features than intensity values of Blue, Green, Red. 
I then proceeded to extract: Mean Hue, Mean Saturation;
Which created a 2D feature vector: (Hue, Saturation).


3. Clustering
For clustering I applied K-Means clustering (k=2) and used Euclidean distance (default in K-Means) to computed centroids for both clusters by initializing K centroids and then assigning each face to the nearest centroid (using Euclidean distance). The code then updates centroids as the mean of assigned points and repeats until the clusters stabilize.


4. Template Classification
First, I loaded a template image of Sir Shashi Tharoor, I extracted Hue and Saturation features for the same and predicted where his data will place with respec to the set clusters using kmeans.predict(). I then visualised the template placement in the made feature space as seen below:

<img width="2020" height="1096" alt="image" src="https://github.com/user-attachments/assets/52ffed62-7fd6-44d6-a95d-42ae99473bbf" />

<br><br><br><br>

Here is a clearer intuitive plot:

<img width="2016" height="1096" alt="image" src="https://github.com/user-attachments/assets/90dc697d-89a7-43da-aaf0-3a8176eb99c7" />

<br><br><br><br>

KEY FINDINGS: 

* Grayscale images work well while using Haar cascade as it works on contrast (intensity differences).
* Hue and Saturation can serve as simple but effective features for basic clustering. 
* K-Means successfully separated faces into different groups based on color features using repeated centroid updates till a threshold was reached.
* The Template classification works by assigning the template to the nearest cluster centroid using kmeans.predict.
* The feature scaling and distance metric choice directly impacts the clustering quality.



LIMITATIONS:

* Haar Cascade may fail for tilted or poorly lit faces (I might do image segmentation and processing like using imbinarize (adaptive) etcetra to refine the image to counter that).
* Using only Hue and Saturation ignores texture and structural facial features.
* K-Means assumes spherical clusters and equal variance which in real world applications like this one, is very rare to have while using color spaces. If clusters are irregular, overlapping, or unevenly spread, centroid based classification may lead to incorrect assignments leading to lower accuracy of results.
* Euclidean distance may not perform well in higher dimensions if we choose to convert to other colour spaces and use more features.
* As the feature space is based on colour and not geometry of the faces, texture or such deeper features, the clusters reflect color similarity, not actual facial identity.
* The clustering also gets affected by characteristics like irregular illumination, shadows of the original image, hence the image processing needs to be taken care of before performing computer vision tasks for precise and accurate results.
  

CONCLUSION:

This project demonstrates a complete pipeline from basic image preprocessing to clustering and classification using distance based learning. It highlights the importance of choosing the right vector space, with efficient independent features, using distance metrics, and unsupervised learning in simple computer vision tasks. While this proved to be effective for this project, a more robust system would use deeper features and methodologies for improved accuracy which i will be doing as part of my future goals and learnings.
