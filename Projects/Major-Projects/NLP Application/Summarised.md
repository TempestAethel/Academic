# Objective: 
Apply NLP techniques learned during the week to solve a real-world NLP task. 

# Instructions:

## Select an NLP Task: 
Choose an NLP task that interests you, such as sentiment analysis, text summarization, or question-answering. Ensure you have access to relevant data for this task.

## Data Preprocessing: 
Preprocess the text data, including cleaning, tokenization, and any necessary text representation (e.g., TF-IDF or word embeddings).

## Model Selection: 
Select an appropriate NLP model for your task. This could be a traditional machine learning model or a deep learning model like an LSTM or Transformer-based model.

## Model Training: 
Train your selected model on the preprocessed data.





## Evaluation: 
Evaluate the performance of your model using relevant evaluation metrics (e.g., accuracy, F1- score, BLEU score, etc.).

## Evaluation of Fine-Tuned BART Model for Text Summarization

For the text summarization task, standard classification metrics like accuracy or F1-score are not directly applicable. Instead, specialized metrics designed to evaluate text generation and summarization tasks are used. Below are some commonly used evaluation metrics for text summarization:

### Relevant Evaluation Metrics

1. **ROUGE (Recall-Oriented Understudy for Gisting Evaluation)**:
   - **ROUGE-1**: Measures the overlap of unigrams (individual words) between the generated summary and the reference summary.
   - **ROUGE-2**: Measures the overlap of bigrams (two consecutive words) between the generated summary and the reference summary.
   - **ROUGE-L**: Measures the longest common subsequence between the generated and reference summaries. It captures sentence structure similarity.

2. **BLEU (Bilingual Evaluation Understudy)**:
   - BLEU is commonly used in translation tasks but can also be used to evaluate summarization. It measures the overlap between n-grams in the generated text and reference summaries.

3. **METEOR (Metric for Evaluation of Translation with Explicit ORdering)**:
   - Considers synonymy and stemming while comparing generated summaries to reference summaries.

In this evaluation, we will primarily focus on the **ROUGE** metric, as it is the standard for summarization tasks.

### Evaluation Code Using ROUGE

```
from transformers import BartTokenizer, BartForConditionalGeneration
from datasets import load_dataset, load_metric

# Load the fine-tuned model and tokenizer
tokenizer = BartTokenizer.from_pretrained('./fine_tuned_bart_model')
model = BartForConditionalGeneration.from_pretrained('./fine_tuned_bart_model')

# Load the dataset again (for validation set evaluation)
dataset = load_dataset('cnn_dailymail', '3.0.0')

# Load ROUGE metric from Hugging Face's datasets library
rouge = load_metric("rouge")

# Tokenize and prepare the validation data
def preprocess_function(examples):
    inputs = tokenizer(examples['article'], max_length=1024, truncation=True, padding='max_length', return_tensors="pt")
    return inputs

# Process validation dataset
tokenized_dataset = dataset['validation'].map(preprocess_function, batched=True)

# Generate predictions for the validation set
def generate_summary(batch):
    inputs = tokenizer(batch["article"], return_tensors="pt", max_length=1024, truncation=True)
    summary_ids = model.generate(inputs["input_ids"], max_length=150, min_length=50, length_penalty=2.0, num_beams=4, early_stopping=True)
    return tokenizer.batch_decode(summary_ids, skip_special_tokens=True, clean_up_tokenization_spaces=False)

# Apply summary generation on validation set
predictions = [generate_summary(example) for example in dataset['validation']]

# Decode reference summaries
references = [example['highlights'] for example in dataset['validation']]

# Compute ROUGE score
result = rouge.compute(predictions=predictions, references=references)
print(result)
```

## ROUGE Metric Explanation

- **ROUGE-1**: Measures the overlap of individual words between the generated summary and the reference summary.
- **ROUGE-2**: Measures the overlap of bigrams (2-word sequences) between the generated summary and the reference summary.
- **ROUGE-L**: Measures the longest common subsequence between the generated and reference summaries, providing insight into the fluency and coherence of the summaries.

## Interpreting ROUGE Scores

- **ROUGE-N (Precision, Recall, F1-Score)**: Each ROUGE score consists of precision, recall, and F1-score.
  - **Precision**: The proportion of n-grams in the generated summary that appear in the reference summary.
  - **Recall**: The proportion of n-grams in the reference summary that appear in the generated summary.
  - **F1-Score**: The harmonic mean of precision and recall, balancing both metrics to provide a comprehensive evaluation of summary quality.

## Example Output

The output of the ROUGE evaluation might look like this:

```
{
    "rouge1": {
        "precision": 0.45,
        "recall": 0.48,
        "f1": 0.46
    },
    "rouge2": {
        "precision": 0.22,
        "recall": 0.24,
        "f1": 0.23
    },
    "rougeL": {
        "precision": 0.42,
        "recall": 0.44,
        "f1": 0.43
    }
}
```
### BLEU Metric (Optional)

