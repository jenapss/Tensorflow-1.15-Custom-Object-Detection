# ✅ Tensorflow-1.15-Custom-Object-Detection📸
This readme describes every step required to get going with your own object detection classifier:

Setting up the Object Detection directory structure
Gathering and labeling pictures
Generating training data
Creating a label map and configuring training
Training
Exporting the inference graph
Testing and using your newly trained object detection classifier
Appendix: Common Errors
# 👨🏻‍💻 Prerequisities: 
-Tensorflow 1.15.0, opencv-python==4.1.1.26,LabelImg

This example requires you to install Tensorflow 1.15 for training, opencv-python==4.1.1.26, and LabelImg for annotating your images

Just type in your terminal:

`pip install tensorflow==1.15`

# Installation procedures

Before starting doing custom object detection let's install and set up coding environment. For that make sure you download this repo to your local PC and inside `/research/` directory run following commands: 
```
python setup.py build
python setup.py install
```

These commands should install Tensorflow Object Detection API to your PC

# 📸 Data Collection & Annotation:
I used my smartphone to take photos of vegetables and used the LabelIMG annotation tool to annotate them. My dataset is made up of more than 6000 images of three classes - carrots, cucumbers and bananas. So for every class I have collected around 2000 images. The annotation part was the most time-consuming part of the project. I have made some research on existing online AI-powered annotation tools and here is the list of them: 



You can use any image dataset collection methods you want such as [Google Open Images](https://storage.googleapis.com/openimages/web/index.html), web scraping, taking photos by yourself and etc. The main goal here is to collect as many images as you can. But for this kind of project 400-600 images would also be enough. After you finished collecting images, now it is time to start annotating them. For this task I used LabelImg. LabelImg is very easy in use an can be used to make annotate in PASCAL VOC and YOLO formats. Make sure you watch some YouTube tutorials about LabelImg in order to know how to use this tool.

Full Documentation for this tool can be found [here](https://github.com/tzutalin/labelImg)


## TFRECORDS 
With the images labeled, it’s time to generate the TFRecords that serve as input data to the TensorFlow training model. This tutorial uses the xml_to_csv.py and generate_tfrecord.py scripts from Dat Tran’s Raccoon Detector dataset, with some slight modifications to work with our directory structure.

First, the image .xml data will be used to create .csv files containing all the data for the train and test images. From the \object_detection folder, issue the following command in the Anaconda command prompt:
  
```
python xml_to_csv.py
```
This creates a train_labels.csv and test_labels.csv file in the \object_detection\images folder.

Next, open the generate_tfrecord.py file in a text editor. Replace the label map starting at line 31 with your own label map, where each object is assigned an ID number. This same number assignment will be used when configuring the labelmap.pbtxt file in Step 5b.

For example, say you are training a classifier to detect basketballs, shirts, and shoes. You will replace the following code in generate_tfrecord.py:
```
# TO-DO replace this with label map
def class_text_to_int(row_label):
    if row_label == 'Carrot':
        return 1
    elif row_label == 'Cucumber':
        return 2
    elif row_label == 'Zucchini':
        return 3
    else:
        None
```

Then, generate the TFRecord files by issuing these commands from the \object_detection folder:

```
python generate_tfrecord.py --csv_input=images\train_labels.csv --image_dir=images\train --output_path=train.record
python generate_tfrecord.py --csv_input=images\test_labels.csv --image_dir=images\test --output_path=test.record
```


## Background/Negative Images.

If you are a newbie to object detection then you might be encountering the topic of usage of background/negative images for the first time. Do not worry, I described this phenomenon in this [article](https://medium.datadriveninvestor.com/what-is-not-taught-in-object-detection-tutorials-and-books-dc33ab4c3063). 
  

# Configuring the config files before training.
  

# 💪 Training Model

# 🆒 Exporting trained model


