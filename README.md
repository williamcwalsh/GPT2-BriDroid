# GPT-2 BriDroid 1.0

This is a fine-tuned version of GPT-2 trained on thousands of real group chat messages from my friend Brio. It captures the tone, slang, and personality of how he texts — including sarcasm, dry humor, and at times unprompted chaotic outbursts (sorry Brio).

## What It Does
- Mimics a specific person’s texting style
- Generates responses based on prompts you give it
- Great for parody, conversation emulation, or just messing with your group chat

## Training Process
- Fine-tuned using HuggingFace Transformers on top of GPT-2
- Dataset: ~50,000 filtered and cleaned messages.
  Note: Since the dataset consists of individual messages without paired prompts and responses, the model was trained to imitate his tone and style rather than learn full conversation flow. As a result, replies may sound like him but don’t always directly answer the prompt. This will be addressed in future versions.
- Format: Single-line messages (`{"text": "..."}`) or dialogue pairs (`{"prompt": "...", "response": "..."}`)

## How to Use It

### Step 1: Download and unzip the model folder
Download brio_model.zip from the first release or under this text, unzip it, and note the folder path.
https://github.com/williamcwalsh/GPT2-BriDroid/releases/download/v1.0/brio_model.zip


### Load the model in your Python environment
Install transformers if you haven’t already:
```
pip install transformers
```
Then run:
```
from transformers import GPT2LMHeadModel, GPT2Tokenizer, pipeline

model = GPT2LMHeadModel.from_pretrained("brio_model")
tokenizer = GPT2Tokenizer.from_pretrained("brio_model")

generator = pipeline("text-generation", model=model, tokenizer=tokenizer)
```
### Generate a reply using a conversational prompt
Try something like this:
```
prompt = "me: what happened at the party?\nfriend:"
output = generator(
    prompt,
    max_length=60,
    do_sample=True,
    temperature=0.9,
    top_k=40,
    top_p=0.95,
    pad_token_id=tokenizer.eos_token_id
)

print(output[0]["generated_text"])
```


