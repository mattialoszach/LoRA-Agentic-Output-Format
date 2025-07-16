# LoRA for Agentic Output Format

## 📌 Motivation

While building LLM-based agents, I repeatedly faced the challenge of enforcing **structured outputs** – specifically **machine-readable JSON** formats – from large language models (LLMs).  
I initially relied on **prompt engineering** to instruct models to follow a specific format. Although this worked in many cases, it was not always **reliable or deterministic**.

So I explored whether a model could **learn the structure itself** through fine-tuning.  
That's where **LoRA** (Low-Rank Adaptation) came in: it allowed me to **efficiently train** a model to consistently return responses in a **fixed JSON format**, suitable for agentic pipelines and downstream automation.

---

## 🔧 What This Project Does

This repository contains a LoRA-finetuned version of [`Qwen3-1.7B`](https://huggingface.co/Qwen/Qwen1.5-1.8B) that behaves like an IT support assistant.  
Given a user input (e.g. a support request), the model returns a structured JSON object with the following fields:

```json
{
  "action": "...",
  "query": "...",
  "result": {
    "status": "...",
    "details": "..."
  },
  "reasoning": "..."
}
```

---

> [!NOTE]
> ## 💡 How to implement the strategy
> It is important to note that after fine-tuning with LoRA, the model may confuse semantically similar actions. Therefore, to guarantee semantic accuracy use Prompt Engineering or Retrieval-Augmented Generation (RAG) to inject semantic context.
>
> Combined, this results in an LLM that can:
> - output reliable structured responses
> - align those responses with task-specific meaning, driven by context
