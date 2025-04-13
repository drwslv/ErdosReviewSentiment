# ErdosReviewSentiment

Using Google review data, we predict the sentiment and star rating given review text. Our model is trained on reivew data from restaurants in the US, roughly ~1.5 million samples. 

Our main model is a recurrent neural network with long short term memory "lstm-main". This model uses a pretrained word embedding layer from the GloVe vector representation of words model. Specifically, the corpus of review text is limited to the 20,000 most common words, and the overlap between those and the GloVe words are assembled to build an embedding matrix. The LSTM is bidirectional and processing reviews with a maximum length of 128 words. 

Two variants of this model were trained: one which predicts sentiment of a review as positive (4,5 star), negative (1,2 star), neutral/mixed (3 star); and another which predicts the star rating of the review text. The sentiment analysis model achieves an accuracy of roughly 98% on the testing set, and the star rating model achieved an accuracy of 94%. 

Both model performed on-par or better than transformer-based models such BERT or RoBERTa (https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment-latest/tree/main) with a siginifcant reduction in training time and resource requirements. 
