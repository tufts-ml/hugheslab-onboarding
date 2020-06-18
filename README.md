# hugheslab-onboarding
Onboarding info for hugheslab (HPC cluster, etc.)

# How to:

* [Request an HPC account](#hpc-request)
* [Use HPC resources at Tufts](#hpc-quick-start)

# <a name="hpc-request"> HPC request</a>

Fill out the Qualtrics form here: <http://research.uit.tufts.edu/>

Use the information below as your default answers:

```
> Supervisor: Michael Hughes (mhughe02)
> Email: michael.hughes@tufts.edu
> Phone: 6176270548

> Usage Description:
"I am pursuing an active research project with Professor Michael Hughes in statistical machine learning. I need to be able to run multiple jobs in parallel on the cluster, have access to the hugheslab storage space, and be a member of the hugheslab unix group"

> Resources requested:
hugheslab group membership
hugheslab storage space

```

# <a name="hpc-quick-start"> HPC Quick Start</a>

Instructions for both interactive and batch workflow here:

<https://www.cs.tufts.edu/comp/150BDL/2019f/tufts_hpc_setup.html>

### Useful commands

Request an interactive session on GPU

```
srun -t 0-02:00 --mem 2000 -p gpu --gres pgpu02 --pty bash
```


