<h1 align="center">MRI Hippocampus Segmentation</h1>

The hippocampus is part of the limbic system, and plays important roles in the consolidation of information from short-term memory to long-term memory, and in spatial memory that enables navigation. In Alzheimer's disease (and other forms of dementia), the hippocampus is one of the first regions of the brain to suffer damage.
This project aims to develop a deep learning model for segmenting the hippocampus in MRI images of patients with Alzheimer's disease. For this purpose, a U-Net backboned by EfficientNet B0 is trained on the [MRI Hippocampus Segmentation](https://www.kaggle.com/datasets/sabermalek/mrihs) dataset from Kaggle.

## Dataset
As mentioned, the [MRI Hippocampus Segmentation](https://www.kaggle.com/datasets/sabermalek/mrihs) dataset is utilized in this project. This dataset contains MRI segmentation of the hippocampus and consists of two parts: one comprising MR images of 100 individuals, used as the training dataset, and another containing images of 35 individuals, used as the test data. All images are gathered from patients suffering from Alzheimer's disease.

Also, there are a total of 150 slices per individual, from which only the non-empty masks (masks containing at least one pixel with a value other than that of the background) were chosen for further processing.

## Model Architecture
The model utilizes the [Segmentation Models PyTorch](https://github.com/qubvel-org/segmentation_models.pytorch) library, which provides a variety of pre-trained architectures for semantic segmentation tasks. In this project, EfficientNet B0 is specifically employed within a U-Net architecure due to its balance between performance and computational efficiency. 

## Model Training
20% of the training data is randomly selected as the validation dataset, resulting in 2375, 594, and 1055 samples for the training, validation, and test datasets, respectively.

To enhance the model's performance and generalizability, various data augmentation techniques such as a random horizontal flip, scaling (padding and cropping), and rotation (up to 5 degrees) are applied to the training data.

Moreover, a combination of Dice Loss and Binary Cross-Entropy Loss is used to train the model to address class imbalance while maintaining consistent gradient updates.

## Performance Metrics
The model's performance is evaluated using Dice coefficient across different datasets:
  * Dice Score on Training Dataset: **0.8973**
  * Dice Score on Validation Dataset: **0.8904**
  * Dice Score on Test Dataset: **0.8390**

An example of an MRI image from the test dataset, its corresponding mask (hippocampus area), and the predicted mask can be seen below:
<p align="center">
  <img src="https://github.com/NegarMov/MRI-Hippocampus-Segmentation/blob/main/sample_prediction.JPG" alt="Sample Prediction" width="600"/>
</p>
