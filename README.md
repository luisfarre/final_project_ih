# final_project_ih_jun_2020

## Deep learning

### Open Image - Object Detection

https://storage.googleapis.com/openimages/web/download.html

Te idea of the project is to train a neuronal network capable of detecting classes of objects.
As working with images need high computational resourses the project is developed in google cloud, using a Tesla K80 GPU.

#### Creating the Dataset (notebook 0)

The real dataset has around 9 million images, and 6k classes. In order to make this project doable we decided to do the hole process just for one class. In that case boats images.

Data used:

- classes: class_descriptions_boxable.csv - https://storage.googleapis.com/openimages/v5/class-descriptions-boxable.csv
- boxes: oidv6-train-annotations-bbox.csv - https://storage.googleapis.com/openimages/v6/oidv6-train-annotations-bbox.csv
- images: train-images-boxable-with-rotation.csv - https://storage.googleapis.com/openimages/2018_04/train/train-images-boxable-with-rotation.csv
- 10 open-images-dataset-train_n.tsv files with all images urls. - https://storage.googleapis.com/openimages/v6/oidv6-train-annotations-bbox.csv

With all those datasets we managed to create a .tsv file with all images urls containing boats, around 26k 
We also created a .csv file with all the data of those images and boxes around 79k boxes for those 26k images.

Once we had the .tsv file we uploaded it to google cloud storage bucket and made it public in order to be able to download all images from their urls through a google cloud url transfer data and store them in the bucket.

images_data_boat_project.tsv file https://storage.googleapis.com/data_images_ih/tsv_files/images_data_boat_project_file.tsv

google cloud storage bucket - https://console.cloud.google.com/storage/browser/data_images_ih 

### Create google cloud bucket

- Upload .tsv file


#### Image preprocessing, creating X_data and y_data (notebook 1)


- Access the bucket
- Clone darknet and create gpu version.
- Create specific folders and paths.
- Get all labels and masks needed and upload them to the labels folder.
- Access all images, resize them and add them to the images folder.
- Check example to make sure images are the right size and lebels match expectations.

### Train, validation, test split (notebook 2)
Once you have decided how many images you want to use it's time to split those images into three diferent sets. 
- Training set: 80% of the images, the network will use those images to train.
- Validation set: 10% of the images, will be used while training to check how well is doing and then update weights and iterate again.
- Test set: 10% of the images, once the model is trained we need to test the accuracy to make sure it's not overfitted and is accurate both with classes and masks.

### Network configuration and train (notebook 3)

To be able to train the model we need to set up the configuration. That means specify the model where the data is.
- Train
- Validation
- classes names
- buckap (where to save weights after x iterations)

Having this set up, we are ready to start training. To help the model train we use pre trained darknet53.conv.74 weights.

### Loss, IOU and Test (notebook 4)
In order to visualize how well the training is going we create two charts using train_log.txt data.
- Loss: we want it to be as close as possible to 0.
- IOU: we want it to be as close as possible to 1.

Now is time to use the model with data never seen before and check how well predicts. For that we use test set.


#### Doubts

