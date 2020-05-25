# final_project_ih

## Deep learning

### Open Image - Object Detection

https://storage.googleapis.com/openimages/web/download.html

Te idea of the project is to train a neuronal network capable of detecting classes of objects.
As working with images need high computational resourses the project is developed in google cloud, using a Tesla K80 GPU.

#### Creating the Dataset

The real dataset has around 9 million images, and 6k classes. In order to make this project doable we decided to do the hole process just for one class. In that case boats images.

Data used:

classes: class_descriptions_boxable.csv
boxes: oidv6-train-annotations-bbox.csv
images: train-images-boxable-with-rotation.csv
10 open-images-dataset-train_n.tsv files with all images urls.

With all those datasets we managed to create a .tsv file with all images urls containing boats, around 26k 

We also created a .csv file with all the data of those images and boxes around 79k boxes for those 26k images.

Once we had the .tsv file we uploaded it to google cloud storage bucket and made it public in order to be able to download all images from their urls through a google cloud url transfer data and store them in the bucket.


#### Image preprocessing, creating X_data and y_data

- Accessing all images in the bucket, resize, convert to numpy array.
- Match each image numpy array with the boxes data for that image.
- Create X_data and y_data