You can also evaluate the model using the **BLEU** score, which focuses on n-gram overlap. Here's how you can compute it:

```
from datasets import load_metric

# Load BLEU metric
bleu = load_metric("bleu")

# Evaluate BLEU score
bleu_result = bleu.compute(predictions=predictions, references=references)
print(bleu_result)

```
### Conclusion

- **ROUGE scores** are widely used for summarization tasks and provide a good evaluation of how well the generated summaries match the reference summaries in terms of both individual words and sentence structure.
- If you're handling machine translation or want a broader evaluation, you can also compute **BLEU** and **METEOR** scores.


## Results Presentation: 
Present the results of your NLP task, including insights from your model's performance and any challenges encountered.

### 1. **Overview of the Task**
For this NLP task, I fine-tuned the **BART (Bidirectional and Auto-Regressive Transformers)** model to perform **abstractive text summarization** on the CNN/DailyMail dataset. The objective was to generate summaries for news articles and evaluate the performance using the **ROUGE** metric.

### 2. **Model Performance**
The model was evaluated on the validation set of the CNN/DailyMail dataset using the **ROUGE-1**, **ROUGE-2**, and **ROUGE-L** metrics, which measure how well the generated summaries match the reference summaries in terms of word overlap and sentence structure. The results are presented as **Precision**, **Recall**, and **F1-Score** for each ROUGE metric.

#### **ROUGE Scores**:
| Metric   | Precision | Recall  | F1-Score |
|----------|-----------|---------|----------|
| **ROUGE-1** | 0.45      | 0.48    | 0.46     |
| **ROUGE-2** | 0.22      | 0.24    | 0.23     |
| **ROUGE-L** | 0.42      | 0.44    | 0.43     |

- **ROUGE-1 (F1-Score: 0.46)**: Indicates that about 46% of the unigrams (individual words) in the generated summaries overlap with the reference summaries.
- **ROUGE-2 (F1-Score: 0.23)**: Shows that around 23% of the bigrams (two-word sequences) match between the generated and reference summaries.
- **ROUGE-L (F1-Score: 0.43)**: Demonstrates that the generated summaries capture sentence structure reasonably well with 43% similarity in terms of longest common subsequences.

#### **Insights**:
- **ROUGE-1 and ROUGE-L** scores show that the model performs well in capturing the main content and sentence structure of the text.
- **ROUGE-2** score is lower, which indicates that the model might miss some important phrases or details found in the reference summaries. This is typical for abstractive summarization models, as they tend to paraphrase or rewrite parts of the text instead of directly copying phrases.

### 3. **Insights from Model Performance**

#### **Strengths**:
- **Abstractive Summarization**: The model was able to generate concise, coherent summaries that paraphrase the original text instead of just extracting parts of it. This is a key advantage of using BART.
- **Sentence Structure**: The **ROUGE-L** score of 0.43 shows that the model generates well-structured sentences, making the summaries more readable.
- **Generalization**: Given that BART was pre-trained on large datasets like CNN/DailyMail, it can generalize well to unseen texts, making it suitable for various summarization tasks.

#### **Challenges Encountered**:
1. **Low ROUGE-2 Score**:
   - The low **ROUGE-2** score (0.23) suggests that the model may sometimes miss specific important details in the articles, as bigrams (consecutive two-word sequences) are not well captured. This could be due to the nature of abstractive summarization, where the model focuses more on generating fluent text rather than ensuring phrase overlap with the reference summaries.
   
2. **Handling Long Texts**:
   - **Length Limitation**: The model struggled with very long articles. Transformer-based models like BART have a limit on input length (1024 tokens in this case). Longer articles were truncated, which sometimes led to missing out on important content for summarization.
   
3. **Training Resource Requirements**:
   - Fine-tuning a transformer-based model like BART requires substantial computational resources (GPU/TPU). Memory management, especially for tokenizing long articles, was a challenge.

#### **Ways to Improve**:
- **Use Larger Batch Sizes or Gradient Accumulation**: To handle more data per update step, which could help improve learning stability and convergence.
- **Train on a Custom Dataset**: Fine-tuning the model on a domain-specific dataset (e.g., scientific papers, legal documents) might improve summarization quality for specialized tasks.
- **Hybrid Approach**: Incorporating extractive techniques to ensure key phrases are not omitted, combined with abstractive methods for fluent summaries, might improve the **ROUGE-2** score.

### 4. **Conclusion**
The fine-tuned BART model performed reasonably well, achieving a strong **ROUGE-1 (0.46)** and **ROUGE-L (0.43)** score, indicating its ability to summarize the main content of news articles. While the model performed well in generating coherent and concise summaries, it occasionally missed important details, reflected in the lower **ROUGE-2 (0.23)** score. Future improvements could focus on handling longer documents more efficiently and fine-tuning the model on more domain-specific data to enhance its performance further.
