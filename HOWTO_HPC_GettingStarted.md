Jump to:
* [Interactive](#interactive)
* [Batch](#batch)
* [New A100 GPUs)(#gpu)


# <a id="interactive">Interactive Workflow</a>

IF you want to manually interact with good computer over next few hours via terminal, you want "interactive".

Instructions for interactive workflow:

<https://www.cs.tufts.edu/comp/150BDL/2019f/tufts_hpc_setup.html>

## Requesting an interactive session on GPU

### To request a V100

Some of the best GPUs around. Only a few available (as of 2020). 

```
srun -t 0-02:00 --mem 2000 -p gpu --gres=gpu:v100 --pty bash
```


### To request a P100

```
srun -t 0-02:00 --mem 2000 -p gpu --gres=gpu:p100 --pty bash
```

### To request a K20

```
srun -t 0-02:00 --mem 2000 -p gpu --gres=gpu:k20 --pty bash
```

### To request a T4 on the *preempt* partition

*Warning*: a preempt job can be canceled at anytime if the owner of that node requests access to the resource.

```
srun -t 0-04:00 --mem 2000 -p preempt --gres gpu:t4:1 --pty bash
```


# <a id="batch">Batch Workflow</a>

If you want to assign long-running jobs for the computer to do without your intervention over next 2 - 100 hours, you want "batch".

Instructions for using a batch (offline, non-interactive) workflow are here:

<https://github.com/tufts-ml-courses/comp150-bdl-19f-assignments//blob/master/hpc_example/README.md>

The tutorial above will walk you through autoencoder (AE), just like in [BDL class Homework 4]().

Will use "batch" workflow to explore several settings:

    learning rate (lr) of 0.010 and 0.001
    number of hidden units of 032, 128, and 512

By launching *many separate* jobs, one for each configuration.

Please be a good citizen when using the grid. Do not request too many resources at once or use more than you really need.

# Using the new A100 GPUs

There are 5 different "nodes" (e.g. specific hardware boxes), each with 8 A100s. So there are 40 GPUs in total! (which we share across the university).

Instructions for access below (note that we are moving to a new virtualized workflow with a different SSH login node address)

Many services on the new architecture (login, slurm controller, web gateways) are virtualized which will bring a number of useful features. Stay tuned as plans move forward on that project.The new architecture mounts the SAME file systems, modules, etc.

#### Login

To connect up, ssh to login.pax.tufts.edu which round robins between two actual login nodes login-prod-01.pax.tufts.edu and login-prod-02.pax.tufts.edu  
ssh your_username@login.pax.tufts.edu
If you are on non-Tufts network, please make sure have Tufts VPN connected first.

#### Jobs

Similar to the other GPU nodes on the cluster you can use the gres syntax but the gpu are type a100 rather than p100, v100 or t4 you may be used to specifying.
See examples below:

All hugheslab research students are in the linux group ccgpu and will be able to submit jobs to the ccgpu partition (-p ccgpu) using the regular slurm commands, srun, sbatch jobs can be specified using partition, gres examples such as “-p ccgpu --gres=gpu:a100:3” (requesting 3 GPUs, max 8 GPUs per node). 

```
srun -p ccgpu --gres=gpu:a100:3 --pty bash
```
