**Instructions**\
Notebook is made to be run in google colab, with drive attached to it\
Four files are given, and should be placed under `/content/gdrive/MyDrive`.\
These are:
* swedish_model_counts.pickle
* swedish_model_endings.pickle
* semi_model.pt
* model.pt

The `swedish_model_*` files contain the data to be loaded into the basic model. \
The `.pt` files contain the trained transformer models. \
If the code is run locally and not in google colab connected to google drive then the paths in 
the code need to be changed to where the files are.
***

The first part of the notebook contains code for the basic model, \
called `Morph`. This can be run by loading the pickle files, but if a new model is to be trained,
then a function gen_func returning a (generator, int) has to be defined. Each batch of the generator should be 
a list with a number of strings of sentences. The int should be the total number of lists in the generator,
meaning the total number of iterations of the generator. A Morph-object can then be trained by 
calling Morph.train(gen_func: func).
***

The second part of the code generates the labeled data using the trained basic model. It uses 
the most common labels and only picks the data where the stem has a certain number of counts in the
count-mapping, and where the label is among the most common.
***

Lastly the tokenizer, transformer and datasets are defined. These are then trained, or loaded from file.
The training can be both (self) supervised or semi-supervised. Self-supervised meaning that the transformer 
only is trained using the labels collected in the previous step. Semi-supervised on the other hand
then means the model utilises all the data.
***

Lastly the models are evaluated on some randomly picked words.