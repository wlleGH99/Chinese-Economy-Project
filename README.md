# Chinese-Economy-Project
# Separate models
The four separate Final Model files are largely similar, but address different issues. Relevance and Sentiment models are divided since there is more data augmentation and rearrangement when training on sentiment compared to relevance.

# Reading data
Samples are labelled with 1 for relevant and 2 for irrelevant. Sentiment labels have a value of 1, 2, and 3, which correspond to positive, negative, and neutral respectively. Samples are filtered out based on relevance or sentiment, depending on the task. 
Sentiment labels are given for 4 different content types: headline, first paragraph, last paragraph, and full article. The dataframe constructed for sentiment analysis consists of all 4 of these contents.

# Downsampling
There may be an uneven distribution of data depending on some tasks. Samples are randomly dropped from the dataframe (at a number of your choosing) to balance out the dataset. It is also necessary to remove any empty samples that have no viable content to use.

# Changing labels
It is necessary to change the labels so that the first label starts with a 0 to feed into BERT. The code currently changes the labels to 0 for irrelevant and 1 for relevant for relevance analysis. Negative samples are reassigned 0, neutral samples are reassigned 1, and positive samples are reassigned 2. If performing sentiment analysis for Chinese data, the labels can also be changed with negative and neutral samples being 0, and positive samples being 1 to compare positive vs nonpositive samples.

# Data augmentation
The Chinese models are currently based off xlm-roberta. This is a cross-language model that is multilingual. Since there is insufficient data for the Chinese dataset, samples from the English dataset are used in conjunction for training.

# Training data
When doing a hyperparameter grid search, it will be useful to split up the data into a training and testing split. The code currently takes 10% of the dataset for training, and randomly shuffles both sets. There is an equal proportion of labels in both groups.

# Tokenization
Tokens are generated using Autotokenizer from transformers.

# Validation data
If doing a hyperparameter grid search, one can also use validation to assess the model's performance. The current models allocate 10% of the training data for validation.

# Model Specification
Bert-base-uncased is used for training the English models and xlm-roberta is used for the Chinese models. The num_labels paramater should be changed depending on the number of classification outputs. Hyperparameters such as learning rate, batch size, and number of epochs can also be changed.

