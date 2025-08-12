---
base_model: unsloth/Qwen3-0.6B-unsloth-bnb-4bit
tags:
- text-generation-inference
- transformers
- unsloth
- qwen3
- trl
license: apache-2.0
language:
- vn
---

# Uploaded  model

- **Developed by:** lammtfkday
- **License:** apache-2.0
- **Finetuned from model :** unsloth/Qwen3-0.6B-unsloth-bnb-4bit
- **Finetuned from dataset :** 5CD-AI/Vietnamese-Multi-turn-Chat-Alpaca

# How to use
You can use this model by loading directedly from huggingface:

from transformers import AutoTokenizer, AutoModelForCausalLM

tokenizer = AutoTokenizer.from_pretrained("lammtfkday/Vnchatbot-using-qwen3")
model = AutoModelForCausalLM.from_pretrained("lammtfkday/Vnchatbot-using-qwen3")
messages = [
    {"role": "user", "content": "Who are you?"},
]
inputs = tokenizer.apply_chat_template(
	messages,
	add_generation_prompt=True,
	tokenize=True,
	return_dict=True,
	return_tensors="pt",
).to(model.device)

outputs = model.generate(**inputs, max_new_tokens=40)
print(tokenizer.decode(outputs[0][inputs["input_ids"].shape[-1]:]))
