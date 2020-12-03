# ECG_AD(Anomaly Detection on ECGs)

Train an autoencoder to detect anomaly.

# Overview

ECG_AD use the autoencoder(AE) to detect anomaly. 

With this data:

*By reducing the reconstruction error , it can improve the performance of the model.

*illustrate the concept of anomaly detection that can be applied to larger datasets with no labels available(for example, if you have thousands of normal data points and only a small number of abnormal data points).

# Requiremnts

## Environment

Currently, requires following packages
- Python 3.5+
- TensorFlow 1.2+
- Pandas 1.0+
- Numpy 1.0+
- Scikit-learn 0.22+
- Keras 2.0+

## Datasets

The dataset is ECG5000.This data set contains 5000 ECGs, each with 140 data points. Use a data sample that already has specific labels (0 means abnormal, 1 means normal, and there are only two labels of 0 and 1)

You can find the dataset [(Here)](http://www.timeseriesclassification.com/description.php?Dataset=ECG5000) .

*This data has 500 training samples, 4,500 test samples, 140 long, and the number of classes is 5. The last column is the label.

*Description: The original dataset for "ECG5000" is a 20-hour long ECG downloaded from Physionet. The name is BIDMC Congestive Heart Failure Database(chfdb) and it is record "chf07". It was originally published in "Goldberger AL, Amaral LAN, Glass L, Hausdorff JM, Ivanov PCh, Mark RG, Mietus JE, Moody GB, Peng C-K, Stanley HE. PhysioBank, PhysioToolkit, and PhysioNet: Components of a New Research Resource for Complex Physiologic Signals. Circulation 101(23)". The data was pre-processed in two steps: (1) extract each heartbeat, (2) make each heartbeat equal length using interpolation. This dataset was originally used in paper "A general framework for never-ending learning from time series streams", DAMI 29(6). After that, 5,000 heartbeats were randomly selected. The patient has severe congestive heart failure and the class values were obtained by automated annotation.

*Best Algorithm: COTE

*Best Accuracy: 94.6%

*Second Link: [(Here)](http://dl.acm.org/citation.cfm?id=2833467) 

<p align="center">
    <a href="http://www.timeseriesclassification.com/images/datasets" target="_blank"> <img src="http://www.timeseriesclassification.com/images/datasets/ECG5000.png"
 width="600" height="400" border="10" /></a>
</p>

*Data displays:

<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/dataset.png?raw=true">

# Which type of the task is it? 

Since this is a labeled data set, it can be regarded as a supervised learning problem. 

# Build the model
<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/model.png?raw=true">

# Training and Testing
Firstly , you should normalize the data via the linear method. The training data's labels r all  1 instead of 0.

* A Normal ECG figure:
<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/A%20normal%20ECG.png?raw=true">

* AN Anomalous ECG figure:
<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/An%20anomalous%20ECG.png?raw=true">


* Becuase the autoencoder only uses normal ECG data for training, but uses all test sets for evaluation.
<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/training_only_train%20set.png?raw=true">

* Training error and Validation error
<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/train_validation.png?raw=true">

* If the reconstruction error is greater than one standard deviation of the normal training example, you will quickly classify the ECG as abnormal. First, let us draw a normal
ECG from the training set, and perform reconstruction after encoding and decoding with an autoencoder, as well as reconstruction errors.

<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/reconstruction%20error.png?raw=true">

<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/anomalous%20reconstruction%20error.png?raw=true">

* Train Loss and Test Loss
<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/Train%20Loss.png?raw=true">

<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/Test%20Loss.png?raw=true">

# Evaluation
  When detecting the reconstruction error of abnormal samples in the test set, the reconstruction error of most samples will be much larger than the threshold.By changing the threshold, the accuracy and recall rate of the classifier can be adjusted.
  
* The result:
<img src="https://github.com/kanesp/ECG_AD/blob/main/data/pic/evaluation.png?raw=true"> 

The main code is from [(Here)](https://www.kaggle.com/mineshjethva/ecg-anomaly-detection) . 
I have corrected some errors,collected the datasets, interpreted the code in Chinese.
