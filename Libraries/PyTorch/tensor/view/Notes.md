PyTorch allows a tensor to be a View of an existing tensor.

View tensor shares the same underlying data with its base tensor.

Supporting View avoids explicit data copy, thus allows us to do fast and memory efficient reshaping, slicing and element-wise operations.

![Screenshot from 2021-09-24 07-40-59](./ss/Screenshot%20from%202021-09-24%2007-40-59.png)
