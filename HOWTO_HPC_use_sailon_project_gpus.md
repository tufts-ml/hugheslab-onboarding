For students involved with the SAIL-ON project, we have a special server with some GPUs available that is *separate* from the Tufts HPC cluster.

This server has 4 RTX2080Ti GPUs, good for prototyping. Of course, the HPC cluster has 40+ GPUs, but the sailon server is specialized for this project so you won't compete with non-project users.

## Server login account creation process

1) Request account access from Zachary Haga (zachary.haga(at)tufts.edu, or @Zachary Haga on the ACT-NOW SAILON slack)

CC Mike Hughes when you make the request

Simplest to make your username the same as your Tufts EECS username (e.g. Mike Hughes is `mhughes`)

2) Be sure to change your password from the default

## Server login

You'll do this process every time you log in:

1) SSH into tufts EECS systems. Directions: http://systems.eecs.tufts.edu/secure-shell-ssh/

2) Then ssh into the sailon server

```
$ ssh [your_sailon_username]@sailon
$ # ... you'll be prompted for your password
```

3) Then access the resources

```
# Check GPU status
$ nvidia-smi
# Train models, etc.
```

## Server facts

Ubuntu 18.04 (with Desktop)
NVIDIA Driver Installation (440.82)
GPU Validation Test Passed (4x GeForce GeForce RTX2080Ti)
1x 2TB M.2 NVMe SSD (OS)
QuickStartGuide_Exxact_NGC_EMLI.pdf located at the user's home folder Off board Video (Left most GPU, see attached page for more info)

NVIDIA Driver (440.82)
Docker version 19.03.9
Anaconda 2, 3
CUDA 10.2, CUDA 10.1, CUDA 10.0
