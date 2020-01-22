# Real-Time Object Detection using Tensorflow Object_detection API (windows)


### This is a beginner friendly tutorial.
_Author: Richard Joy_  
richardjoy530@gmail.com

---
You can do object detection using tensorflow even with very little to no knoledge in python by following this tutorial. Actually tensorflow makes is much easier to do machine learning. All we really need to know is how to setup all the packages and various installations, and how to not mess up with different versions of the same package or library.

Just keep on reading you will get the hang of it  :)

    NOTE: some files in this are a bit large you will be required to download around 800Mb throughout this 
    process if your internet connection is slow it will take a lot of time

## 1. The setup

#### Installing Anaconda Environment

There are mainly two different variations on tensorflow:        
`tensorflow`-it runs on the systems CPU and `tensorflow_gpu`- it runs on GPU, this is fast but not all GPUs are supported by tensorflow and its installation is not quite simple.

There are various versions of tensorflow, and this is the most annoying part that i've seen. Some python modules doesn't work with `tensorflow_v2.0` and others work only with `tensorflow2.0`. Therefore, I highly recommend using virtual environments for installing multiple versions of tensorflow. Dont worry, i'll tell you how. For virtual environment, I am using Anaconda(python3.7) 

Download and install Anaconda from this link: https://www.anaconda.com/distribution/#download-section keep the installation settings as it is.

#### Setting up workspace

A good pratice in doing a project is keeping everything organized. Especially if you are doing this types of project.
For this, lets make a folder `Tensorflow` in our `Documents` folder. We will be saving all our required recources and scripts to this folder. The paths of these folders will be used later in our programs.


#### Creating Virtual Environment

Now that you have anaconda installed, lets make an environment for our program.

We will be using `tensorflow 2.0` for this tutorial.

open Anaconda Promt from Start menu
![Annotation%202020-01-22%20124206.png](attachment:Annotation%202020-01-22%20124206.png)

    
    Throughout this tutorial, there are two types of codes. The ones that start with '!' and the ones that dont.
    
    '!' These are shell commands. These are to be run in our Anaconda Prompt with the "Tensorflow" folder as our command line location. You can change the location of command line by using "cd Documents\Tensorflow" in the Anaconda prompt as shown here:
  


```python
!cd Documents\Tensorflow 
```

 ![Annotation%202020-01-22%20130038.png](attachment:Annotation%202020-01-22%20130038.png)
    
    The other comands are python commands. We'll see how and where to run it later in this tutorial.
    
Now create an environment by typing this in our Anaconda prompt with our folder `Tensorflow` as our command line location.


```python
!conda create -n tensorflow2 pip python=3.6
```

This will create an environment named `tensorflow2` and with python3.6 as the interpreter.



Next, activate the environment by:


```python
!conda activate tensorflow2
```

Once you do this you'll see `(tensorflow2)` at the begning of the command line, it means you are in that environment. We can create as many environments as we need, the modules that we install in an environment is exclusive to that environment. As a result, there will not be any clash between different versions of any module. Well, now we understood why it is crusial to use virtual environments. 
![Annotation%202020-01-22%20132153.png](attachment:Annotation%202020-01-22%20132153.png)


#### Installing modules
Now that we are in the virtual env'  lets install tensorflow.


```python
!pip install tensorflow==2.*
```

we can install python libraries using `pip` or `conda`. These are some python libraries that we need in our code, so lets install it using `pip` or if it doesnt work use `conda` as shown below.


```python
!pip install pillow lxml jupyter matplotlib cython numpy
```

if any of the above libraries did not sucessfully install, then use `conda` just replace `pip` as the code:


```python
!conda install opencv -y
```

#### Installing protobuffers 


In simple words: Protobuffers are some formats/structure in which we can save data (like .XML and .json files) and are language independent(these files can be used by different languages). We need to compile these before we can use it.



There are various different methods to install this. The safest method that i've found is shown below.


Download `(eg: protoc-3.11.2-win64.zip)` and extract the latest version of protoc for windows from :

https://github.com/protocolbuffers/protobuf/releases



Now go to the folder `Program Files` in your `C:` drive and create a folder named `Google Protobuf`
copy the extracted folders into this folder

now it should look like this:
![Annotation%202020-01-22%20100017.png](attachment:Annotation%202020-01-22%20100017.png)

Now we have to add this to the system path.
search `environment variables` in the `Start menu` ![Annotation%202020-01-22%20095759.png](attachment:Annotation%202020-01-22%20095759.png)

Select `Environment Variables`

![Annotation%202020-01-22%20100254.png](attachment:Annotation%202020-01-22%20100254.png) 

In `System variables` select `path` and edit.

