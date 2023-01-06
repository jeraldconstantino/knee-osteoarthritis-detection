<h1 align="center"> Knee Osteoarthritis Detection </h1>
<p align="center"> A deep learning approach project that utilized a mask R-CNN algorithm to distinguish between healthy and degenerative knees based on the narrowing of the knee joint space using plain radiograph. </p>

## How to use this project
To clone and use this project, make sure that you have [Git](https://git-scm.com/) installed in your machine. Kindly follow the instructions below:    
* Use `cd` command to go to your desired directory where you want to save the files.
1. Clone this repository
```
$ git clone https://github.com/jeraldconstantino/knee-osteoarthritis-detection
```
2. Upload the [train](https://github.com/jeraldconstantino/knee-osteoarthritis-detection/tree/main/train) and [test](https://github.com/jeraldconstantino/knee-osteoarthritis-detection/tree/main/test) dataset in your Google Drive account or any cloud platforms. 

3. Upload the .ipynb files in [Google Colab](https://colab.research.google.com/).
> Aside from the Google Colab, you can also use Jupyter Lab from the [Anaconda](https://www.anaconda.com/) software. However, this step requires you physical GPU and consume your time in manually installing the required dependencies.

## Model Training and Evaluation (using Google Colab)
1. open the [Model Training and Evaluation file](https://github.com/jeraldconstantino/knee-osteoarthritis-detection/blob/main/Model%20Training%20and%20Evaluation.ipynb).
2. Check if you are using the virtual GPU to accelerate the processing or training stage. To check, click and follow these steps: `Runtime > Change runtime type > Hardware accelerator`.
3. Run the cell for Google Drive connection.
4. Change the file directory included in the code depending on the path where your dataset is saved.
```
cd /content/drive/[path]
```
5. Install the required dependencies. 
> Don't forget to click the `restart runtime` after installing the depedencies. You can locate it from the output of this cell. 
6. Run all the succeeding code. 

### Model Training code:
```
import pixellib
from pixellib.custom_train import instance_custom_training

train_maskrcnn = instance_custom_training()
train_maskrcnn.modelConfig(network_backbone = "resnet101", num_classes= 3, batch_size = 4) # You can also used Resnet-50 by changing the network backbone to "resnet50"
train_maskrcnn.load_pretrained_model("/content/drive/path")  # path of the pretrained model 
train_maskrcnn.load_dataset("/content/drive/path")   # path of the dataset
train_maskrcnn.train_model(num_epochs = 300, augmentation=True,  path_trained_models = "mask_rcnn_models")
```
Don't forget to keep track on the generated model with a file extension of `.h5`.

### Model Evaluation code:
```
import pixellib
from pixellib.custom_train import instance_custom_training

train_maskrcnn = instance_custom_training()
train_maskrcnn.modelConfig(network_backbone = "resnet101", num_classes=3) # if you used Resnet-50, don't forget to change the network backbone to "resnet50" too.
train_maskrcnn.load_dataset("/content/drive/Shareddrives/path")           # path of the dataset
train_maskrcnn.evaluate_model("/content/drive/Shareddrives/deep_learning/mask_rcnn_models")  # path of your generated models.
```
To check what AI model has a higher accuracy. Look at the output generated by this code, the last number for each output indicates your model accuracy. For instance, this output `...path/mask_rcnn_models/mask_rcnn_model.036-0.139314.h5 evaluation using iou_threshold 0.5 is 0.941667` indicates that the model has an accuracy of 94.17%.





