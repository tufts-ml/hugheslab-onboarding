# Process for creating figures for any paper

1) Make the raw data for each results figure / table stored somewhere simple (like a CSV or whatever on disk)

2) Write a standalone script to plot each figure / make each table just by loading the CSV and making the plot

That way, if we want to make cosmetic changes later, it's super easy to do (we just rerun the plotting script).
And you don't need to retrain models or recompute numbers or something

# Preamble for figure saving code

(sets good font sizes, etc)

```
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style("whitegrid") # or use "white" if we don't want grid lines
sns.set_context("notebook", font_scale=1.25)
```

# Exporting figures

Always save the figure as a PDF (so we get vector graphics if possible, esp for line plots like the ROC curves):

```
 plt.savefig("my_figure.pdf", bbox_inches='tight', pad_inches=0)
```
