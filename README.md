# CITS4404-ASSG3
This is the submission for CITS4404 assignment3 GANs model

BY: ZIMIN MENG 22665473


## Introduction
File 'extra.mat' contains 50 custom images and is added in the original data set

File 'Code' is the coding file.


## Comparison of the result

The original model has a consistent learning rate lr = 0.0002 by default. And the generaed images and loss are shown below:
 ![image](http://github.com/CITS4404-ASSG3/origin_loss.png)
 
 The quality of image is not vey good. 
 

Then the learning rate is gradually decreasing with epoch increasing. More specifically, with other setting keep same as default, we assign differnt learning rate when epoch = 20, 40, 60 ,80 and total epoch = 100. The generated image is and loss is shown below:


We can see that there is little bit improve of the image quality, but the training loss for generator is much higher and volatile than before while the loss of discriminator is become flatten and stable than before.


Then we using two different method and retrain the model to see whether the quality can be improved or not.
 i.Apply Batch-Normalization both in generator and discriminator
 
 Based on the DCGANs paper, authors mentioned that if applying batchnorm layer to all layers, it will caused the unstable and volitle of the sample. Therefore,it's not suitable to apply batch normalization to Generator's onput layer and Discriminator's iutput layer.
 In here, we apply batch normalization on D's input layer to see how the quality of image changes. 

 
 ii. All layers using Leaky-ReLU as activation functions. 
 By default, we use Leaky-ReLU as discriminator's activation function and ReLU as generator's activation function. In this experienment model, we use ReLU instead of Leaky-ReLU as generator's activation function to see whether the result can be improved or not.
 
 The result shows that
 
 ## Select model and fine tuning again
 The final model we select is same as default setting but only variuos of learning rate which shows the best quality of generated image. 

## Summary 
Trying with different parameters demonstrates that both activation function and batchnormalization can have significant influence on the quality of the image. Improper using batch normalization can increase the volitilty of training loss.

## Benefit of using Batch Normalization
can helping with
Against overfitting problme of the model.
减少了训练时间，而且可以进行深层网络的训练，同时可以使用更大的学习率
会减少梯度爆炸和梯度消失的问题，特别是对sigmoid, tanh这种激活函数
BN使得学习过程更少收到初始化的影响
有对抗过拟合的作用，可以减少正则化的需求