Now `Add` a new path to the list `C:\Program Files\Google Protobuf\bin` ![Annotation%202020-01-22%20100731.png](attachment:Annotation%202020-01-22%20100731.png)

Protobuf installation is complete


#### Downloading Tensorflow/Models

NOTE: This download is around 500 Mb

You can either download this folder from https://github.com/tensorflow/models/archive/master.zip 

and extract this zip file into our `Tensorflow` folder and rename the `model-master` folder to just `model`. The directory must be as shown below:
![Annotation%202020-01-22%20200255.png](attachment:Annotation%202020-01-22%20200255.png)

##### or

Install `git` and clone the directory as it is.(I recommend using `git`, its more convinent otherthan going to the website, downloading and then extracting..... aahhh thats a mess. )


```python
!conda install -c anaconda git -y
```


We can get the same by this shell command (Remember to run this shell commands in our `Tensorflow` folder location as we've seen before)



```python
!git clone https://github.com/tensorflow/models.git
```

#### Protobuf Compiling.
Lets compile those protobuf files that we've seen above. The `protos` files in our `Tensorflow` folder is located at `models/research/object_detection/protos/` it can be combined using a shell command:
You need to open a new Anaconda shell and activate our environment by `!conda activate tensorflow2`





But unlike other commands, we shuld run this in prompt with location model/research
```
just run these codes it should get you there.
```


```python
!cd Documents/Tensorflow/model/research
!protoc object_detection/protos/*.proto --python_out=.
```

#### Building and Installing Object Detection files

Building and Installing this baisically means : Telling our python interpreter where to search for, if a module is requested by our code. In other words, in our python code, we are importing various files from the `model` folder. So by building and installing, our python interpreter will know where to look at if such a file is requested.

These commands must be run at `Tensorflow\models\research`

```
just run these commands since we are already in this location
```


```python
!python setup.py build
!python setup.py install
```

### Congratulations!!! our Setup part is complete. Now, have a glass of water!!!

## 2. Python Code

You can just copy the entire code blocks below to a notepad and save it as `run.py` in our `Tensorflow` Folder.

After that you can read the explanation of each code block down below:

```

    copy all the codes to a text document in notepad as shown :


```

![Annotation%202020-01-22%20211555.png](attachment:Annotation%202020-01-22%20211555.png)

```

    Save the file as 'run.py' as shown:


```
![Annotation%202020-01-22%20211703.png](attachment:Annotation%202020-01-22%20211703.png)

```


    Now your 'Tensorflow' folder should look like this


```

![Annotation%202020-01-22%20211733.png](attachment:Annotation%202020-01-22%20211733.png)


To run the file `run.py`:
```
enter the shell command given below in the anaconda prompt at the location of our 'Tensorflow' folder
```


```python
!cd..
!cd..
!python run.py
```

#### 1. Importing required modules for our program 

There is nothing much to say in here, its just telling the interpreter that these are the files that we need to run this program.

``` 
if you come across any error here, then that means that module is not installed in the environment. You can fix it by runinng ' !pip install _______ ' in the prompt.
```


```python
import numpy as np
import os
import six.moves.urllib as urllib
import sys
import tarfile
import tensorflow as tf
import zipfile
import pathlib


from collections import defaultdict
from io import StringIO
from matplotlib import pyplot as plt
from PIL import Image
from IPython.display import display
```

Next we are importing the modules that we build and installed before. If u get an error here, its because the building and installing was not sucessful


```python
from object_detection.utils import ops as utils_ops
from object_detection.utils import label_map_util
from object_detection.utils import visualization_utils as vis_util
```

#### 2. Maping old functions to new
There are still some modules that use `tensorflow_v1` and we have installd `tensorflow_v2` so these bits of code just maps the old functions the corresponding functions in the new version.


```python
# patch tf1 into `utils.ops`
utils_ops.tf = tf.compat.v1

# Patch the location of gfile
tf.gfile = tf.io.gfile
```

#### 3. Defining a function to Load a given model

`load_model` is a generic function which takes a parameter `model_name` which is the name of the pre trained models.
`model_name` can be the name of any of the trained models in this link : https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md

This function downloads the model from the internet and  saves it in our `Tensorflow` folder


```python
def load_model(model_name):
    base_url = 'http://download.tensorflow.org/models/object_detection/'
    model_file = model_name + '.tar.gz'
    model_dir = tf.keras.utils.get_file(
        fname=model_name, 
        origin=base_url + model_file,
        untar=True)

    model_dir = pathlib.Path(model_dir)/"saved_model"

    model = tf.saved_model.load(str(model_dir))
    model = model.signatures['serving_default']

    return model
```

`PATH_TO_LABELS` is the location of the `mscoco_lable_map.pbtxt`. It is a file which has all the names and tags of the dectectable objects. ie, if the program detects an object, it looks in th lable map to find its name.

`category_index` its like a dictionary which stores all the name of the objects in the `mscoco_lable_map.pbtxt` and its tag(a number)


```python
# List of the strings that is used to add correct label for each box.
PATH_TO_LABELS = 'models/research/object_detection/data/mscoco_label_map.pbtxt'
category_index = label_map_util.create_category_index_from_labelmap(PATH_TO_LABELS, use_display_name=True)
```

#### 4. Loading the model
This is where we run the function `load_model` that we made above. Notice the `model_name` here we use the 
   model: `ssd_inception_v2_coco_2017_11_17`. You can see this name in the link above.
   
And this model is saved in `detection_model`



```python
model_name = 'ssd_inception_v2_coco_2017_11_17'
detection_model = load_model(model_name)
```

    Downloading data from http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2017_11_17.tar.gz
    278126592/278126337 [==============================] - 114s 0us/step
    INFO:tensorflow:Saver not created because there are no variables in the graph to restore
    

#### 5. Defining a function to detect objects

`run_inference_for_single_image` is a function that takes a `model` and an `image`. It uses the given `model` to detect the objects in the given `image`


```python
def run_inference_for_single_image(model, image):
    
    # The image is converted to a number array for computation and this array replaces the image in the variable 'image'.
    image = np.asarray(image)
    
    # The number array is converted to a tensor object for tensorflow to work, this tensor object is our input
    # to the model and is saved in 'input_tensor'
    input_tensor = tf.convert_to_tensor(image)
    input_tensor = input_tensor[tf.newaxis,...]
    
    # This is where the MAGIC happens. Our image processed in the form of tensor object is given to the
    # model. 
    output_dict = model(input_tensor)

    # All outputs are batches tensors.
    # Convert to numpy arrays, and take index [0] to remove the batch dimension.
    # We're only interested in the first num_detections.
    num_detections = int(output_dict.pop('num_detections'))
    output_dict = {key:value[0, :num_detections].numpy() 
                   for key,value in output_dict.items()}
    output_dict['num_detections'] = num_detections

    # detection_classes should be ints.
    output_dict['detection_classes'] = output_dict['detection_classes'].astype(np.int64)

    # Handle models with masks:
    if 'detection_masks' in output_dict:
        # Reframe the the bbox mask to the image size.
        detection_masks_reframed = utils_ops.reframe_box_masks_to_image_masks(
                                    output_dict['detection_masks'], output_dict['detection_boxes'],
                                    image.shape[0], image.shape[1])      
        detection_masks_reframed = tf.cast(detection_masks_reframed > 0.5, tf.uint8)
        output_dict['detection_masks_reframed'] = detection_masks_reframed.numpy()
    
    return output_dict
```

#### 6. Detecting frame by frame

This set of code is just taking each frame of the video image by image and passing it to the `run_inference_for_single_image` function that we defined before. This process in looped in the `while` loop given below. Further explanation is given in the code...#....


```python
import cv2
cap = cv2.VideoCapture(0)
try:
    def run_inference(model, cap):
        while True:
            #this is where  we capture each frame image by image.
            ret, image_np = cap.read()
            # this image along with the model is given to the previous function as it gives the detection details
            # the output is stored in 'output_dict' and it contains the objects name, probablity score, 
            # and the boundary box
            output_dict = run_inference_for_single_image(model, image_np)
            # Visualization of the results of a detection.
            vis_util.visualize_boxes_and_labels_on_image_array(
                image_np,
                output_dict['detection_boxes'],
                output_dict['detection_classes'],
                output_dict['detection_scores'],
                category_index,
                instance_masks=output_dict.get('detection_masks_reframed', None),
                use_normalized_coordinates=True,
                line_thickness=8)
            cv2.imshow('object_detection', cv2.resize(image_np, (800, 600)))
            if cv2.waitKey(25) & 0xFF == ord('q'):
                cap.release()
                cv2.destroyAllWindows()
                break
except Exception as e:
    print("Done")
    cap.release()
run_inference(detection_model, cap)
```

#### Congratulations you've made if to the end.

#### If you have got the final output, just take a moment and appricate yourself for doing this

#### If you did not get the output, find out what went wrong , take it as a challenge. This way you will learn a lot.

---

# The End

I will be making similar tutorials on : Training object detection on custom objects. You can always find my tutorials at my github-repo: https://github.com/richardjoy530/object_detection_tutorials

Feel free to contact me if you ran into some troubles : richardjoy530@gmail.com