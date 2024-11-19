Multi-lingual Sentiment Analysis

This program integrates **language detection** and **multilingual sentiment analysis** into a single interactive loop, making it suitable for analyzing text in multiple languages with sentiment classification capabilities.

### **1. Loading Pre-trained Sentiment Model**
- The code first loads a pre-trained sentiment analysis model from Hugging Face, specifically **XLM-RoBERTa**, which is a multilingual model fine-tuned for sentiment classification tasks.
  - **Model**: `XLMRobertaForSequenceClassification` is used for sequence classification, i.e., predicting sentiment labels (e.g., positive, neutral, negative).
  - **Tokenizer**: The `XLMRobertaTokenizer` is used to convert the input text into tokens, which can then be processed by the model.

### **2. Loading Pre-trained Language Detection Model**
- The program uses **fastText** for language detection.
  - The **`lid.176.bin`** model is used to detect the language of the input text, which supports 176 languages.
  - The `predict` method from fastText provides the top-1 prediction for the language in which the text is written.

### **3. Defining Sentiment Labels**
- The sentiment labels are predefined as:
  - **Negative**
  - **Neutral**
  - **Positive**
- These labels correspond to the outputs of the sentiment model.

### **4. Input Loop for User Interaction**
- The program enters an input loop where the user is prompted to enter a sentence.
  - The user can enter a sentence in any language.
  - If the user types **"exit"**, the program will terminate.

### **5. Language Detection**
- The input sentence is passed to the **fastText language detection model** to determine the language of the input.
  - The model returns the top predicted language, which is printed to the user.
  - The language prediction is cleaned by removing the **`__label__`** prefix.

### **6. Sentiment Prediction**
- The input sentence is tokenized using the `XLMRobertaTokenizer` and then passed to the **XLM-RoBERTa model** to predict the sentiment.
  - The model outputs a tensor containing logits for each sentiment class.
  - The class with the highest logit is selected using **`torch.argmax`** to determine the sentiment.
  - The sentiment label corresponding to the predicted class is printed.

### **7. Output**
- For each input sentence, the program displays:
  - **Detected Language**: The language in which the input text is written.
  - **Sentiment**: The sentiment classification (positive, neutral, or negative).

---

### **Summary of the Workflow**
1. **Input Sentence**: The user inputs a sentence in any language.
2. **Language Detection**: The sentence's language is detected using the **fastText model**.
3. **Sentiment Prediction**: The sentiment of the sentence is predicted using the **XLM-RoBERTa sentiment model**.
4. **Output**: The detected language and sentiment are displayed.

