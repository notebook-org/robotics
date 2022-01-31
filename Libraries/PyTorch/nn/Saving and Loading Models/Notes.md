Three core functions:
1. torch.save: Save a serialized object to disk.
    - Uses pickle under the hood.
    - Models, tensors, and dictionaries of all kinds of object can be saved using this function.
2. torch.load: Uses pickle's unpacking facilities to deserialize pickled object files to memory.
3. torch.nn.Module.load_state_dict: Loads a model's parameter dictionary.

## What is a state_dict?
- In PyTorch, the learnable parameters of an torch.nn.Module model are contained in the model's parameters (accessed with model.parameters()).
- **state_dict:** Its a simple Pithon dictionary object that maps each layer to its parameter tensor.

## Saving and Loading Model for Inference
1. Save:
  ```python
  torch.save(model.state_dict(), PATH)
  ```
2. Load:
  ```python
  torch.load_state_dict(torch.load(PATH))
  ```

A common PyTorch convention is to save models using either a .pt or .pth file extension.

- Remember that you must call model.eval() to set dropout and batch normalization layers to evaluation mode before running inference.
- Failing to do this will yield inconsistent inference results.

## Save/Load Entire Model
1. Save:
  ```python
  torch.save(model, PATH)
  ```
2. Load:
  ```python
  model = torch.load(PATH)
  ```

The disadvantage of this approach is that the serialized data is bound to the specific classes and the exact directory structure used when the model is saved. 

