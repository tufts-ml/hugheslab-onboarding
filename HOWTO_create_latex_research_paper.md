Just as a reference, here's my recommended "template" for a workshop submission (obviously, this is for ICLR, and you would change the style file (*.sty) following the directions of your target workshop)

https://www.overleaf.com/read/yfgppzwqtcxs

I like having overleaf as a way to look quickly at the "latest" version, but I mostly use overleaf's Git integration features so that I can edit locally on my laptopThus, I prefer the "many small text files" approach.

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

I also recommend that each figure and table has text source that is standalone .tex file.... this makes it super easy to move figures around in the document (we just change in main where we import the figure)

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
