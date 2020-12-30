# Classifying Scientific Publications with BERT - Is Self-Attention a Feature Selection Method?

The annotation and classification of scientific literature is a crucial task to make scientific knowledge easily discoverable, accessible, and reusable. We address the annotation as a multilabel classification task using **BERT** and its different flavors specialized in the scientific domain: **BioBert** and **SciBERT**. In our experiments, using papers from **Springer Nature SciGraph**, we confirm that using transformers to train scientific classifiers generally results in greater accuracies compared to linear classifiers (e.g., LinearSVM, FastText)

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

### Running the notebooks in Colaboratory
While these notebooks can be run in _google colaboratory_ with a subset of the articles, to train on the full set of articles used in the paper we advise to use other infrastructure. 

To run the notebooks in Colaboratory go to *https://colab.reasearch.google.com* and use the option *open notebook* from *GitHub* where you can copy and paste the full url of each notebook.

## Fine-tuning language models for text classification

We put into test the following language models to classify research articles: i) BERT and GPT-2, pre-trained on a  general-purpose corpus, ii) SciBERT, pre-trained solely on scientific documents, and iii) BioBERT, pre-trained on a combination of general and scientific text. Below we describe some properties about the pre-training of each language model.

<p align="center">
  <img src="./images/Table 1.PNG" title="Language models pre-training information"/></br>
  Language models pre-training information.
</p>

To fine-tune BERT models we take the last layer encoding of the classification token ``<CLS>`` and add an N-dimensional linear layer, with N the number of classification labels. We use a binary cross-entropy loss function (_BCEWithLogitsLoss_) 
to allow the model to assign independent probabilities to each label.  We train the models for 4 epochs, with batch size 8 and 2e-5 learning rate.

### Experimental results
Below we present the evaluation of the classifiers for 22 first level categories in the ANZRSC (right hand side) and second level categories (left hand side)

<p align="center">
  <img src="./images/Table 2.PNG" title="Evaluation results of the multilabel classifiers"/></br>
  Evaluation results of the multilabel classifiers (f-measure) on first level categories (a), and on second level categories (b).
</p>

## Exploring self-attention heads
 The following images depict the mean weights of the 12 self-attention heads in the last hidden state of the fine-tuned models for two papers titled _BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding_, and _A universal long-term flu vaccine may not prevent severe epidemics_.

 The plots clearly show the so-called vertical pattern, where a few tokens receive most of the attention, such as **training, deep, transformer, language**, and **understanding** in the first sentence, and **flu, vaccine, prevent, severe** and **epidemic** in the second. We do not include in the plots ``<CLS>`` or ``<SEP>``.
 
| <img src="./images/finetuned-bert-2.png" title="BERT" /><p align="center"><b>BERT</b></p>  | <img src="./images/finetuned-bert-3.png" title="BERT" /><p align="center"><b>BERT</b></p> |
|:---:|:---:|
| <img src="./images/finetuned-scibert-2.png" title="SciBERT" /><p align="center"><b>SciBERT</b></p> | <img src="./images/finetuned-scibert-3.png" title="SciBERT" /><p align="center"><b>SciBERT</b></p> |
| <img src="./images/finetuned-biobert-2.png" title="BioBERT-1.1" /><p align="center"><b>BioBERT-1.1</b></p> | <img src="./images/finetuned-biobert-3.png" title="BioBERT-1.1" /><p align="center"><b>BioBERT-1.1</b></p> |

We also extract the words with higher attention than the average attention in each sentence. Note that the words are highly relevant to the corresponding scientific category. 

<p align="center">
Visualization  of  average  weights  in  the  self  attention  heads  of  the  last layer.
</p>

<p align="center">
  <img src="./images/Table 3.PNG" title="Most attended words above average attention in the fine-tuned models"/></br>
  Most attended words above average attention in the fine-tuned models.
</p>

## Feature selection
In this section we compare the lists of the attended words above average attention with feature selection algorithms frequently used in text classification. 

<p align="center">
  <img src="./images/Table 4.PNG" title="Word overlap"/></br>
  Word overlap: most attended and feature selection results. algorithm.
</p>
We also compare the rankings using the Rank-Biased overlap metric:

<p align="center">
  <img src="./images/Figure 2.PNG" title="Rank-biased overlap at different p values"/></br>
  Rank-biased overlap at different p values (X axis) between most attended words and selected by feature selection algorithm.
</p>

### Domain knowledge
We search the words attended above average in **ConceptNet** and leverage the relation _HasContext_ to identify the domains where they are commonly used:

<p align="center">
  <img src="./images/Table 5.PNG" title="Number of words per ANZRSC category that match the corresponding context in ConceptNet."/></br>
  Number of words per ANZRSC category that match the corresponding context in ConceptNet.
</p>

In BERT and SciBERT, self-attention identifies more domain-relevant words than feature selection methods. However, this is not the case for BioBert. 

Weighing the words by their term frequency (TF), attended words remain more domain-relevant than those obtained through feature selection. In fact, the domain relevance of the frequent attended words is greater or on pair with those selected when TF/IDF is used to weigh the output of feature selection method

### Feature evaluation

To measure the stability of the features we compute the mean Jaccard coefficient between the different subsets of words generated by each method using 5-folds:

<p align="center">
  <img src="./images/Table 6.PNG" title="Stability of the features measured using Jackard similarity coefficient"/></br>
  Stability of the features measured using Jackard similarity coefficient.
</p>

 We use the set of features to learn classifiers for the 22 first level categories using Logistic Regression (LR), Naive Bayes (NB), Random Forest (RF), Neural Networks (NN), and SVM: 
 
<p align="center">
  <img src="./images/Figure 3.PNG" title="Classifiers performance using distinct feature sets and number of features"/></br>
  Classifiers performance using distinct feature sets and number of features. x axis is the number of features used to train each classifier.
</p>

We observe that traditional feature selection methods like chi-square and information gain mainly help to learn more accurate classifiers than the set of most attended words by the language models. This observation clearly indicates that the success of BERT models in this task is not only driven by the self-attention mechanism but also by the contextualized outputs of the transformer, which are the input of the added classification layer.


