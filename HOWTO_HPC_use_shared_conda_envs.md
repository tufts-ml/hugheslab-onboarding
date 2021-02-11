# STEP 0: Log into HPC and request a gpu machine

Request a good gpu machine:

`$ srun -t 0-04:00 -n 1 --mem-per-cpu 2000 --partition ccgpu --gres gpu:a100:1 --pty bash`

# STEP 1: Use the latest shared conda install (miniconda3)

`$ export PATH="/cluster/tufts/hugheslab/miniconda3/bin:$PATH"`

### VERIFY step 1

```
$ which conda
/cluster/tufts/hugheslab/miniconda3/bin/conda
```

# STEP 2: Activate the environment 

`$ conda activate fixmatch-a100`

### VERIFY step 2
```
$ which python
/cluster/tufts/hugheslab/miniconda3/envs/fixmatch-a100/bin/python
```

```
$ conda list | grep "tensorflow\|cuda"
cudatoolkit               10.1.243             h6bb024c_0  
cudnn                     7.6.5                cuda10.1_0  
tensorflow                1.14.0          gpu_py37h74c33d7_0  
tensorflow-base           1.14.0          gpu_py37he45bfe2_0  
tensorflow-estimator      1.14.0                     py_0  
tensorflow-gpu            1.14.0               h0d30ee6_0  
```

# STEP 3: Try out the test code for tensorflow gpus with tf version 1

```
$ cd /cluster/tufts/hugheslab/code/
$ python test_gpu_tensorflow1.py 
```

**Expected output**

```
Listing CUDA_VISIBLE_DEVICES
0
2021-02-11 08:52:01.593067: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcuda.so.1
2021-02-11 08:52:01.872561: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1640] Found device 0 with properties: 
name: A100-PCIE-40GB major: 8 minor: 0 memoryClockRate(GHz): 1.41
pciBusID: 0000:1b:00.0
2021-02-11 08:52:01.872979: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcudart.so.10.1
2021-02-11 08:52:01.875242: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcublas.so.10
...
[lots more log messages]
...
2021-02-11 08:52:02.165437: I tensorflow/compiler/xla/service/service.cc:175]   StreamExecutor device (0): A100-PCIE-40GB, Compute Capability 8.0
[[22. 28.]
 [49. 64.]]
```
