# Jaws Dataset Segmentation

This project is about applying image segmentation on dicom images for Jaws dataset. Those dicom images consist of a coordinate system of three planes. The three planes' types are as in the following:
1. axial plane: by placing your point of view above the patient and looking down to take the patient image
2. coronal plane: by placing your point of view either in the eyes (anterior) or in the back of a patient (posterior).
3. sagittal plane: by placing your point of view from the side (either right or left) of the patient.
Each plane type dataset consists of 3 classes (background, upper and lower jaw). As a result, when we use all the planes to train one model the number of classes = 7, and when training the model with a specific plane type the number of classes = 3.

In this project I build two segmentation models, the models are the implementation of the UNET model:
1. one is applying on the entire dataset for the three planes (axial, coronal and sagittal) together.
2. the second one you can specify which plane dataset you want to segment (axial, or coronal or sagittal)
In both cases the data is divided into:
1. Training ==> The training is splitted into (90% train and 10% validation)
2. Testing
The data is passed to the model in the form of patches of size = 16. And I didn't apply any image augmentation. 

## Project's components:
The project consists of 6 notebooks:
1. dataset: Has the methods required for downloading, preparing, reading and plot samples of the data.
2. explore_dataset: By running this notebook you can read, print pixel values, see histogram and see actual samples of all planes' types of the dataset. This notebook imports a dataset notebook as it uses its functions to explore the data.
3. model: Has the unet model class and functions. It is used to create instances of the model.
4. utils: It contains all the helper functions which will be used to load and save the data. Also plot the used metrics (loss, accuracy and IoU) for visualizing the model performance.
5. train_all_planes: Create a model. Apply training, validation and testing methods for the model with the entire 3 planes' dataloaders. To successfully run the model you need to combine all the 3 planes' datasets together, which is done through untils notebook.
6. train_one_plane: Create a model. Apply training, validation and testing methods for the model with a specific plane type dataloaders. To successfully run the model you need to write which plane type (axial, or coronal or sagittal) you want to learn the model on. Here, we learn a model on axial data.
- model_all_data_10: it is a saved model, which is trained on the entire 3 planes training data for 10 epochs.
- model_axial_data_10: it is a saved model, which is trained on only axial's training data for 10 epochs.
- predicted_masks folder: contains all predicted masks from model one (trained on3 planes together).
- true_masks folder: contains all ground truth masks from the entire 3 planes' testing data.
- predicted_masks_axial folder: contains all predicted masks from model two (trained on only axial raining data).
- true_masks_axial folder: contains all ground truth masks from axial3 plane's testing data.
### Comparing between predicted and true masks, you will find that the models results have avery small loss which means a good models' performance

## Metric used:
For measure the models performance I used the following metrics
1. Loss
2. Accuracy
3. IoU
when running the "train_all_planes and train_one_plane" notebooks you will see their values and see graphs to visualize the metric.

## Used tools:
- Python, pytorch
- Google Drive
- GPU of google colab and kaggle.
- CPU of my pc using jupyter.
### You can run the code on any of them, but it will take too much time to train models on CPU. you just need to adjust data path.
