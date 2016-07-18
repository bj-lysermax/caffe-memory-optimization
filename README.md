Memory optimizations for Caffe.

This is a revision and optimization of fengfu-chris's verson of caffe-memory-optimization.

===
### 0. Minor errors of fengfu-chris's verson of caffe-memory-optimization
  net.cpp: In function BackwardFromTo, layer_type is not defined 
  
  batch_norm_layer.cpp/batch_norm_layer.cu: In function Backward_cpu/Backward_gpu, num_by_chans_bak_ is not needed since num_by_chans_ is not revised after forward propagation

### 1. Backward memory optimization
  In the backward propagation of each layer, the mem of bottom_vecs is reallocate before real backward calculation. Then, the mem of top_vecs is reset after backward propagation.

### 2. BatchNorm layer memory optimization
   Mem of temporal variable is reallocate and reset in each forward and backward propagation

### 3. Performance
   The peak mem cost of TrainNet after mem optimization is approximately 1/3 of original Caffe. But, compared to original Caffe, the time cost will go up to about 1.3 times in single GPU mode and 2.5 times in multiple GPUs mode. 
