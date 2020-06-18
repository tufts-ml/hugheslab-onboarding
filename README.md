# hugheslab-onboarding

Onboarding info for hugheslab (how to get access to all the right documents, groups, technology, HPC cluster, etc.)


# How to:

* [Join Tufts ML Slack](#slack-request)
* [Join Tufts ML GitHub organization](#github-request)
* [Request an HPC account](#hpc-request)
* [Use HPC resources at Tufts](#hpc-quick-start)

# This is a Living Document: Please keep me alive and relevant!

Have some useful tips to add? See an error you want to fix? Please make changes! You don't need Mike's permission!

# <a name="slack-request">Slack request</a>

We do quick informal communication via Slack at <tufts-ml.slack.com>

Email Mike and request a slack account.
Give your preferred username.

# <a name="github-request">GitHub request</a>

We use Github to manage lab documents (like this README) and all source code.

Our "Tufts ML" organization is home to both Mike Hughes' research team and Liping Liu's research team.

* (1) If you don't have one yet, create a github account here: <https://help.github.com/en/github/getting-started-with-github/signing-up-for-a-new-github-account>

* (2) Send an email to Mike (or slack message) with your github username. He'll add you to the team here: https://github.com/tufts-ml/


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


