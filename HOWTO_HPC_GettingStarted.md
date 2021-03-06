Jump to:
* [Interactive](#interactive)
* [Batch](#batch)
* [New A100 GPUs](#a100-gpus)


# <a id="options">Key Options</a>

See full list of options here: <https://slurm.schedmd.com/sbatch.html>

Here's some example settings for a CPU-only job

```
--nodes 1                     # Number of hardware nodes needed. Not sure this ever needs to be >1 unless you are sure cross-machine overhead is low.
--ntasks 1                    # Number of tasks your job will launch. Usually should just be 1, unless you will be spawning multiple processes within your job.
--partition batch/interactive # If you want sbatch, use 'batch'. If you want an interactive job, use 'interactive'
--cpus-per-task 1             # Number of cpus needed. Usually numpy ops on CPU can do fine with 1 but benefit from 2-4 cores with diminishing returns after 8.
--mem-per-cpu 32000           # Memory in MB needed by each requested CPU. Usually want 1GB - 32GB, except with big data jobs.
--export ALL                  # Any environment variable in current workspace is exported to the task. Useful for setting up envs.
```


Here's some example settings for the new A100 gpus 

```
--nodes 1                   # Number of hardware nodes needed. Not sure this ever needs to be >1 unless you are sure cross-machine overhead is low.
--ntasks 1                  # Number of tasks your job will launch. Usually should just be 1, unless you will be spawning multiple processes within your job.
--partition ccpgu           # 
--gres gpu:a100:1           # Request an A100 GPU 
--cpus-per-task 1           # Number of cpus needed. Usually numpy ops on CPU can do fine with 1 but benefit from 2-4 cores with diminishing returns after 8.
--gpus-per-task 1           # Number of gpus needed. Usually just need 1. Getting multiple GPUs to work well in parallel is not easy in MCH experience. 
--mem-per-cpu 15000         # Memory in MB needed by each requested CPU. Usually want 1GB - 32GB, except with big data jobs.
--mem-per-gpu 5000          # Memory in MB needed by each requested GPU. A100s max out at 32GB.
--export ALL                # Any environment variable in current workspace is exported to the task. Useful for setting up envs.
```

# If you have not used SLURM before but have used IBM's LSF or Sun grid engine

See the "rosetta stone" here, super useful for translating commands across different grid systems:

https://slurm.schedmd.com/rosetta.pdf


# Convenient SLURM commands


Want to know the history of a completed job? Try this:

```
sacct -j 428 --format=User,JobID,Jobname,partition,state,time,start,elapsed,nnodes,ncpus,nodelist,ReqGRES%20
```

Note that the "%20" suffix ensures it prints out 20 characters worth of info about the requested gpu resources.

For more, see: 
https://docs.rc.fas.harvard.edu/kb/convenient-slurm-commands/

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

# <a name="a100-gpus"> Using the new A100 GPUs </a>

There are 5 different "nodes" (e.g. specific hardware boxes), each with 8 A100s. So there are 40 GPUs in total! (which we share across the university).

Instructions for access below (note that we are moving to a new virtualized workflow with a different SSH login node address)

Many services on the new architecture (login, slurm controller, web gateways) are virtualized which will bring a number of useful features. Stay tuned as plans move forward on that project.The new architecture mounts the SAME file systems, modules, etc.

#### Login

To connect up, ssh to login.pax.tufts.edu which round robins between two actual login nodes login-prod-01.pax.tufts.edu and login-prod-02.pax.tufts.edu  

```
ssh your_username@login.pax.tufts.edu
```

If you are on non-Tufts network, please make sure have Tufts VPN connected first.

#### Jobs

Similar to the other GPU nodes on the cluster you can use the gres syntax but the gpu are type a100 rather than p100, v100 or t4 you may be used to specifying.
See examples below:

All hugheslab research students are in the linux group ccgpu and will be able to submit jobs to the ccgpu partition (-p ccgpu) using the regular slurm commands, srun, sbatch jobs can be specified using partition, gres examples such as “-p ccgpu --gres=gpu:a100:3” (requesting 3 GPUs, max 8 GPUs per node). 

```
srun -p ccgpu --gres=gpu:a100:3 --pty bash
```
