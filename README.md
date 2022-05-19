# Tillage Classification

Author: Tommy Kimura

## Introduction

This is the Tillage Classification project that loads field images, classfies an image to one of the four classes – Grass, High Tillage, Low Tillage, and No Tillage, and then conduct analysis. This project belongs to National Center for Supercomputing Application, as a part of Dr.Kaiyu’s study. 

Some directories and files are too big in size to be uploaded to GitHub, therefore, I am storing them in using [Box](https://uofi.box.com/s/wnqj881dcv2jgqko0sjnw80ke98jrhxl). This contains `StreetviewImages`, `StreetviewBoundaries`, and some previous models. 

### Directory

```
tillage_classificaion
├── StreetviewImages
	├── ...
├── StreetviewBoundaries
	├── ...
├── README.md
├── analysis.ipynb
├── confidence_data.pickle
├── corn_model.ipynb
├── load.ipynb
├── process.ipynb
└── soybean_model.ipynb
```

## Preprocessing

We need to preprocess the images into train, validation, and test datasets. If we want to apply Geotagging mask to each image, this is also where we compute the masked images. Everything is done mainly in `process.ipynb`, and it requires the directories `StreetviewImages` and the pickle file `confidence_data.pickle` that has information for each data. If Geotagging is desired, we also need the `StreetviewBoundaries` directory.

### Preprocessing directory

```
tillage_classificaion
├── StreetviewImages
	├── ...
├── StreetviewBoundaries
	├── ...
├── confidence_data.pickle
├── process.ipynb
```

This part should create the new directory with the name specified by the user and contains train, validation, and test directories for each type of the crop. 

```
tillage_classificaion
├── USER_SPECIFIED_image
	├── corn_dataset
		├── train
			├── ...
		├── val
			├── ...
		└──  test
			├── ...
	└── soybean_dataset
        ├── train
			├── ...
		├── val
			├── ...
		└──  test
			├── ...
```

## Resent Models

### General Model Information

For this project, we are mainly applying transfer learning, and uses a pretrained Resnet18 model for classification. Compared to the previus intern’s result, we have achieved 70%+ accuracy, and even higher for certain setting. 

### General Pipeline

For this project, we have the general pipeline as below. Example files (`soybean_model.ipynb` and `corn_model.ipynb`) for each crop type in the repository follows this pipeline. 

1. Initialize **Data Transformation** for a given directory
2. Initialize **Resnet18 Model** and tune the model for our classification purpose
3. Train with 50 epochs 
   1. Generate accuracy and loss curves
4. **Confusion Matrices** evaluation
5. **Save** models to specified path

There is also a `load.ipynb` file that loads the model from the saved path, and conduct step 4. 

### Improvements

- For now, the model architecture has been set, and it is mainly the Image transformation that we have been conducting experiements on for better performance. 
- We could also have class weights for each class to rule out the imbalanced dataset issue. 
- Data augmentation could also improve model accuracy. 
- More accurate labeling

## Analysis

We have also conducted experiments to discard images with confidence below a certain threshold. This is in the file `analysis.ipynb` where we have discarded images with confidence below thresholds from 0.5 to 0.9. 

### Metrics

- F1 Macro scores
- Recall
- Supports
