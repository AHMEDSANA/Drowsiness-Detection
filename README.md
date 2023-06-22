# Drowsiness-Detection

**Project Working:**

This project will work in two phases in first phase we will train a model on eyes if open/closed using different models. After achieving good accuracy and low loss we will give it to another code which is phase two in which we will use face detector libraries to detect a face so we can see where the eyes are and then employ our model to predict if our outputs are good or not.

For first phase training I tried different model architectures, but they were too big as I wanted my project to run on a micro-controller. I designed a model of my own to reduce the model file size but when I tried to further decrease it, I got many issues like validation loss was enormous. So, the model I used is the max size reduced and efficient model which I tried to develop.

There are many face-detection libraries, but I went with this was because it was more accurate and gave better results as compared to other libraries such as harsh cascade even thought it might be more computationally complex or consuming.

**Step 1 : Downloading and Uploading dataset**

First, we will download the Drowsiness Detection Dataset from Kaggle the link is given below:

**Dataset Link:** [Human eyes open\close | Kaggle](https://www.kaggle.com/datasets/tauilabdelilah/mrl-eye-dataset)

After downloading this dataset from the website, we will replace the word in labels as follows:

**Open Eyes:** 1

**Close Eyes:** 0

After this we will upload the data on our drive that we will mount on the Google Colab.

**Step 2 : Changing runtime and loading the data in Colab**

- Create a new notebook in Colab
- Go on the Runtime tab and change the Runtime type to GPU and save it.
- Mount the Drive in which you uploaded the Dataset you want to train the model.
- After mounting the data read the dataset using the code given below.
- This code will unzip the file into the Colab hardisk.

  !unzip /content/drive/MyDrive/Drowsiness2.zip -d /content/Untitled

**Step 3 : Importing Libraries and setting our Train and Test data Paths.**

 path = '/content/Untitled/data'

 train\_dir = os.path.join(path, 'train')

 test\_dir = os.path.join(path, 'test')

 print(train\_dir)

 print(test\_dir)

 print(os.listdir(train\_dir))

**Step 4 : Preprocessing and Generation of Data**

- Now we input image size of what we want.
- Batch size and Epochs.
- Preprocess our data (Rescale, zoom, flip, shear)
- Use an image generator to generate our data in class mode.

**Step 5 : My Model**

- My Neural Network Uses 13 layers.
- Four Convolution layers
- Four Pool layers
- One Flatten layer
- One Dropout
- Three Dense Layers
- Stride of the Model is 1
- And filter size is 3x3

**Step 6 : Compiling our model**

- Now we will select our loss function according to our classes.
- And at the end we choose our Optimizers and Metrics.
- I used Adam optimizer and Binary Cossentropy.

**Output:**

<p align="center">
<img width="" height="" src="https://user-images.githubusercontent.com/73955220/210314080-80ca9241-5302-46d3-94db-e68c0645db2f.png">
</p>

**Step 8 : Predicting/Validating**

- Now we will predict to check if our model was trained right or not.
- And see some output images with prediction.


**Output:**

<p align="center">
<img width="" height="" src="https://user-images.githubusercontent.com/73955220/210316496-b42f5ad5-3073-4c20-a155-d44bd0b35d33.png">
</p>


**Step 9: Final (testing our model)**

- Use face detection model to detect eyes.
- Apply our eyes closed and open model to detect the output.
- Then apply conditions accordingly to detect our output.


# Face Detection and Predinction of Drowsiness IRL

To run the real time detection you will have to run it on ur personal pc and use ide's like Spyder,Jupyter etc as colab doesnot allow access to your camera.

To run the file for detection of drowsiness we will have to run:

- Install Face Detection library
  
  pip install playsound
  
  pip install -U PyObjC
  
  pip install face_recognition
  
  pip install -U tensorboard_plugin_profile

- Sound Alarm Library
   
   pip install playsound
  
  
- Then give the location of the trained model file (h file)

- Then run the code.


**Output :**

<p align="center">
<img width="" height="" src="https://user-images.githubusercontent.com/73955220/210318546-4310aaca-ad5b-4956-b0ca-3e7495cb2f04.png">
</p>


**Implementation on Controller:**

We can run our code and implement the model on Raspberry Pie as the total storage memory of our model is 18 mb and that of face library is 100 mb and the total space memory required for our model is 150 mb.

The Ram required to run a three second video to detect the output is:


<div align="center">


| CNN Layers | Memory | Parameters |
| --- | --- | --- |
| Input Layer | 128x128x3=49152 | 0 |
| Conv2D | 126x126x32=508032 | 896 |
| Max Pooling | 63x63x32=127008 | 0 |
| Conv2D | 61x61x64=238144 | 18496 |
| Max Pooling | 30x30x64=57600 | 0 |
| Conv2D | 28x28x128=100352 | 73856 |
| Max Pooling | 14x14x128=25088 | 0 |
| Conv2D | 12x12x256=36864 | 295168 |
| Max Pooling | 6x6x25=9216 | 0 |
| Flatten | 1x1x9216=9216 | 0 |
| Dropout | 1x1x9216=9216 | 0 |
| Dense | 1x1x128=128 | 1179776 |
| Dense | 1x1x256=256 | 33024 |
| Dense | 1x1x1=1 | 257 |
| RAM in Bytes | 1170273x4=4681092 |
**RAM in Mega Bytes = 4.681092 MB** 

</div>


As we can see from above calculations the total RAM required for running the model is 4MB for forward and one frame. Extra procedures will also require some memory usage which cannot be calculated.

We can also reduce the RAM usage and processing usage by reducing the number of frames it operates to detect the drowsiness of the driver.

**Conclusion:**

We detected drowsiness of a driver using CNN and Python Face Recognition libraries and succeeded in reducing the memory and processing it uses so it is implementable on the Controller.

We used face recognition software so we can detect eyes on a face as the Neural

Network doesn't directly detect images form a face so we used it to detect face and see where the eyes are present then use the trained model to detect our output.
