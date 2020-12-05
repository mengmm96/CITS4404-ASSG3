# CITS4404-ASSG3
This project applying DCGANs model with using  [SVHN data set](http://ufldl.stanford.edu/housenumbers/) to generate fake house number pictures.
Additionally, an extra 50 processed house-number pics is added to the original data set to see whether this will infulence the quality of generated fake image.

BY: ZIMIN MENG 


## Introduction
File 'extra.mat' contains 50 custom images and is added in the original data set

File 'ASSG3_DCGANS_ZIMINM' is the python file.

## Comparison of the result

### Part I. Various learning rate
The original model has a consistent learning rate lr = 0.0002 by default. And the generaed images and loss are shown below:
 ![image](https://github.com/mengmm96/CITS4404-ASSG3/blob/master/origin_loss.png)
 
 ![image](https://github.com/mengmm96/CITS4404-ASSG3/blob/master/origin_image.png)
 The quality of image is not vey good.
 

Then the learning rate is gradually decreasing with epoch increasing. More specifically, with other setting keep same as default, we assign differnt learning rate when epoch = 20(0.01), 40(0.005), 60(0.002) ,80(0.001) and total epoch = 100. The generated image is and loss is shown below:
Loss:
 ![image](https://github.com/mengmm96/CITS4404-ASSG3/blob/master/various_epoch_loss.png)
Image:
 ![image](https://github.com/mengmm96/CITS4404-ASSG3/blob/master/various_epoch_image.png)
We can see that there is little bit improve of the image quality, but the training loss for generator is much higher and volatile than before while the loss of discriminator is become flatten and stable than before. This maybe caused by the learning rate is much higher than before, thus we imply another trying with a smaller learning rate to epoch = 20(0.001), 40(0.0005), 60(0.0002) ,80(0.0001) and total epoch = 100. Theere is no obvious different between the quality of generated image and the generator loss is slightly smaller than the previous setting.

### Part II. Changing other items
Then we using two different method and retrain the model to see whether the quality can be improved or not.
 
#### i.Apply Batch-Normalization to discriminator's input layer
 
 Based on the DCGANs paper, authors mentioned that if applying batchnorm layer to all layers, it will caused the unstable and volitle of the sample. Therefore,it's not suitable to apply batch normalization to Generator's onput layer and Discriminator's iutput layer.
 In here, we try toapply batch normalization on D's input layer to see how the quality of image changes. 
Loss:
 ![image](https://github.com/mengmm96/CITS4404-ASSG3/blob/master/D_BN_loss.png)
Image:
 ![image](https://github.com/mengmm96/CITS4404-ASSG3/blob/master/D_BN_image.png)
 
 The result shows that applying batch normalization on D's input layer will cause a volatile for the result which is not surprised since this is same as mentioned in papoer.
 
#### ii. Using Leaky-ReLU instead of ReLU as activation functions for generator. 
 By default, we use Leaky-ReLU as discriminator's activation function and ReLU as generator's activation function. In this experienment model, we use ReLU instead of Leaky-ReLU as generator's activation function to see whether the result can be improved or not.
 
 Loss:
 ![image](https://github.com/mengmm96/CITS4404-ASSG3/blob/master/leaky-relu_loss.png)
Image:
 ![image](https://github.com/mengmm96/CITS4404-ASSG3/blob/master/leaky-relu_image.png)
 
 The result shows that the loss of generator keeps volite and increasing butt the loss for discriminator is gradually decreasing and become flatten after 400 , but in general worse than before. This result is not surprised since it's same as author mentioned.
 
 ## Select model 
The final model we select is same as default setting but only variuos of learning rate which shows the best quality of generated image, which is epoch(lr) = 20(0.01), 40(0.005), 60(0.002) ,80(0.001).

## Summary 
From this experiment, we can see adding new 50 images not helping to generate higher quality image. Trying with different parameters demonstrates that both activation function and batchnormalization can have significant influence on the quality of the image. There are lots of benefit of busing batch normalisation such as helping with gradient vanishing/exploding problem as well as problem of overfitting, but improper using batch normalization can increase the volitilty of training loss. And the result for this assignment also demenstrated that using  ReLU as activation function for generators can produces more stable loss and thus are more suitable to use.

