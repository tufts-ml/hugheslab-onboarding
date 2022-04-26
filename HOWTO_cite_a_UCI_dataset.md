The best practice (in my mind) for citing a dataset is to:
- (1) cite the creators directly by citing a paper using the dataset that they wrote (so they get some credit)
- (2) cite the data resource directly via a URL as possible
- (3) be sure to mention the access policy / license for a dataset (so others know if it is available or not)
- (4) include some kind of human readable summary, so readers have a vague context for what the dataset is for

Here's how I'd cite the Anuran Frog Call dataset from UCI:

<img width="357" alt="image" src="https://user-images.githubusercontent.com/2365444/165352096-6f1046cd-8f7c-4153-a909-5fe2def2e3b1.png">

Here's what the refs look like:

<img width="368" alt="image" src="https://user-images.githubusercontent.com/2365444/165352282-875f61b3-9229-4916-b8b3-c5d539ad37b6.png">


And here's the bibtex:

```
@online{anuranFrogDataset2017,
   author       = {Colonna, Juan and Nakamura, Eduardo and Cristo, Marco and Gordo, Marcelo},
   title        = {{Anuran Calls (MFCCs)}},
   year         = {2017},
   howpublished = {UCI Machine Learning Repository},
   editor = {Dua, Dheeru and Graff, Casey},
   url = {https://archive-beta.ics.uci.edu/ml/datasets/anuran+calls+mfccs},
   notes = {CC-BY},
}
```  

Note that *author* field gives credit to individual contributors of this particular dataset, while *editor* field gives credit to the maintainers of the overall repo.

(I still have trouble getting a bibtex to show both authors and editors.) Please let me know if you see a fix.
