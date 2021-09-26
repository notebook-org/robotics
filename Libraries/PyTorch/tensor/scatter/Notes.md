tensor.scatter(dim, index, src, reduce=None) --> Tensor

Writes all values from the tensor src into self at the indices specified in the index tensor.

* **dim (int):** the axis along which to index
* **index (LongTensor):** the indices of elements to scatter
* **src (Tensor or float):** the source element(s) to scatter


![Screenshot from 2021-09-24 07-59-25](./ss/Screenshot%20from%202021-09-24%2007-59-25.png)
