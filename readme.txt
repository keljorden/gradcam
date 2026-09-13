date: 09.09.2026

actions:

    1. implemented forward and backward hooks
    2. implemented grad-cam
    3. initially targeted the whole model.block2
    4. found out that the last layer was a maxpool so switched target to model.block2[2]

observations :

    - model seems to use the negative space in the image to make prediction
    - while the accuracy is high and the model have generalize well, we still want the mosel to learn correctly.

    - the core cause of this behaviour was our failure to implement data augmentation and dropout.

future tasks :

    1. train a new model
        - implement data augmentation
        - implement dropout



date: 13.09.2026

observation: 

our best model :


my_best_CNN_model(
  (layers): Sequential(
    (0): Conv2d(1, 32, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
    (1): BatchNorm2d(32, eps=1e-05, momentum=0.1, affine=True, bias=True, track_running_stats=True)
    (2): ReLU()
    (3): Conv2d(32, 32, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
    (4): BatchNorm2d(32, eps=1e-05, momentum=0.1, affine=True, bias=True, track_running_stats=True)
    (5): ReLU()
    (6): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
    (7): Dropout2d(p=0.1, inplace=False)
    (8): Conv2d(32, 64, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
    (9): BatchNorm2d(64, eps=1e-05, momentum=0.1, affine=True, bias=True, track_running_stats=True)
    (10): ReLU()
    (11): Conv2d(64, 64, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
    (12): BatchNorm2d(64, eps=1e-05, momentum=0.1, affine=True, bias=True, track_running_stats=True)
    (13): ReLU()
    (14): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
    (15): Dropout2d(p=0.1, inplace=False)
    (16): Conv2d(64, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
    (17): BatchNorm2d(128, eps=1e-05, momentum=0.1, affine=True, bias=True, track_running_stats=True)
    (18): ReLU()
  )
  (classifier): Sequential(
    (0): Flatten(start_dim=1, end_dim=-1)
    (1): Linear(in_features=6272, out_features=128, bias=True)
    (2): ReLU()
    (3): Dropout(p=0.2, inplace=False)
    (4): Linear(in_features=128, out_features=10, bias=True)
  )
)

    
    
    
  ----------  our best model achived :   ------------

 epoch 93:
	train loss: 	0.1778 	||	 train acc: 	0.9340
	test loss: 	0.2059 	||	 test acc: 	0.9281

epoch 94:
	train loss: 	0.1728 	||	 train acc: 	0.9370
	test loss: 	0.2139 	||	 test acc: 	0.9238

epoch 95:
	train loss: 	0.1743 	||	 train acc: 	0.9358
	test loss: 	0.2057 	||	 test acc: 	0.9265

epoch 96:
	train loss: 	0.1736 	||	 train acc: 	0.9377
	test loss: 	0.2073 	||	 test acc: 	0.9273

epoch 97:
	train loss: 	0.1732 	||	 train acc: 	0.9373
	test loss: 	0.2154 	||	 test acc: 	0.9252

epoch 98:
	train loss: 	0.1742 	||	 train acc: 	0.9375
	test loss: 	0.2067 	||	 test acc: 	0.9271

epoch 99:
	train loss: 	0.1727 	||	 train acc: 	0.9369
	test loss: 	0.2080 	||	 test acc: 	0.9255




....................     BUT      ...............


Grad-CAM results shows something different?

    - there are some reasonable heatmaps but most of them show no activities?????
    - what does that even means?
    

    - out testing shows no major signs of overfitting?
    - is our grad-cam not working correctly?


    ............. FOUND THE PROBLEM ..............

so the problem was that we were targeting model.layer[16] which is the last Conv2d before Flatten() because we generally dont target BatchNorm 
and Relu.

but since we were not getting any accurate representation because of it, I targeted the model.layers[18] which is the last layer before Flatten
ans now we are getting qualitatively better insight into our models decisions.