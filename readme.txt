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

    our best model achived :

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