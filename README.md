# Is BERT self-attention a feature selection method? A case study in classification of scholarly communications
This repository includes full-size images, tables and jupyter notebooks with the experiments reported in the paper **Is BERT self-attention a feature selection method? A case study in classification of scholarly communications** submitted for revision to **ECIR 2021**. The following subjects presented in the paper are covered here:

* [Fine-tuning Language Models for Text Classification](#fine-tuning-language-models-for-text-classification)
  + [Experimental results](#experimental-results)
* [Exploring self-attention heads](#exploring-self-attention-heads)
* [Feature Selection](#feature-selection)
  + [Domain knowledge](#domain-knowledge)
  + [Feature evaluation](#feature-evaluation)

## Fine-tuning language models for Text Classification
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

## Feature Selection

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
  <img src="./images/Figure 3.PNG" title=""/></br>
</p>
