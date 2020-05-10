# CIFAR 10 : Classification

## Index  
1. [Objective](#objective)  
2. [Model Summary](#model-summary)
2. [Receptive Field Calculations](#receptive-field-calculations)
3. [Result Summary](#result-summary)
4. [Result Visualizations](#result-visualizations) (misclassification/accuracy/loss)

## Objective   
1. Code uses GPU - **Done**  
2. Use the architecture to C1,C2,C3,C4,O (basically 3 MPs) - **Done**  
3. Total RF must be more than 44 - **Done(RF = 96)**  
4. One of the layers must use Depthwise Separable Convolution - **Done**  
5. One of the layers must use Dilated Convolution  - **Done**  
6. Use GAP (compulsory):- add FC after GAP to target #of classes (optional) - **Done**  
7. Achieve 80% accuracy, as many epochs as you want. Total Params to be less than 1M - **Done**   
8. All the code is split and individual modules are called upon for execution - **Done**    

## Model Summary  
![image](https://user-images.githubusercontent.com/36323558/81509423-34152f80-9328-11ea-9c22-8138b09ec692.png)

## Receptive Field Calculations 

-------Net summary------   

**Input Block**  
* input image:     
	+ n features: 32   
	+ jump: 1    
	+ receptive size: 1    
	+ start: 0.5    
* conv1:   
	+ n features: 30    
	+ jump: 1    
	+ receptive size: 3    
	+ start: 1.5    
	
**Convolution Block - 1**  : Depthwise Separable layer  

* conv2:   
	+ n features: 36    
	+ jump: 1    
	+ receptive size: 5    
	+ start: -1.5    
* conv3:   
	+ n features: 44    
	+ jump: 1    
	+ receptive size: 5    
	+ start: -5.5    

**Transition Block - 1**	

* MP1:   
	+ n features: 22    
	+ jump: 2    
	+ receptive size: 6    
	+ start: -5.0    
* conv4:   
	+ n features: 22    
	+ jump: 2    
	+ receptive size: 6    
	+ start: -5.0    

**Convolution Block - 2** : Dilated layer  	

* conv5:
	+ n features: 22    
	+ jump: 2    
	+ receptive size: 14    
	+ start: -5.0    
* conv6:   
	+ n features: 22    
	+ jump: 2    
	+ receptive size: 22    
	+ start: -5.0    
* conv7:   
	+ n features: 22    
	+ jump: 2    
	+ receptive size: 30    
	+ start: -5.0    

**Transition Block - 2**		

* MP2:   
	+ n features: 11    
	+ jump: 4    
	+ receptive size: 32    
	+ start: -4.0    
* conv8:   
	+ n features: 11    
	+ jump: 4    
	+ receptive size: 32    
	+ start: -4.0    

**Convolution Block - 3** : Dilated layer  	

* conv9:   
	+ n features: 11    
	+ jump: 4    
	+ receptive size: 48    
	+ start: -4.0    
* conv10:   
	+ n features: 11    
	+ jump: 4    
	+ receptive size: 64    
	+ start: -4.0    
* GAP:   
	+ n features: 1    
	+ jump: 36    
	+ receptive size: 96    
	+ start: 16.0   

**Convolution Block - 4**	

* conv11:   
	+ n features: 1    
	+ jump: 36    
	+ receptive size: 96    
	+ start: 16.0    

------------------------    

## Result Summary

The following image gives an idea of which model seems to achieve the best Validation Accuracy.  

Best Model based on Accuracy : **Model with L2 regularization**  
Model Parameters : **160,384**  
Receptive Field : 96  
No of Blocks : 4 Convolution blocks, 2 Transition blocks, 1 GAP block  

**In Best Model with L2 :**   

Best Train Accuracy : 83.50%  
Best Test Accuracy : 81.49%  

## Result Visualizations

### Validation Accuracy   
![Validation Accuracy](./images/Validation_Accuracy.png)

### Validation Loss  
![Validation Loss](./images/Validation_Loss.png)

### 25 misclassified images for L2 : Best Model  
![L2 misclassified](./images/Val_L2_Misclassification.png)

