# USMLE Prompt Engineering

Reproducible prompt-engineering evaluation of large language model (LLM) performance on USMLE-style multiple-choice questions. This repository contains the code, notebook, HTML export, question-level model results, and performance summaries for the empirical case study described in the accompanying manuscript.

The experiment evaluates the effects of three prompt-design factors:

- Role assignment: none vs. medical expert
- Explanation requirement: answer only vs. answer with a brief explanation
- Number of in-context examples: zero-shot, one-shot, or three-shot

The resulting 2 × 2 × 3 factorial design contains 12 prompt configurations, each evaluated on the same 84-question test set, for a total of 1,008 model evaluations.

This repository accompanies the manuscript:

> **Prompt Engineering for Large Language Models: Foundations, Design, and Evaluation**  
> Christopher Meaney (2026)

---

## Repository Contents

### Input Dataset

**Medical Chat USMLE Correctness Check - Test 1_CM.csv**

The USMLE-style multiple-choice question dataset used in this demonstration was obtained from the Medical Chat Performance Evaluation repository:

> Chat Data LLC. Medical Chat Performance Evaluation Repository.  
> https://github.com/chat-data-llc/medical_chat_performance_evaluation

Original dataset:

https://github.com/chat-data-llc/medical_chat_performance_evaluation/blob/main/test_datasets/USMLE/Medical%20Chat%20USMLE%20Correctness%20Check%20-%20Test%201.csv

The local CSV file included in this repository is a working copy used for the prompt-engineering demonstration and reproducibility analyses presented in the accompanying manuscript.

The notebook uses the multiple-choice question subset of the dataset and partitions the questions into:

- **Reservoir set:** 10 questions used for one-shot and three-shot prompting examples
- **Evaluation set:** 84 questions used for model evaluation

The demonstration questions are therefore separated from the evaluation questions and are not reused as evaluation items.

---

## Analysis Notebook

**example1_prompt_eng_usmle_mcq_ver_final.ipynb**

Primary Jupyter notebook implementing the September 17, 2026 prompt-engineering experiment.

The notebook:

- Loads and preprocesses the USMLE dataset
- Selects the multiple-choice question subset
- Creates the demonstration reservoir and evaluation set
- Constructs the prompt templates
- Evaluates 12 prompt configurations
- Queries the DeepSeek-V4-Flash model through OpenRouter
- Uses explicit provider routing to DeepInfra
- Validates structured JSON responses
- Records response validity, errors, latency, and token usage
- Computes question-level and configuration-level performance measures
- Produces the summary results reported in the manuscript

The notebook is intended to provide a complete, executable record of the experimental workflow.

---

## HTML Notebook Export

**example1_prompt_eng_usmle_mcq_ver_final.html**

Static HTML export of the Jupyter notebook.

The HTML file allows the complete executed notebook, including code and recorded outputs, to be reviewed without launching Jupyter or rerunning the experiment.

---

## Question-Level Results

**model_results.csv**

Question-level results for all 1,008 prompt–question evaluations.

The results file records, where applicable:

- Prompt configuration
- Role-assignment condition
- Explanation condition
- Number of in-context examples
- Question identifier and question text
- Correct answer
- Model identifier
- Generation parameters
- Provider configuration
- Requested and actual provider
- Number of API attempts
- Model answer
- Response status and failure reason
- Latency
- Prompt token count
- Completion token count
- Total token count
- Raw JSON response
- Repaired JSON response, where applicable

The experiment consists of:

- **12 prompt configurations**
- **84 evaluation questions**
- **1,008 total model evaluations**

Not every evaluation necessarily produces a valid model response. API failures are retained in the question-level results so that unsuccessful evaluations are distinguishable from incorrect but valid answers.

---

## Performance Summary

**performance_summary.csv**

Aggregated performance results for each of the 12 prompt configurations.

The summary includes:

- Number of evaluation questions
- Number of valid responses
- Number of invalid responses
- Valid-response rate
- Number of correct responses
- Strict accuracy
- Conditional accuracy
- Retry rate
- JSON-repair rate
- Mean response latency
- Mean prompt token count
- Mean completion token count
- Mean total token count

These summaries correspond to the empirical results reported in the accompanying manuscript.

---

## Experimental Design

Prompt performance was evaluated using a 2 × 2 × 3 factorial design:

| Factor | Levels |
|----------|----------|
| Role assignment | None, Medical Expert |
| Explanation requirement | No, Yes |
| Number of examples | 0-shot, 1-shot, 3-shot |

This produces **12 prompt configurations**, with each configuration evaluated against the same **84-question evaluation set**.

The evaluation design therefore produces:

**12 configurations × 84 questions = 1,008 model evaluations**

Ten additional questions were reserved as a demonstration reservoir for the one-shot and three-shot conditions.

---

## Model and Execution Configuration

The September 17, 2026 experiment used:

- **Model:** DeepSeek V4 Flash 0731
- **Model identifier:** `deepseek/deepseek-v4-flash-0731`
- **Inference interface:** OpenRouter
- **Provider:** DeepInfra
- **Temperature:** 0.0
- **Top-p:** 1.0
- **Maximum output tokens:** 256
- **Reasoning:** Disabled
- **Response format:** JSON object
- **Provider fallback:** Disabled
- **External web search/retrieval:** Disabled

The notebook explicitly specifies these model-generation and provider-routing parameters rather than relying on changing provider defaults.

The experiment was executed on **September 17, 2026**.

---

## Reproducibility

Reproducibility in this experiment is based on explicitly documenting the prompt configuration, evaluation dataset, model identifier, generation parameters, provider routing, execution date, response format, and evaluation procedures.

The repository therefore contains:

- The input question dataset used in the analysis
- The complete experimental notebook
- The executed HTML notebook export
- Question-level model results
- Configuration-level performance summaries

Because hosted LLM services and inference infrastructure can change over time, rerunning the notebook at a later date may not reproduce identical model outputs even when the same prompt, parameters, model identifier, and dataset are used.

The results reported in the accompanying manuscript should therefore be interpreted as an execution-specific empirical evaluation of the documented model, provider, dataset, and experimental configuration.

---

## Evaluation Metrics

The primary performance measure is **strict accuracy**:

$$
\text{Strict Accuracy} = \frac{N_{\text{correct}}}{N}
$$

where $N$ is the total number of evaluation questions.

**Conditional accuracy** is reported as a secondary measure:

$$
\text{Conditional Accuracy} = \frac{N_{\text{correct}}}{N_{\text{valid}}}
$$

where $N_{\text{valid}}$ is the number of valid model responses.

Reporting both measures distinguishes incorrect answers from invalid or unsuccessful model responses.

---

## Scope and Interpretation

The purpose of this experiment is methodological: to demonstrate how prompt components can be evaluated systematically using a reproducible factorial experimental design.

The results should not be interpreted as a universal benchmark of prompt-engineering strategies or as evidence that any particular prompt configuration will perform similarly across other models, providers, datasets, or execution dates.

The experiment is intentionally limited to the documented model–provider–dataset configuration.

---

## Manuscript

The accompanying manuscript is:

**Prompt Engineering for Large Language Models: Foundations, Design, and Evaluation**

The USMLE multiple-choice question example is presented in the manuscript as an empirical case study demonstrating prompt specification, factorial experimental design, programmatic evaluation, response validation, and reproducible reporting.

---

## Citation

Meaney, Christopher. *Prompt Engineering for Large Language Models: Foundations, Design, and Evaluation*. 2026.

Repository:

https://github.com/meaneych/usmle-prompt-engineering
