# Drowsiness-Detection
<p align="center" width="100%">
    <img width="33%" src=![image](https://user-images.githubusercontent.com/73955220/210215415-7d0219fc-bf69-45ce-8067-f1ac2be806a7.png)> 
</p>
  
  
  
In this project we will train our model on open and close eyes dataset then use that with face recognition library to check if the driver is sleeping or  not.
This project will work in two phases in first phase we will train a model on eyes if open/closed 
using different models. After achieving good accuracy and low loss we will give it to another code 
which is phase two in which we will use face detector libraries to detect a face so we can see where 
the eyes are and then employ our model to predict if our outputs are good or not.
For first phase training I tried different model architectures, but they were too big as I wanted my 
project to run on a micro-controller. I designed a model of my own to reduce the model file size 
but when I tried to further decrease it, I got many issues like validation loss was enormous. So, the 
model I used is the max size reduced and efficient model which I tried to develop.
There are many face-detection libraries, but I went with this was because it was more accurate and 
gave better results as compared to other libraries such as harsh cascade even thought it might be 
more computationally complex or consuming.
You can Futher learn about his project by reading the Pdf file given in the rep.
Step by step information is also provided in the coded file.
