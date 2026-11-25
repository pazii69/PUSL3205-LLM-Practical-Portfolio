# Final Reflection — PUSL3205 Practical Portfolio

## Overview
Over the course of this module, I have progressed from traditional text classification to building complex, multi-component AI systems. This portfolio demonstrates a practical understanding of how Large Language Models function under the hood, how to adapt them, and how to ground them using external knowledge and tools.

## Skills Gained
- **Traditional NLP & Evaluation:** Can build reproducible ML pipelines, interpret Precision/Recall/F1, and understand the limits of Bag-of-Words models.
- **Transformer Architecture:** Implemented a decoder-only Transformer from scratch, understanding token embeddings, positional embeddings, and masked self-attention.
- **Fine-Tuning (PEFT):** Successfully applied LoRA and QLoRA to a 500M parameter model, drastically reducing memory requirements while achieving domain-specific instruction following.
- **Retrieval-Augmented Generation (RAG):** Built an end-to-end pipeline using ChromaDB and LangChain to dynamically ingest user-uploaded PDFs and ground LLM answers to prevent hallucination.
- **AI Agents:** Implemented the ReAct (Reasoning and Acting) paradigm from scratch in pure Python, allowing an LLM to execute external tools and maintain persistent memory via SQLite.

## Challenges and How I Addressed Them
1. **Environment Dependency Conflicts:** When using free cloud environments (Colab/Kaggle), libraries like `transformers` and `bitsandbytes` frequently conflicted. I learned how to pin specific versions, downgrade incompatible packages, and ultimately bypass broken framework dependencies by writing custom Python execution loops.
2. **GPU Hardware Limitations:** The T4 GPU does not support `bfloat16` math. I learned to force `float16` precision and adjust training arguments to prevent `Out-Of-Memory` (OOM) and kernel errors.
3. **Agent Hallucination:** Small models often fail to output the exact `Action:` format required by Agent parsers. I resolved this by enforcing regex parsing and implementing a `max_steps` loop limit to prevent infinite hallucinations.

## Key Insights
- **Fine-Tuning vs. RAG:** Fine-tuning (Lab 04) is excellent for changing the *style*, *tone*, and *persona* of a model. However, RAG (Lab 05) is vastly superior and cheaper for injecting factual, frequently changing knowledge (like PDFs) because it does not require retraining the model weights.
- **The Importance of Prompt Engineering:** Whether it was asking an LLM to design a product (Lab 02) or forcing it to use a calculator (Lab 06), the structure of the prompt is critical. The ReAct prompt pattern transformed a standard chatbot into an autonomous agent.
- **Base Models are Powerful, but Context is King:** The pre-trained models we used (Qwen, Flan-T5) already possessed incredible linguistic understanding. The challenge was not teaching them English, but teaching them *how to format their English* to interact with our software.

## Limitations of My Work
Because free cloud GPUs (14GB VRAM) were used, I could only train small models (under 2 Billion parameters) for a short duration. The generated text in Lab 03 is slightly incoherent due to the tiny model size and limited training steps. In a real-world setting, scaling up the data and model size would yield much better results. Furthermore, the Agent built in Lab 06 relies on regex parsing; a production system should use native tool-calling APIs (like OpenAI's function calling).
