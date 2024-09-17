# Literature Search

There are two goals for a literature search: learning about existing work and creating an artifact for future reference.
This artifact can be a spreadsheet or text document depending on your preference.
Regardless of form, the artifact should contain:
* link to the papers
* summaries (goal, contributions, what’s good/bad, potential questions to authors)
* context of the paper (year of publication, authors, venue)
* why you’re reading it
When determining which papers to read, find relevant survey papers to identify key recent works then follow interesting citations from there.
However, make sure to also read widely from recent publications, not just your specialty.

# Hypothesis Formation

First, form a guiding question, which is a broad topic that is of interest and beyond the scope of a single hypothesis, experiment, or paper.
The hypothesis should be able to be tested via experiments to answer part of the guiding question.
Use the literature search to identify common properties across papers that are relevant to your hypothesis.

## Hypothesis Evaluation

Think about what is necessary for the hypothesis to stand out from prior work:
* What makes it novel compared to prior work?
* Is there domain knowledge that is missing in prior work?
* Is there a weakness in prior work that hypothesis testing can resolve?

Also consider [The Heilmeier Catechism](https://www.darpa.mil/work-with-us/heilmeier-catechism):
* What are you trying to do? Articulate your objectives using absolutely no jargon.
* How is it done today, and what are the limits of current practice?
* What is new in your approach and why do you think it will be successful?
* Who cares? If you are successful, what difference will it make?
* What are the risks?
* How much will it cost?
* How long will it take?
* What are the mid-term and final “exams” to check for success?

# Coding for Reproducibility

## Reproducible Environments

Use a virtual environment to ensure that the Python environment can be easily reproduced.
Recommended options are [Pipenv](https://pipenv.pypa.io/en/latest/) or [conda](https://anaconda.org/anaconda/conda).

## Documentation

The commands needed to install the repo, run experiments, and produce figures and tables should be clearly documented.
If code is going to be distributed to others, have someone else try to run the code with only the documentation and fix what goes wrong.

When writing code, use very clear labels (filenames, variable/function/class names) and documentation of files and functions/classes (docstrings).
Try to construct APIs that would be easy to extend (e.g. adding a new dataset).
Using a Python linter integrated into an IDE can support these practices and helps to ensure that code is easy for others to read while automating tedious tasks (fixing spacing inconsistencies, creating docstring templates).

Use Git to manage code, committing frequently and with clear commit messages (“Fixed Bug” ➡️ “Move Tensors to GPU Before Forward Pass”).
Small commits with clear messages make referencing previous work much easier.

## Reproducible Execution

If there is any randomness, set random seeds and ensure results from same seed are consistent by checking loss values and model weights.
Also ensure consistency when stopping and restarting a run, if supported by the repo.

Automated testing with pytest and GitHub Actions can be set up to automatically run tests every commit/day/week and ensure that changes don't break existing code.

Document hardware that you run experiments on (CPUs, GPUs, amount of compute time).

# Data

## Choosing Datasets

Choose datasets used by notable related work, but also identify datasets that are less common but particularly interesting or a good fit for method or task.
If using private datasets, also choose datasets that are publicly available to make experiments that are more easily reproducible.
Creating a table/visualization for how datasets differ (features, labels, number of examples, etc.) can make choosing datasets easier and be useful for communicating dataset information in a paper.

For creating datasets, consider much work/money does it take to gather the raw data, clean it, and create labels.

## Using Datasets

Use a common API to access different datasets (training/testing code doesn’t vary based on dataset).
Determine what data cleaning or augmentations are necessary for your method (what is the data quality?) then integrate into the PyTorch DataLoader.
The PyTorch DataLoader will load samples from a dataset class (e.g. PyTorch ImageFolder) into memory, with dedicated worker processes enabling this to happen in parallel to learning.
```
from torch.utils.data import DataLoader
from torchvision.datasets import ImageFolder

my_dataset = ImageFolder("path/to/data")
my_dataloader = DataLoader(my_dataset, num_workers=4)
```

# Model

Consider what inductive biases from the model can be useful for the data being used.
Use backbones and methods used by notable related works, consider multiple metrics relevant for the experiment task when making these choices.
Basic but widely known baseline methods can clearly communicate improvement of other methods and check that simpler solutions aren't outperforming more popular methods.
For new tasks, using basic extensions of previous methods as baselines can show that a specialized model is better.

Sharing a trained model via GitHub releases makes it easier to show that inputting the test set produces the raw model outputs used in evaluations.
The repository can be set up to allow PyTorch to automatically download trained weights from a link and properly load the model.

# Experiments

Each experiment type should have a main file that parses arguments for hyperparameter input and contains train/test loop functions.
Small experiment changes, such as which dataset is used, should be handled by argument parsing in the same file, not by creating multiple main files.
Tensorboard (local) or Weights and Biases (externally hosted service) should be used to record training diagnostics such as train/validation losses and evaluation metrics.

Use separate files for model architecture, loss functions, data loading, supplemental algorithms, etc. to make it easier to find code.

To conduct hyperparameter searches, use a script to launch the main file with the desired selection of hyperparameters on the GPU server.
This script runs the main file one time per hyperparameter configuration.

To record experiment outputs, use tensors to cache both the true values from the datasets and the predicted values from the model.
For some models, it can be useful to capture soft predictions (e.g. class probabilities) instead of hard predictions (e.g. argmax of class probabilities), so plan ahead for the analysis before running the experiment so you don’t need to collect things you missed later.
Cached values should be written to a separate folder for each model, along with the saved version of the model and training diagnostics.
Values can be saved as PyTorch tensors and/or CSV files.

Consider using [PyTorch Distributed Model Training](https://docs.google.com/presentation/d/1cY6Q5T7guvWsrEjoulFHyocxyl7vjQfEo7C5ZMIL16I/edit?usp=sharing) for methods that need more GPU memory/compute.
Make sure the job meets the resource limit requirements for the cluster partition and doesn't get stuck waiting for resources due to other jobs.

Make sure there is a fair allocation of computational resources across methods (don’t give way more compute for more complex methods).

# Analysis

Create scripts that takes a list of folders to read outputs from and parses them into usable metrics.
It may be necessary to precompute expensive metrics and cache those in new files.
For example, if a figure/metric is taking more than 30 seconds to produce per experiment then precomputation should be used.

Results should consider statistical significance through the use of error bars ([Creating Confidence Intervals for Machine Learning Classifiers](https://sebastianraschka.com/blog/2022/confidence-intervals-for-ml.html) and statistical significance tests 
(see Figure 23 on page 47 of [Model Evaluation, Model Selection, and Algorithm Selection in Machine Learning](https://arxiv.org/pdf/1811.12808)).

When determining whether to present results as a figure or a table, consider which is the most efficient way to communicate the information.
This can vary based on your audience, such as how readable it would be to a domain expert.

Reproducing good figures from previous papers can make result communication easier and enable better comparison to prior work.

# Communicating Results

Create a slideshow for your experiment results as they’re being run to make it easier to communicate in progress work and produces components for use in a future paper early.

Communicate succinctly.
For papers, ensure readers can learn about your good ideas without reading through the densest parts of the paper.
For slideshows, avoid slides that have way too much information.
A title and 1 line of text accompanying a figure is a good baseline for slide density.

Choose a target venue and consider that audience while writing.
What do they want to know and how can they best learn?
This will vary when talking to different levels of proficiency (general audience, academic department, specialist).
What is the audience’s vocabulary and conceptual knowledge base?
What is the audience interested in?
Utility or technical details?

Communicating results is about telling a story.
Making sure a story is being built from the start, instead of building a story to fit results.
Also be honest about claims and limitations of your work.

Write recursively: the abstract presents the purpose and main arguments, the intro expands on the abstract, the paper expands on the intro, the supplement expands on aspects of the paper.

Make artifacts easily accessible.
Create public websites (see [Modern Web Technologies](https://docs.google.com/presentation/d/1Um-XF0vELfqrZBJ_HLySx_7mUXEMzPpmI6EMmWphR3s/edit?usp=sharing)), such as a page on a personal website or a website for a specific project.
Blogs are good for a more general audience and some conferences/workshops are supporting blog tracks.
Write a paper for a conference, workshop, or journal and release an open access version, such as hosting on arXiv.
Publish a code repository with documentation and licensing to distribute for replicability, including model predictions and evaluation scripts to reproduce tables and figures as well as reporting all details about hyperparameter search and model training.

For writing LaTeX papers, use Overleaf for writing a shared document and Zotero to organize references and produce BibTeX.

# References

* [Experimental Standards for Deep Learning in Natural Language Processing Research](https://arxiv.org/pdf/2204.06251)
* [How to Write Defensible VIS Papers](https://docs.google.com/presentation/d/1g-oPa3_0o7zeULe2zydP8uLcSfomuRubKaRCa8fpXHU/edit?usp=sharing)
