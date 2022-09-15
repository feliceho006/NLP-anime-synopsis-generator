# NLP Anime Synopsis Generator

### 1 Introduction
Anime, typically animated works made in Japan, has always been a popular source of entertainment over the years. However, the quality of anime storylines has been declining in recent times, and through this project, we hope to be able to draw on the storylines of popular anime to generate storylines of better quality, or even inspire creativity in future storylines. Our project features models which are able to generate story synopses which could potentially stimulate more creativity in scriptwriters.

### 2 Approach
**2.1 Dataset** <br>

The dataset we decided to proceed with is from https://www.kaggle.com/marlesson/myanimelist-dataset-animes-profiles-reviews . In this dataset, there are **16214** unique values in the **animes.csv** file. However, after taking a look at the data, we found that there are repeated synopsis, for example animes with many seasons will reuse the synopsis, there are entries with no synopsis, and there are synopsis of very short length. Hence in our text generation, we remove those entries.

**2.2 LSTM Model** <br>

Since we will be attempting to generate text, we decide to use RNN models, specifically LSTM to generate the text using the many-to-many architecture. In a single LSTM cell, it contains a forget gate, input gate and output gate. The weights in the forget gate and input gate will decide how to extract features from the input data so as to determine which time-steps are important, which are not important, and how to encode information from the current time-step into the cell state.

Upon further research, we found that there are mainly 2 kinds of LSTM generation models. 
1. Character level LSTM generation models
2. Word level LSTM generation models

We decided to try both and compare their performance. In both models, the architecture used is very simple.

**2.2.1 Character Level Model** <br>
In character level LSTM generation, we will need to create a dictionary of all the unique characters. Before pre-processing there are many emojis, japanese characters and escape sequences, hence in the dictionary of unique characters we remove those and in the synopsis, we replace those characters with “” to remove them. After generating a dictionary of characters, where we can look up the indices of the characters with the characters as the key, we create an inverse dictionary where we can look up the characters with the indices in order for text generation later on.
<br>
<br>
Since the sentences are of different lengths and LSTM takes in an input of constant length, we splice the sentences into sub-sentences of 150 characters, where each character is encoded into their indices. This will ensure that the model takes in an input of constant sequence length of 150. We then split this data into batch sizes of 256 hence our input now has a shape of [256,150,65] where there are 65 unique characters. This data is first passed through the embedding layer, then the 2 LSTM layer and finally a Dense layer which will output a probability matrix of the next character in the sequence.
<br>
<br>
In order to calculate loss, we compute the CrossEntrophyLoss of this output probability matrix with the actual next character matrix. This loss is then fed back to the model in order to update the weights. This is done for 20 epochs. 
<br>
<br>
During prediction, we switch the model to eval mode and pass a randomly selected synopsis from the dataset as inputs. We use the output probability matrix to pick the most probable next character of that input sentence. This generated text is then printed at the end of iterating through 500 rounds of prediction.

**2.2.2 Word Level Model** <br>
In word level LSTM generation, we will need to create a dictionary of all the unique words instead of character and the rest of the process is the same as that of the character level prediction.

### Usage
```
Code description:

1. Using the .ipynb, change the PATH of all dataset
2. Run all and watch the text be generated

```

**2.2 GPT-2 Model** <br>

We also tried finetuning a model, GPT-2, to see what more sophisticated text generation would be able to do. We used a Python package, [gpt-2-simple](https://github.com/minimaxir/gpt-2-simple), that provides finetuning and generation functions. The Google Colab notebook with the results are [here](https://colab.research.google.com/drive/16v66nXQTdElfs6bYzUbjKGS2WacTXqA8?usp=sharing). 





