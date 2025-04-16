# ErdosReviewSentiment
Summary: Using Google review data, we predict the sentiment and star rating based on review text. Our model is trained on review data from restaurants in the US, roughly ~2 million samples.

Our main model is a recurrent neural network with long short term memory. This model uses a pre-trained word embedding layer from the GloVe vector representation of words model. Specifically, the corpus of review text is limited to the 20,000 most common words, and the overlap between those and the GloVe words are assembled to build an embedding matrix. The LSTM is bidirectional and can process reviews with a maximum length of 128 words (reviews past that length are truncated).
Two variants were trained on this data set:
- A model for predicting sentiment of a review as positive (4, 5 star), negative (1, 2 star), neutral/mixed (3 star)
- A model for predicting the star rating of the review text.

The sentiment analysis model achieves an accuracy of over 98% (F1 0.98132) on the testing set, and the star rating model achieves an accuracy of over 94% (F1 0.94016). Confusion matrices are available in the /confusion-mats subfolder.
Both LSTM models demonstrated comparable or superior performance to transformer-based models such as BERT or ROBERTa, with faster training and prediction times, and a smaller storage footprint.

Using these files:
- "import-restaurant-ratings" extracts the relevent reviews (restaurants) from the Google Local .json files, to create regionally aggregated csv files storing only restaurant reviews
- "data-read-state" downsamples (at 1%) these regional files into our main dataset. A train/val/test split is created and saved as "all-states-train", "all-states-val", "all-states-test" datasets found in the /data subfolder. 
- "lstm-main" contains all code needed to build and train our LSTM model from review data. Checkpoints for these trained models can be found in the /models subfolder, and the saved embedding matrices and vocabulary dictionaries can be found in /embedding-mats.
- Comparison models for RoBERTa and BERT-base can be built using "roberta-main" and "bert-main". Saved checkpoints for these models are too large to be saved on GitHub, but can be produced upon request. 
- Additional datasets (e.g., thai restaurants, vegetarian restaurants) are found in the /data subfolder as well
