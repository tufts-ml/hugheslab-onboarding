Jump to:
* [Interactive](#interactive)
* [Batch](#batch)


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
