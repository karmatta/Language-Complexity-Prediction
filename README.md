# Language-Complexity-Prediction
This repo has code that builds language embeddings of Hindi and Telugu script and a Language Complexity Prediction model for English, Hindi and Telugu Script

### Step 1: Building a custom word embedding for a language:

In the case of English, we have open-source pretrained word embeddings available such as word2vec and GloVe that is trained on 6B words corpora from wikipedia and other sources. Since the word embedding for English is already available, I will be using a pre-trained word embedding (GloVe) for embedding English words.

In the case of Hindi and Telugu, there are no pre-trained, open-source embeddings available so I will be building these embeddings from the data that is provided.

To train the embedding, I am using the Continuous Bag Of Words algorithm which is defined as follows:

For example, lets take {"The", "cat", ’over", "the’, "puddle"} as a context and from these words, be able to predict or generate thecenter word "jumped". This type of model we call a Continuous Bag of Words (CBOW) Model.

##### CBOW Algorithm:

    Build the corpus vocabulary
    Build a CBOW (context, target) generator
    Build the CBOW model architecture
    Train the Model
    Get Word Embeddings 

![](https://github.com/karmatta/Language-Complexity-Prediction/blob/master/Misc_files/Screenshot%20from%202019-05-16%2016-50-58.png)

The corpus is constructed using the stories in the dataset provided for Telugu and Hindi.

### Step 2: Train a Language Complexity Classifier

A NLP classifier is built and trained and the architecture I have used is a LSTM and GRU stack 

![](https://github.com/karmatta/Language-Complexity-Prediction/blob/master/Misc_files/LSTM_Dimensions.png)

##### Model Architecture:

    Use the trained language embedding to extract a 300 dim feature vector for each word
    Pass these feature vectors to the LSTM + GRU
    Dense layer 
    Softmax layer with crossentropy loss function

### Data

The data set consists of original and translated stories in English, Telugu and Hindi languages.

The data set consists of about 3697 stories out of which 3 stories do hot have any content

Basic propressing of the data consists of removing stray English characters in Hindi and Telugu corpora, in addition to remove some special characters

#### Train test split for cross validation of model

| Set  | Train  | Test |
| :------------ |:---------------:| -----:|
| English     | 6876 | 303 |
|Hindi      | 795         |   234 |
| Telugu | 2133     |    570 |

#### DV Distribution for English

| Level  | Train Count  | Train % | Test Count  | Test % |
| :------------ |:---------------:| -----:|:---------------:| -----:|
| L1     | 972| 42%  |40|40%|
|L2      | 796         |   35% |40|40%|
| L3 | 384     |    17% | 15 | 15%|
| L4| 140     |    6% | 6|6%|

#### DV Distribution for Hindi

| Level  | Train Count  | Train % |Test Count  | Test % |
| :------------ |:---------------:| -----:|:---------------:| -----:|
| L1     | 302| 42%  | 84| 44%|
|L2      | 234         |   33% | 66|35%|
| L3 | 107     |    15% | 27| 14%|
| L4| 68    |    10% |13| 7%|

#### DV Distribution for Telugu

| Level  | Train Count  | Train % | Test Count  | Test % |
| :------------ |:---------------:| -----:|:---------------:| -----:|
| L1     | 86| 42%  | 37| 47%|
|L2      | 89         |   33% | 18|23%|
| L3 | 61     |    15% | 14|18%|
| L4| 29    |    10% | 9| 12%|

#### Model  training

##### English model:
![](https://github.com/karmatta/Language-Complexity-Prediction/blob/master/Misc_files/English_lr.png)

##### Hindi model:
![](https://github.com/karmatta/Language-Complexity-Prediction/blob/master/Misc_files/Hindi_lr.png)

##### Telugu model:
![](https://github.com/karmatta/Language-Complexity-Prediction/blob/master/Misc_files/Telugu_lr.png)

#### Test Performance

English Model Accuracy: 51%
Hindi Model Accuracy: 53%
Telugu Model Accuracy: 44%

The low accuracies can be further improved by hyperparameter tuning such as increasing the dropout values and a larger test size
