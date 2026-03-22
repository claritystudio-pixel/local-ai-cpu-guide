# How to Run a Local AI Model on CPU-Only Hardware Using LM Studio

## Why This Matters

Running a local AI model means your data stays private — nothing 
sent to external servers. It also functions as a personal memory 
system when connected to a tool like Obsidian. This guide is for 
anyone without a dedicated GPU who wants to make this work anyway.

---

## My Hardware

- CPU: AMD Ryzen 7 7700X — 8 Core, 16 Logical Processors @ 4501 MHz
- RAM: 32GB
- OS: Windows 11
- No dedicated GPU

---

## Step 1: Download LM Studio

Go to the official LM Studio website and download the desktop app.  
Current version used in this guide: **0.4.7**

Do not use third-party sources. Official site only.

---

## Step 2: Choose Your Model

Model size matters on CPU-only hardware. Stay at 8B parameters 
or under until you expand your RAM.

I started with Meta Llama 3.1 8B Instruct. I replaced it with 
**Qwen3 8B** after finding it performed better for my use case.

Also download: **nomic-embed-text** — required for vault indexing 
in Obsidian Copilot.

When downloading, enable **CORS** in LM Studio settings.

---

## Step 3: Configure Model Parameters

These settings are tuned for CPU-only performance:

| Parameter | Value |
|---|---|
| Temperature | 0.7 |
| Top P Sampling | 0.8 |
| CPU Threads | 8 |
| Context Length | 16,409 |
| Truncation | Middle |
| Reasoning | Off |

Save these as a preset for easy reloading.

---

## Step 4: Start the Local Server in LM Studio

1. In LM Studio go to the **Developer** tab 
2. Find **Local Server** — toggle it on 
3. It will display: **Reachable at:** followed by your server address 
4. Copy that address — you will paste it into Obsidian 
 --- 
## Step 5: Connect Obsidian Copilot to LM Studio

In Obsidian Copilot settings go to **Models** then ** Add Model**

**Add your chat model:**
- Model: Qwen3 8B Local
- URL: `http://localhost:1234/v1`
- Provider: LM Studio

**Add your embedding model:**
- Model: nomic-embed-text-v1.5
- URL: `http://127.0.0.1:1234/v1`
- API: Key: `lm-studio`
- Provider: LM Studio

**Critical:** Disable all other models listed above that show a cloud/internet connection. Those are not local- your data leaves your machine when they are active. 

---
## Step 6: Configure Copilot Plugin Settings

In the Copilot **Basic** tab: - Default Chat Model: **Qwen3 8B Local (LM Studio)** - Default Mode: **Vault QA (Basic)** In the Copilot **QA** tab: - Embedding Model: **nomic-embed-text-v1.5 (LM Studio)** 

---

## Current Limitation

32GB RAM limits you to 8B parameter models comfortably. Adding 
another 32GB RAM opens access to larger models with better performance.

---

## Goal

Privacy-first AI. A local model that knows your knowledge base 
and keeps everything on your own machine.
