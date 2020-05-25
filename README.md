# final_project_ih_jun_2020

## Deep learning

### Open Image - Object Detection

https://storage.googleapis.com/openimages/web/download.html

Te idea of the project is to train a neuronal network capable of detecting classes of objects.
As working with images need high computational resourses the project is developed in google cloud, using a Tesla K80 GPU.

#### Creating the Dataset

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


#### Image preprocessing, creating X_data and y_data

- Accessing all images in the bucket, resize, convert to numpy array.
- Match each image numpy array with the boxes data for that image.
- Create X_data: image numpy array
- Create y_data: box locations and confidence (Xmin, Xmax, Ymin, Ymax, confidence)

#### Creating the neuronal network
single shot vs multi shot \
ssd model \
Resnet and keras \
Yolo v1, v2, v3 (https://github.com/FMsunyh/keras-yolo, https://github.com/ecaradec/humble-yolo)

#### Doubts
- Each box should go with one image? how to indicate those images having more than one box?
- There are two kinds of boxes Xmin, Xmax, Ymin, Ymax. But also XClick1X, XClick2X,	XClick3X,	XClick4X,	XClick1Y,	XClick2Y,	XClick3Y,	XClick4Y? xclick are manually drawn boxes using the method presented in [1], were the annotators click on the four extreme points of the object. How to proceed.

- If at some point we want to train for more than one Label we should add Label to y_data

- Do we need to add more info to y_data (Label, 'IsOccluded', 'IsTruncated', 'IsGroupOf', 'IsDepiction', 'IsInside')

IsOccluded: Indicates that the object is occluded by another object in the image. / IsTruncated: Indicates that the object extends beyond the boundary of the image. / IsGroupOf: Indicates that the box spans a group of objects (e.g., a bed of flowers or a crowd of people). We asked annotators to use this tag for cases with more than 5 instances which are heavily occluding each other and are physically touching. / IsDepiction: Indicates that the object is a depiction (e.g., a cartoon or drawing of the object, not a real physical instance). / IsInside: Indicates a picture taken from the inside of the object (e.g., a car interior or inside of a building).
