# emotion-classification---Qwen3-QLoRA
## 🔷 Overview
This repository presents experiments from an NLP class project, where we fine-tuned and compared encoder-only and decoder-only language models on a multi-label emotion classification task using QLoRA and PEFT. We worked with tweets labeled for 11 emotions and explored two approaches:

- Classification head (predicts binary labels)
- Label generation (predicts the emotion labels as text)

We submitted our predictions to the Kaggle competition and tracked experiments with Weights & Biases (W&B)

# 📊 Methods & Models

## 🔷 Experiment 1 – RoBERTa
Model name: roberta-base (encoder-only)

Task: Multi-label emotion classification with BCEWithLogitsLoss + pos_weight to handle imbalance.

- Metrics:
  
Macro F1: 0.5416
 
Micro F1: 0.6132

Validation loss: 0.6379 

Kaggle Public Score: **0.52961.**

*Good for: Showing strong performance on multi-label tasks with a classic encoder + classification head setup*.

## 🔷 Experiment 2 – QLoRA + Qwen2.5-7B
Model name: Qwen2.5-7B (decoder-only, fine-tuned with QLoRA).

Task: Same multi-label emotion classification but using decoder model + QLoRA.

- Metrics:
  
Macro F1: 0.2542

Micro F1: 0.3139

Kaggle Public Score: **0.30040**

*Good for: Showing how a decoder-only model fine-tuned with QLoRA performs worse than the encoder-based approach on this task, potentially due to architectural mismatch for classification.*

## 🔷 Experiment 3 – QLoRA + Qwen3 (Label Generation)
Model name: Qwen3 (decoder-only, QLoRA, label generation as text)

Task: Emotion label generation (instead of classification head).

- Metrics:

Eval Loss: 2.73456

Mean Token Accuracy: ~54.3%

Training Loss: 2.6456

Kaggle Public Score: **0.486**

*Good for: Showing that framing the task as text generation (rather than classification) improves performance compared to Qwen2.5 + classification head, though still below RoBERTa.*


# 📝 Results & Comparisons
| Model                 | Approach             | Kaggle Public Score | Macro F1 (Val)                       |
| --------------------- | -------------------- | ------------------- | ------------------------------------ |
| **Exp 1: RoBERTa**    | Encoder + Class Head | **0.5296**          |     **0.5416**                       |
| **Exp 2: Qwen2.5-7B** | Decoder + Class Head | **0.30040**         |     **0.2542**                       |
| **Exp 3: Qwen3-0.6B** | Decoder + Gen Labels | **0.486**           | *(N/A for F1, Token Accuracy \~54%)* |



# 📊 Insights
The experiments highlight clear differences between encoder and decoder approaches:

Exp 1: Roberta (Encoder + Class Head) performed best, with the highest macro F1 (0.5416) and Kaggle score (0.5296), showing the strength of encoders for multi-label tasks.

Exp 2: Qwen2.5-7B (Decoder + Class Head) struggled, scoring much lower (macro F1: 0.2542, Kaggle: 0.3004), suggesting decoders are less suited for classification heads.

Exp 3: Qwen3-0.6B (Decoder + Label Generation) improved significantly over Exp 2, with a Kaggle score of 0.486 and ~54% token accuracy, proving label generation aligns better with decoder capabilities.

Overall, Roberta was the strongest, but Qwen3 showed promise when used as a label generator rather than a classifier.


![image](https://github.com/user-attachments/assets/e9db8dc7-60f5-40bc-8f5e-cbdf00b6a9b0)

