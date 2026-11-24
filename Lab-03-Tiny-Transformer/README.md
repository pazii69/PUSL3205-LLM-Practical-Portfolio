# Lab 03 — Developing a Tiny Transformer Language Model

## 1. Laboratory Session
- **Lab number:** 03
- **Title:** Developing a Tiny Transformer Language Model
- **Dataset:** roneneldan/TinyStories (Hugging Face, 5,000 story subset)
- **Environment:** Python 3, PyTorch, Hugging Face Datasets, Google Colab (T4 GPU)

## 2. Objective
The objective of this laboratory activity was to implement a decoder-only Transformer architecture from scratch and train it for next-token prediction. By building a "Tiny Transformer", this lab demonstrates the core mechanisms of Large Language Models (like self-attention and embeddings) and evaluates the model's ability to generate text using perplexity and sample generation.

## 3. Tasks and Implementation
1. **Data Loading:** Loaded the TinyStories dataset from Hugging Face. To keep training times reasonable, a subset of 5,000 stories was selected.
2. **Preprocessing:** Implemented a character-level tokenizer. Converted all text to lowercase and created a vocabulary of the 90 unique characters found in the dataset. Created `encode` and `decode` functions to translate between text and numbers.
3. **Preparing Training Data:** Built a PyTorch DataLoader to generate input/target batches (context window = 128 characters, batch size = 32) for next-token prediction.
4. **Model Architecture:** Built a `TinyTransformer` class using PyTorch. This included:
   - Token Embeddings (turning numbers into vectors) and Positional Embeddings (giving the model a sense of word order).
   - A Transformer Encoder Layer with Masked Multi-Head Self-Attention (4 heads) to prevent the model from looking into the future.
   - A Feed-Forward Network and Layer Normalization.
   - A linear output layer to predict the next character.
5. **Training:** Initialized the model with 2 layers and trained for 1,000 steps using the AdamW optimizer and Cross-Entropy loss.
6. **Evaluation & Generation:** Plotted the training loss curve and used a text generation loop to sample text starting with the prompt "Once upon a time".

## 4. Results and Evidence
- **Vocabulary Size:** 90 unique characters.
- **Model Size:** 582,234 trainable parameters.
- **Training Loss:** Dropped from 4.66 (Step 0) to **1.95** (Step 800). The loss curve shows a clear, healthy downward trend, indicating the model successfully learned the patterns in the data.
- **Generated Text:** 
  > *"Once upon a timed here was hat to peved and but un, the selfing to want wat ch and qu so lay, of he was wy, so ras sa was hin way loomew the gaves. Ap. She maree had usawas sknd braddy, crom bound was wing bed aged w"*

*(See `/screenshots` folder for the training curve, model output, and vocabulary output).*

## 5. Observations
- **Training Success:** The model successfully learned the structural patterns of the English language. The loss dropped significantly from 4.66 to 1.95, and the generated text contains clear English letter combinations and spacing. 
- **Why the text is gibberish:** The generated story does not make logical sense (e.g., "peved and but un"). This is expected for a Tiny Transformer. With only 582k parameters and 1,000 training steps on a small subset of data, the model has learned *how* to spell words, but it hasn't learned complex grammar or long-term coherence yet.
- **The Importance of Attention:** Unlike the Bag-of-Words model in Lab 01, this Transformer uses Self-Attention. This means it looks at the characters that came before it (e.g., if it sees "Onc", it knows "e" is highly likely to follow). However, its context window is very small.
- **Hardware Impact:** Training this model on a CPU would have taken hours. By switching the Colab runtime to a T4 GPU (cuda), the 1,000 training steps were completed in just a few minutes, proving the necessity of GPUs for deep learning.

## 6. Learning Outcomes
- Can implement the core components of a Transformer (embeddings, attention masking, feed-forward layers) from scratch using PyTorch.
- Understand the mechanics of next-token prediction and how loss curves indicate model learning.
- Can generate text using sampling (softmax + multinomial) and understand how model size and training steps impact text coherence.
- Understand the critical importance of GPUs for training deep neural networks.
