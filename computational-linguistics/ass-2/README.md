## HMM-Viterbi based POS tagger

### Intruduction

This assignment implements a bigram Hidden Markov Models (HMM) based parts-of-speech tagger that uses [Viterbi](https://en.wikipedia.org/wiki/Viterbi_algorithm) algorithm for determining the most likely tags for the given sequence of wods. This comes with an extra capability to handle unknown words.

### Tested on

- Python: `3.8.3 [GCC 7.3.0]`
- NLTK: `3.5`

### Project file structure

```
├── utils.py
├── viterbi.py
├── hmm_train.py
├── eval.py
├── data
│   ├── de-eval.tt
│   ├── de-test.t
│   └── de-train.tt
├── results
│   ├── de-tagger_base.tt
│   ├── de-tagger_laplace.tt
│   └── de-tagger_log.tt

```

### Usage

- **Help**: for help
  ```
  python hmm_train.py --help
  ```
- **Training**: following script fits HMM on the given data and predicts POS tags of words given in the test set.

  ```
  python hmm_train.py de-train.tt de-eval.tt de-test.t
  ```

  This will save a file `de-tagger.tt` with test words as first column and predicted POS tags as second column in CoNLL format.

- **Evaluation**: evaluate the tagger using the evaluation script provided.
  ```
  python eval.py de-eval.tt de-tagger.tt
  ```

### Runtime

```
Runtime (training): 208.369 s
Runtime (viterbi): 14.566 ss
```

### Results

The best results below were obtained without using any smoothing techniques or other optional parameters. The HMM-viterbi predicted POS tagged files that produced the below results can be found in `results`

| **POS tag** | **Precision** | **Recall** | **F1-score** |
| :---------: | :-----------: | :--------: | :----------: |
|     DET     |    0.8115     |   0.9761   |    0.8862    |
|    NOUN     |    0.9271     |   0.9201   |    0.9236    |
|    VERB     |    0.9300     |   0.9143   |    0.9221    |
|     ADP     |    0.9095     |   0.9814   |    0.9440    |
|      .      |    0.9531     |   1.0000   |    0.9760    |
|    CONJ     |    0.9578     |   0.8683   |    0.9108    |
|    PRON     |    0.9298     |   0.8364   |    0.8806    |
|     ADV     |    0.8996     |   0.8058   |    0.8501    |
|     ADJ     |    0.8104     |   0.7165   |    0.7605    |
|     NUM     |    0.9858     |   0.7741   |    0.8672    |
|     PRT     |    0.8754     |   0.9153   |    0.8949    |
|      X      |    0.2222     |   0.0909   |    0.1290    |

**Accuracy**: 90.89

Results with laplace smoothing technique and Viterbi algo that uses log probablities:

|         \*\*\*\*         | **Accracy** |
| :----------------------: | :---------: |
|    Laplace smoothing     |    86.28    |
| Viterbi log probablities |    86.86    |
