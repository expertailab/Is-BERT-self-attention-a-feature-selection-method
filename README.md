# Is BERT self-attention a feature selection method? A case study in classification of scholarly communications
This repository includes full-size images, tables and jupyter notebooks with the experiments reported in the paper **Is BERT self-attention a feature selection method? A case study in classification of scholarly communications** submitted for revision to **ECIR 2021**. The following subjects presented in the paper are covered here:

* [Fine-tuning Language Models for Text Classification](#fine-tuning-language-models-for-text-classification)
  + [Experimental results](#experimental-results)
* [Exploring self-attention heads](#exploring-self-attention-heads)

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
