# Turkish MMLU Fine-Tuned T5-Small Model

This project focuses on fine-tuning the **T5-Small** model using the **Turkish MMLU dataset**, which consists of 293,468 questions covering academic and professional exams such as KPSS, TUS, and many others in Turkey. The goal is to train the model to answer questions accurately based on this dataset.

## Model Overview

The model used in this project is **T5-Small**, a text-to-text transformer model, fine-tuned on Turkish academic and professional exam questions. The model takes a question as input and generates the correct answer in Turkish.

- **Model**: [T5-Small](https://huggingface.co/t5-small)
- **Dataset**: [Turkish MMLU](https://doi.org/10.5281/zenodo.13378019) (293,468 questions) 

- **Objective**: Fine-tune T5-Small to correctly answer questions from various Turkish exams (KPSS, TUS, etc.).

## Project Details

This project follows the following steps:

1. **Data Preparation**: 
   - The dataset is cleaned and filtered, focusing on `soru` (question) and `dogru_cevap` (correct answer).
   - The dataset contains questions and multiple-choice options. We map the correct answer from the options to the correct response.

2. **Fine-Tuning**:
   - The **T5-Small** model is fine-tuned using the prepared dataset.
   - The model is trained to take questions as input (formatted as "Soru: ...") and generate the correct answer (formatted as "Cevap: ...").

3. **Evaluation**:
   - The model's performance is evaluated based on its ability to answer questions accurately.
   - The training loss after 3 epochs was **0.0749**, indicating good model performance.

## Dataset

The Turkish MMLU dataset is one of the largest and most comprehensive datasets for academic and professional exams in Turkey. The dataset includes:

- 293,468 questions.
- Covers multiple exams (KPSS, TUS, and others).
- Includes detailed explanations and correct answers.

### Example

Here is an example of how the input and output are structured:

- **Input**: `Soru: Türkiye'nin başkenti neresidir?`
- **Output**: `Cevap: Ankara`

## How to Use

To use the fine-tuned model, you can load it via the Hugging Face model hub:

```python
from transformers import T5Tokenizer, T5ForConditionalGeneration

# Load the fine-tuned model
tokenizer = T5Tokenizer.from_pretrained("cuneytkaya/fine-tuned-t5-small-turkish-mmlu")
model = T5ForConditionalGeneration.from_pretrained("cuneytkaya/fine-tuned-t5-small-turkish-mmlu")

# Test the model with a question
question = "Türkiye'nin başkenti neresidir?"
inputs = tokenizer(f"Soru: {question}", return_tensors="pt")
outputs = model.generate(**inputs)

# Decode the output
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
