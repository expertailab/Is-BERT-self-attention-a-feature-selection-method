# Classifying Scientific Publications with BERT - Is Self-Attention a Feature Selection Method?

The annotation and classification of scientific literature is a crucial task to make scientific knowledge easily discoverable, accessible, and reusable. We address this multilabel classification task using **BERT** and its different flavors specialized in the scientific domain: **BioBert** and **SciBERT**. In our experiments, using papers from **Springer Nature SciGraph**, we confirm that using transformers to train scientific classifiers generally results in greater accuracies compared to linear classifiers(e.g., LinearSVM, FastText)

To shed light on BERT internals, we analyze the self-attention mechanism inherent of the transformer architecture. Our findings show that **the last layer of BERT attends to words that are semantically relevant for the scientific fields associated with each publication** (see [Exploring self-attention heads](#exploring-self-attention-heads)). This observation suggests that self-attention actually performs some type of feature selection for the fine-tuned model.

This repository includes jupyter notebooks to reproduce the experiments reported in the paper **Classifying Scientific Publications with BERT - Is Self-Attention a Feature Selection Method?** accepted in the *43rd European Conference on Information Retrieval* **ECIR 2021**. In addition, we present some of the paper highlights.


# Table of content

* [Jupyter Notebooks](#Jupyter-notebooks)
* [Fine-tuning language models for text classification](#fine-tuning-language-models-for-text-classification)
  + [Experimental results](#experimental-results)
* [Exploring self-attention heads](#exploring-self-attention-heads)
* [Feature selection](#feature-selection)
  + [Domain knowledge](#domain-knowledge)
  + [Feature evaluation](#feature-evaluation)
  
## Jupyter notebooks
In the __notebooks__ directory of this repository we release self-contained notebooks, including dataset and required libraries, that allows to reproduce the following experiments: 

* Fine-tune BERT, SciBERT and BioBERT to classify research articles into multiple research fields in the ANZRSC taxonomy.
 
   [BertModels4ArticleClassification.ipynb](./notebooks/BertModels4ArticleClassification.ipynb)
   
* Visualize self-attention in the last layer of the BERT models

   [BertModelsAttentionHeadsVisualization.ipynb](./notebooks/BertModelsAttentionHeadsVisualization.ipynb)

* Get lists of most attended words above average in the last layer of the BERT models

   [BertModelsAttendedWordsOverAverage.ipynb](./notebooks/BertModelsAttendedWordsOverAverage.ipynb)

Note that while this notebooks can be run in _google colab_ with a subset of the articles, to train on the full set of articles used in the paper we advise to use other infrastructure. 

To run the notebooks in google colab go to *https://colab.reasearch.google.com* and use the option *open notebook* from *GitHub* where you can copy and paste the full url of each notebook.

## Fine-tuning language models for text classification
<p align="center">
  <img src="./images/Table 1.PNG" title="Language models pre-training information"/></br>
  Language models pre-training information.
</p>

### Experimental results
<p align="center">
  <img src="./images/Table 2.PNG" title="Evaluation results of the multilabel classifiers"/></br>
  Evaluation results of the multilabel classifiers (f-measure) on first level categories (a), and on second level categories (b).
</p>

## Exploring self-attention heads
 
| <img src="./images/finetuned-bert-2.png" title="BERT" /><p align="center"><b>BERT</b></p>  | <img src="./images/finetuned-bert-3.png" title="BERT" /><p align="center"><b>BERT</b></p> |
|:---:|:---:|
| <img src="./images/finetuned-scibert-2.png" title="SciBERT" /><p align="center"><b>SciBERT</b></p> | <img src="./images/finetuned-scibert-3.png" title="SciBERT" /><p align="center"><b>SciBERT</b></p> |
| <img src="./images/finetuned-biobert-2.png" title="BioBERT-1.1" /><p align="center"><b>BioBERT-1.1</b></p> | <img src="./images/finetuned-biobert-3.png" title="BioBERT-1.1" /><p align="center"><b>BioBERT-1.1</b></p> |

<p align="center">
Visualization  of  average  weights  in  the  self  attention  heads  of  the  last layer.
</p>

<p align="center">
  <img src="./images/Table 3.PNG" title="Most attended words above average attention in the fine-tuned models"/></br>
  Most attended words above average attention in the fine-tuned models.
</p>

## Feature selection

<p align="center">
  <img src="./images/Table 4.PNG" title="Word overlap"/></br>
  Word overlap: most attended and feature selection results. algorithm.
</p>
<p align="center">
  <img src="./images/Figure 2.PNG" title="Rank-biased overlap at different p values"/></br>
  Rank-biased overlap at different p values (X axis) between most attended words and selected by feature selection algorithm.
</p>

### Domain knowledge

<p align="center">
  <img src="./images/Table 5.PNG" title="Number of words per ANZRSC category that match the corresponding context in ConceptNet."/></br>
  Number of words per ANZRSC category that match the corresponding context in ConceptNet.
</p>

### Feature evaluation

<p align="center">
  <img src="./images/Table 6.PNG" title="Stability of the features measured using Jackard similarity coefficient"/></br>
  Stability of the features measured using Jackard similarity coefficient.
</p>
<p align="center">
  <img src="./images/Figure 3.PNG" title="Classifiers performance using distinct feature sets and number of features"/></br>
  Classifiers performance using distinct feature sets and number of features. x axis is the number of features used to train each classifier.
</p>



