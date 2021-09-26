# model.train() and model.eval()

## References
* [Source](https://stackoverflow.com/questions/51433378/what-does-model-train-do-in-pytorch)

## Answer
- model.train() tells your model that you are training the model.
- model.eval() tells your model that you are testing the model.
- So effectively layers like dropout, batchnorm etc. which behave different on the train and test procedures know what is going on and hence can behave accordingly.
- Use model.training flag to check if model is in training or test mode.
    - It is False, when in testing mode, and True when in training mode.
