## Answer
- There are a few operations on Tensors in PyTorch that do not change the contents of a tensor, but change the way the data is organized.
- These operations include:
    - narrow()
    - view()
    - expand()
    - transpose()
- Tensor x is contiguous but tensor y is not because its memory layout is different to that of a tensor of same shape made from scratch.
- Note that the word "contiguous" is a bit misleading because it's not that the content of the tensor is spread out around disconnected blocks of memory. Here bytes are still allocated in one block of memory but the order of the elements is different!
- When you call contiguous(), it actually makes a copy of the tensor such that the order of its elements in memory is the same as if it had been created from scratch with the same data.
- Normally you don't need to worry about this. You're generally safe to assume everything will work, and wait until you get a RuntimeError: input is not contiguous where PyTorch expects a contiguous tensor to add a call to contiguous().

