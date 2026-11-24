# Lab 04 — Fine-Tuning an LLM using LoRA/QLoRA

## 1. Laboratory Session
- **Lab number:** 04
- **Title:** Parameter-Efficient Fine-Tuning (LoRA & QLoRA)
- **Base Model:** Qwen/Qwen2.5-0.5B-Instruct
- **Environment:** Python 3, Kaggle Notebooks, Tesla T4 GPU (14.56 GB VRAM)
- **Libraries:** transformers, peft, trl, bitsandbytes, accelerate

## 2. Objective
The objective of this laboratory activity was to adapt a pre-trained, instruction-tuned Large Language Model to a specific domain (a fictional computer shop, "TechZone"). By using LoRA (Low-Rank Adaptation) and QLoRA (4-bit quantization), this lab demonstrates how to efficiently fine-tune an LLM on a small dataset without the massive memory requirements of full fine-tuning.

## 3. Tasks and Implementation
1. **Environment Setup:** Verified GPU availability (Tesla T4, 14.56 GB memory) using PyTorch.
2. **Dataset Creation:** Created a custom dataset of 30 Question-and-Answer pairs related to a computer shop domain. The data was formatted using the ChatML template (`<|im_start|>user...`).
3. **Model Loading (QLoRA):** Loaded the `Qwen2.5-0.5B-Instruct` model. To save GPU memory, the model was loaded in 4-bit precision using `BitsAndBytesConfig` with NF4 quantization.
4. **LoRA Configuration:** Configured LoRA (r=8, alpha=16) targeting the attention projection layers (`q_proj`, `v_proj`). This reduced the number of trainable parameters to just a fraction of the total model.
5. **Supervised Fine-Tuning (SFT):** Used Hugging Face TRL's `SFTTrainer` to train the model for 10 epochs. Configuration was locked to `fp16=True` to ensure compatibility with the T4 GPU architecture.
6. **Evaluation:** Compared the original base model against the fine-tuned model using domain-specific questions not seen in training.

## 4. Results and Evidence

**Parameter Efficiency:**
- **Total Parameters:** 498,431,872
- **Trainable Parameters:** 4,399,104
- **Trainable Percentage:** 0.8826%

**Model Comparison (Before vs. After):**

**Question:** *What products does TechZone sell?*
- **Original Model:** "I'm sorry for the confusion, but I am not able to provide information on specific companies... I can suggest you check out the official website of TechZone..."
- **Fine-Tuned Model:** "TechZone sells various products such as servers, storage devices, networking equipment, and software solutions."

**Question:** *My laptop is overheating. What should I do?*
- **Original Model:** "When your laptop overheats... Check the temperature... 70 degrees Fahrenheit (21 degrees Celsius)... Open the laptop case and use a fan..."
- **Fine-Tuned Model:** "Check the fans and see if they're working properly."

*(See `/screenshots` folder for the training logs and full model comparison output).*

## 5. Observations
- **Effectiveness of LoRA:** By training only **0.88%** of the model's parameters, we successfully taught the LLM new domain-specific knowledge. This proves that full fine-tuning is unnecessary for simple persona/knowledge adaptation.
- **Conciseness:** The original model gave verbose, "AI assistant" style answers and frequently refused to answer ("I am not able to provide..."). The fine-tuned model adapted perfectly to the TechZone persona, providing direct, concise, and helpful answers.
- **Hallucination Reduction:** The original model hallucinated bizarre technical specs (e.g., claiming an i5 processor has 2GB of RAM). The fine-tuned model stayed grounded in the style of the training data, which was factual and brief.
- **QLoRA Memory Efficiency:** Loading the model in 4-bit allowed us to train a 500-million parameter model easily on a free Kaggle T4 GPU. Without 4-bit quantization, loading the model and optimizer states would likely have caused an Out-Of-Memory (OOM) error.
- **Overfitting:** Because the dataset was only 30 examples, the model likely memorized the exact phrasing. If asked a complex question outside the 30 pairs, it might still struggle.

## 6. Learning Outcomes
- Can configure and apply LoRA/QLoRA to a pre-trained LLM using Hugging Face PEFT.
- Understand the significance of 4-bit quantization (NF4) in reducing VRAM usage.
- Can use `SFTTrainer` to fine-tune a model on custom conversational data.
- Can critically evaluate the before/after performance of a fine-tuned model against a baseline.
