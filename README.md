# ErdosReviewSentiment

Using Google review data, we predict the sentiment and star rating given review text. Our model is trained on reivew data from restaurants in the US, roughly ~1.5 million samples. 

Our main model is a recurrent neural network with long short term memory "lstm-main". This model uses a pretrained word embedding layer from the GloVe vector representation of words model. Specifically, the corpus of review text is limited to the 20,000 most common words, and the overlap between those and the GloVe words are assembled to build an embedding matrix. The LSTM is bidirectional and processing reviews with a maximum length of 128 words. 

Two variants of this model were trained: one which predicts sentiment of a review as positive (4,5 star), negative (1,2 star), neutral/mixed (3 star); and another which predicts the star rating of the review text. The sentiment analysis model achieves an accuracy of roughly 98% on the testing set, and the star rating model achieved an accuracy of 94%. 

![cm-lstm-all-states](https://github.com/user-attachments/assets/085b5442-b6b1-446e-90c5-8e291b80c29a)
![cm-lstm-all-states-5star](https://github.com/user-attachments/assets/f9ad0eb0-0600-4354-9e21-430cd48646e1)

Both model performed on-par or better than transformer-based models such BERT or RoBERTa (https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment-latest/tree/main) with a siginifcant reduction in training time and resource requirements. 

Our LSTM model was also trained on restaurant-type specific datasets ("lstm-thai", "lstm-veg") and compared against RoBERTa and BERT on these tasks. The results were consistent with the nationally sampled data. 

Saved models for the LSTMs along with datasets including the predicted probabilities of each model is contained within this repository, along with the files for constructing the datasets ("import-restaurant-ratings", "data-read-state"), and building/training the models ("lstm-main", "bert-main", "roberta-main"). A short summary notebook contains more detailed evaluation metrics of each individual on the given datasets. 
