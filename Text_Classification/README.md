
### Text Classification

This project uses a RoBERTa pre-trained model (`cardiffnlp/twitter-roberta-base-sentiment-latest`) from Hugging Face to classify the text input as positive, neutral, or negative. This particular model was optimized for sentiment analysis of tweets and returns predicted labels with a confidence score for each input text. Responses are then further tuned based on confidence thresholds to refine the classification of sentiments.

### Requirements
- **Python 3.x**
- **Packages**
	+ `transformers`
	+ `matplotlib`
  + `re`
  + `numpy`

Use the following code to install the necessary libraries:

```bash
pip install transformers matplotlib
```

### Code Review
- **Sentiment Analysis**: This class in the `transformers` library gives a pipeline for classifying text provided by users. Predictions give a confidence score and the sentiment is refined to assure reliability through thresholds set on confidence levels.
- **Label Adjustment**: Predictions are categorized over confidence score:
  - **Positive**: Confidence > 0.7
  - **Neutral**: 0.4 < Confidence ≤ 0.7
  - **Negative**: Confidence ≤ 0.4
-**Visualization**: A bar chart is created to show the distribution of the sentiment classification where color codes stand for Positive (green), Neutral (yellow), and Negative (red).
 
Output:
Run to view the sentiment for each text. It will print out in the console, along with the sentiment label prediction and confidence. The final chart plots a bar of the distribution of all input sentiments.

### Example Output
- **Text**: "The product quality exceeded my expectations!"
  - **Predicted Sentiment**: Positive
  - **Confidence**: 0.92

