
# Getting started with Overleaf and LaTeX

https://www.overleaf.com/learn/latex/Free_online_introduction_to_LaTeX_(part_1)

# Workflow

In slack, ping collaborators and let them know you'll edit Section A, B, and C for next X hours.

Always check slack to make sure no one else is editing your sections before you get started


## Workflow in your browser

* Edit the source directly

## Workflow on your local machine

* Git clone the overleaf into a folder on your machine 
* Build/edit the document locally

MCH recommends TexPad: <https://www.texpad.com/>

* Verify that overleaf is set up as a remote repository

#### To view the current remote url

```
$ git remote -v
```

Expected output:
```
origin	https://git.overleaf.com/609a6fc02a1f8d0e9cdc81dd (fetch)
origin	https://git.overleaf.com/609a6fc02a1f8d0e9cdc81dd (push)
```

#### To edit the remote url
```
git remote set-url origin https://git.overleaf.com/5f204125... [Overleaf ID]
```

#### Once you're satisfied with changes, commit and push to the overleaf repo

```
git push origin master
```

# HughesLab template 

Just as a reference, here's my recommended "template" for a workshop submission (obviously, this is for ICLR, and you would change the style file (*.sty) following the directions of your target workshop)

https://www.overleaf.com/read/yfgppzwqtcxs

I like having overleaf as a way to look quickly at the "latest" version, but I mostly use overleaf's Git integration features so that I can edit locally on my laptop. Thus, I prefer the "many small text files" approach.

* main.tex is the primary file you can build by calling "pdflatex", as in the associated Makefile
* Inside main, after the package importing and title and so one, we use \input{abc.tex} to draw content from a specific .tex file (e.g. the text of the abstract or the text of the intro, etc)

```
\begin{abstract}
\input{abstract.tex}
\end{abstract}\section{Introduction}
\input{intro.tex}\section{Methods}
\input{methods_short.tex}\section{Evaluation}
\input{results_short.tex}
```

I also recommend that each figure and table has text source that is standalone .tex file.... 

Reasons for standalone tex files for each item in the paper:
* chance of conflict goes down a lot. if you are editing a.txt and I am editing b.txt, git will merge no problem without us even thinking about avoiding the other's turf
* git diffs and manipulation with almost any other program is so much easier to understand.... you can look at line 33 not line 1033
* reorganizing the paper is so much easier. You can just comment out or move one \input{} statement in the main document, and a whole section gets rearranged. this is super easy to do while others are *editing other sections or even the section you are moving*

## Figures

For a figure with many subplots, I find the easiest hting to do is create a separate PDF for each subplot, and use Latex to craft the perfect composition of these subplots into an overall figure, like this example:

```
\begin{figure}[!h]
\setlength{\tabcolsep}{0.3cm}
\begin{tabular}{m{1.5cm} m{8cm}}
Lowell General Hospital &     \includegraphics[width=0.7\textwidth]{figures/LGH.pdf}
	\\ ~ \\~ \\ 
Melrose-Wakefield Hospital &    \includegraphics[width=0.7\textwidth]{figures/MWH.pdf}
	\\ ~ \\~ \\ 
Tufts Medical Center & 
    \includegraphics[width=0.7\textwidth]{figures/TMC.pdf}
\end{tabular}
```

Don't worry if this doesn't make sense to you, I've got like 12 years of TeX experience so I'm happy to help you create the perfect figure TeX code once you create the tex files

Speaking of how to create figures, please please please follow the advice here: https://github.com/tufts-ml/hugheslab-onboarding/blob/master/HOWTO_create_publication_ready_figures.md

All plots you make in matplotlib should be PDF format with vectorized graphics (unless they have bitmap image content taken by a real camera). See the instructions above for how to export these plots
