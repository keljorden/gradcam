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