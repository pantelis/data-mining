---
title: NMT Metrics - BLEU
---

## NMT Metrics - BLEU

In 2002, IBM researchers developed the BiLingual Evaluation Understudy (BLEU) that remains, with its many variants to this day, one of
the most respected and reliable methods for machine translation.

### [Intuition](https://en.wikipedia.org/wiki/BLEU)

The BLEU algorithm evaluates the precision score of a candidate machine translation against a reference human translation. To refresh your memory the following picture is a easy picture for you to memorize and draw every time you forget the definitions of precision and recall.

![precision-recall](images/precision-recall.png)

The reference human translation is a assumed to be a model example of a translation, and we use _n-gram_ matches as our metric for how similar a candidate translation is to it. Why simple precision can't be used? Consider the following example of poor machine translation output with high precision metric using unigrams. 

| Output      |       |     |     |     |     |
| ----------- | ----- | --- | --- | --- | --- | --- |
| Candidate   | the   | the | the | the | the | the | the |
| Reference 1 | the   | cat | is  | on  | the | mat |
| Reference 2 | there | is  | a   | cat | on  | the | mat |

Of the seven words in the candidate translation, all of them appear in the reference translations. Thus the candidate text is given a unigram precision of,

$$ P= \frac{m}{w_{t}} = \frac{7}{7}=1$$

where $m$ is number of words from the candidate that are found in the reference, and $w_t$ is the total number of words in the candidate. This is a perfect score, despite the fact that the candidate translation above retains little of the content of either of the references.

The modification that BLEU makes is fairly straightforward. For each word in the candidate translation, the algorithm takes its maximum total count, $m_{max}$, in any of the reference translations. In the example above, the word "the" appears twice in reference 1, and once in reference 2. Thus $m_{max}=2$.

For the candidate translation, the count $m_{w}$ of each word is clipped to a maximum of $m_{max}$ for that word. In this case, "the" has $m_w=7$ and $m_{max}=2$ thus $m_w$ is clipped to 2. These clipped counts $m_w$ are then summed over all distinct words in the candidate. This sum is then divided by the total number of unigrams in the candidate translation. In the above example, the modified unigram precision score would be:

$$P= \frac{2}{7}$$

### Calculation

A simple practical example is shown next. Note that the weights are specified as a tuple where each index refers to the gram order. To calculate the BLEU score only for 1-gram matches, you can specify a weight of 1 for 1-gram and 0 for 2, 3 and 4 (1, 0, 0, 0). 

```python
# 1-gram individual BLEU
from nltk.translate.bleu_score import sentence_bleu
reference = [['this', 'is', 'small', 'test']]
candidate = ['this', 'is', 'a', 'test']
score = sentence_bleu(reference, candidate, weights=(1, 0, 0, 0))
print(score)
```

In practice, however, using individual words as the unit of comparison is not optimal. Instead, BLEU computes the same modified precision metric using n-grams. The length which has the "highest correlation with monolingual human judgement" was found to be **four**. This is also the default in many packages that calculate BLUE scores (BLUE-4 metric).

```python
# n-gram individual BLEU
from nltk.translate.bleu_score import sentence_bleu
reference = [['this', 'is', 'a', 'test']]
candidate = ['this', 'is', 'a', 'test']
print('Individual 1-gram: %f' % sentence_bleu(reference, candidate, weights=(1, 0, 0, 0)))
print('Individual 2-gram: %f' % sentence_bleu(reference, candidate, weights=(0, 1, 0, 0)))
print('Individual 3-gram: %f' % sentence_bleu(reference, candidate, weights=(0, 0, 1, 0)))
print('Individual 4-gram: %f' % sentence_bleu(reference, candidate, weights=(0, 0, 0, 1)))
```

Cumulative scores refer to the calculation of individual n-gram scores at all orders from 1 to n and weighting them by calculating the weighted _geometric mean_.


The BLEU score more formally consists of a brevity penalty $\beta$:

$$\beta = \exp(\min(0, 1- \frac{len(R)}{len(C)}))$$

where $len()$ is the length operator as applied in the reference (R) and candidate (C) sentences. 

$$BLEU = \beta \prod_{i=1}^k p_n^{w_n}$$

where $p_n$ is the n-gram precision and this makes BLUE a  _precision_ oriented metric. You can remember it easily if you remember to draw the diagram above and make the following associations

| Metric | Description as it applies to the NMT         |
| ------ | -------------------------------------------- |
| TP     | There are n-grams in C that are in R         |
| FP     | There are n-grams in C that are not in R     |
| FN     | There are missing n-grams in C that are in R |

BLUE is concerned with the first two rows and it shouldn't be a surprise that the n-gram precision is ratio of the counts $\frac{TP}{TP+FP}$.



