If you have parameters in your model, which should be saved and restored in the state_dict, but not trained by the optimizer, you should register them as buffers.

Buffers won’t be returned in model.parameters(), so that the optimizer won’t have a change to update them.

register_parameter will be returned by parameters() and will be used by optimizer for training.
