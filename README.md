# USMLE Prompt Engineering

Reproducible prompt-engineering evaluation of LLM performance on USMLE multiple-choice questions. This repository implements a factorial experiment comparing role assignment, explanation requirements, and zero-, one-, and few-shot prompting using the DeepSeek-V4-Flash model via OpenRouter.

This repository accompanies the manuscript:

> **Prompt Engineering for Large Language Models: Foundations, Design, and Evaluation**  
> Christopher Meaney (2026)

---

## Repository Contents

## Input Dataset

**Medical Chat USMLE Correctness Check - Test 1_CM.csv**

The USMLE-style multiple-choice question dataset used in this demonstration was obtained from the Medical Chat Performance Evaluation repository:

> Chat Data LLC. Medical Chat Performance Evaluation Repository.  
> https://github.com/chat-data-llc/medical_chat_performance_evaluation

Original dataset:

https://github.com/chat-data-llc/medical_chat_performance_evaluation/blob/main/test_datasets/USMLE/Medical%20Chat%20USMLE%20Correctness%20Check%20-%20Test%201.csv

The local CSV file included in this repository is a working copy used for the prompt-engineering demonstration and reproducibility analyses presented in the accompanying manuscript.

The notebook uses the multiple-choice question (MCQ) subset of the dataset and partitions the questions into:

- Reservoir set (10 questions) used for one-shot and few-shot prompting examples
- Test set (84 questions) used for model evaluation

This separation ensures that prompt examples are not reused in the evaluation set.

---

### Analysis Notebook

**example1_prompt_eng_usmle_mcq_ver3.ipynb**

Primary Jupyter notebook implementing the prompt-engineering experiment. The notebook:

- Loads and preprocesses the USMLE dataset
- Creates prompt templates
- Evaluates 12 prompt configurations
- Queries DeepSeek-V4-Flash through OpenRouter
- Validates JSON outputs
- Computes accuracy, latency, and token-usage metrics
- Produces summary tables used in the manuscript

---

### HTML Report

**example1_prompt_eng_usmle_mcq_ver3.html**

Static HTML export of the notebook for readers who wish to review the complete analysis without running Jupyter.

---

### Question-Level Results

**model_results.csv**

Contains model outputs for all prompt–question combinations, including:

- Prompt configuration
- Question identifier
- Correct answer
- Model prediction
- Response validity
- Latency
- Token usage
- Raw JSON response

The experiment evaluates:

- 12 prompt configurations
- 84 USMLE questions

for a total of 1,008 model evaluations.

---

### Performance Summary

**performance_summary.csv**

Aggregated results for each prompt configuration, including:

- Conditional accuracy
- Number of valid responses
- Average latency
- Prompt tokens
- Completion tokens
- Total token usage

These summaries correspond to the results reported in the manuscript.

---

## Experimental Design

Prompt performance was evaluated using a factorial design involving:

| Factor | Levels |
|----------|----------|
| Role assignment | None, Medical Expert |
| Explanation requirement | No, Yes |
| Number of examples | 0-shot, 1-shot, 3-shot |

This produces a total of 12 prompt configurations.

---

## Reproducibility

The notebook was executed using:

- Python 3.14
- pandas 3.0.1
- numpy
- OpenAI Python SDK
- OpenRouter API

Model outputs were generated using:

- DeepSeek-V4-Flash
- Temperature = 0

The repository contains all code, prompts, outputs, and summary results required to reproduce the USMLE prompt-engineering case study.
