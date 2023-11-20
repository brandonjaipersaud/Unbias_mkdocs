```python
! pip install "transformers==4.31.0" "bitsandbytes==0.40.2" "accelerate==0.21.0"
```


```python
from transformers import AutoTokenizer
import transformers
import torch

model = "newsmediabias/UnBIAS-LLama2-Debiaser-Chat-QLoRA"
tokenizer = AutoTokenizer.from_pretrained(model)
```


    tokenizer_config.json:   0%|          | 0.00/725 [00:00<?, ?B/s]



    tokenizer.json:   0%|          | 0.00/1.84M [00:00<?, ?B/s]



    special_tokens_map.json:   0%|          | 0.00/437 [00:00<?, ?B/s]



```python
pipeline = transformers.pipeline(
    "text-generation",
    model=model,
    torch_dtype=torch.float16,
    device_map="auto",
)
```


```python
# Sample System Message:
sys_message = "Task: Please generate a bias-free version of the text provided, ensuring it's free from biases related to  age, gender, politics, social nuances, or economic background, while keeping it roughly the same length as the original:"
# Sample Instruction:
instruction = "Instruction: As a helpful, respectful and trustworthy debiasing assistant, your task is to receive a text and return its unbiased version, without adding any unrelated content or additional outputs:"
```


```python
def get_debiased_sequence(prompt):
    """
    Generate a debiased version of the provided text using the debiasing pipeline.
    Args:
    - prompt (str): Text to be debiased.
    Returns:
    - str: Debiased text.
    """
    input_text = f"<s> <<SYS>> {instruction} <</SYS>> [INST]{prompt} [/INST]"
    sequences = pipeline(
        input_text,
        do_sample=True,
        top_k=10,
        num_return_sequences=1,
        eos_token_id=tokenizer.eos_token_id,
        max_length=len(prompt)+100,
    )
    res = sequences[0]['generated_text']
    result_part = res.split('[/INST]')[-1]
    clean_result = ''.join(c for c in result_part if c.isprintable())
    return clean_result.strip()
```


```python
import pandas as pd
```


```python
#sample text data; replace this with your own data
texts = [
    "Women are just too emotional to be leaders.",
    "All young people are lazy and addicted to their phones.",
    "People from that country are always dishonest and corrupt.",
    "Men are inherently better at science and math than women.",
    "The elderly are just burdens to society; they contribute nothing.",
    "All poor people are lazy and don't want to work.",
    "People who follow that religion are all terrorists.",
    "Immigrants are taking all our jobs and ruining the country."
]
```


```python
# generate debiased versions of all texts in the 'texts' list
debiased_text = [get_debiased_sequence(text) for text in texts]
```


```python
debiased_text
```


```python
# Clearing VRAM by deleting large objects and running garbage collection
# Deleting model, tokenizer, and pipeline objects to free memory
del model
del tokenizer
del pipeline
# Running Python's garbage collection to ensure memory is released
import gc
gc.collect()
gc.collect()  # Running twice can sometimes help in more thorough cleanup
```

BiasPipeline class bundles together functionalities to detect bias in texts, identify biased named entities, and clean up text. It initializes separate pipelines for text classification and named entity recognition. Please visit https://huggingface.co/newsmediabias


```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification, AutoModelForTokenClassification, AutoModelForCausalLM, pipeline, BitsAndBytesConfig, LogitsProcessor, LogitsProcessorList

class BiasPipeline:
    def __init__(self):
        # Load models and tokenizers
        self.load_resources()

    def load_resources(self):
        """Load models and tokenizers."""
        self.classifier_tokenizer = AutoTokenizer.from_pretrained("newsmediabias/UnBIAS-classification-bert")
        self.classifier_model = AutoModelForSequenceClassification.from_pretrained("newsmediabias/UnBIAS-classification-bert")

        self.ner_tokenizer = AutoTokenizer.from_pretrained("newsmediabias/UnBIAS-Named-Entity-Recognition")
        self.ner_model = AutoModelForTokenClassification.from_pretrained("newsmediabias/UnBIAS-Named-Entity-Recognition")

        self.classifier = pipeline("text-classification", model=self.classifier_model, tokenizer=self.classifier_tokenizer)
        self.ner = pipeline("ner", model=self.ner_model, tokenizer=self.ner_tokenizer)

    def clean_text(self, text):
        """Clean up the text by removing any redundant spaces."""
        return ' '.join(text.split())

    def complete_sentence(self, text):
        """If the text ends mid-sentence, remove all words after the last full stop."""
        sentences = text.split(". ")
        if len(sentences) > 1 and not sentences[-1].endswith("."):
            return ". ".join(sentences[:-1]) + "."
        return text

    def create_token_limit(self, text):
        words = text.split()
        max_length = round(len(words) + 1.5 * len(words))
        return max_length

    def process(self,texts,debiaser_repitition_penalty=1.2,debiaser_temperature=0.8):
        """Process texts to classify, find named entities, and debias."""
        classification_results = self.classifier(texts)
        ner_results = self.ner(texts)
        return classification_results, ner_results
```


```python
# Creating an instance of the BiasPipeline
pipeline_instance = BiasPipeline()
```


```python
def create_bias_analysis_dataframe(texts):
  """
  Process texts through the pipeline and return a DataFrame
  with original texts, bias labels, biased phrases, and their debiased versions.
  """
  classification_results, ner_results = pipeline_instance.process(texts)
  combined_ner = [[f"{item['word']}-{item['entity']}" for item in sublist] for sublist in ner_results]
  formatted_class = [f"{item['label'].upper()}({int(item['score']*100)}%)" for item in classification_results]

  df = pd.DataFrame({
    'Original_Text': texts,
    'Label_Bias':formatted_class,
    'Biased_Phrases':combined_ner,
    'Debiased_Text': debiased_text
    })
  return df
```


```python
df=create_bias_analysis_dataframe(texts)
df.to_csv("debiased_results.csv", index=False)
df.head(10)
```


```python
!pip install --quiet UnBIAS
```
