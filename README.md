# 🏷️ The Price is Right – Autonomous Deal Hunting Agent

An autonomous multi-agent system that scans the internet for product deals, estimates their true value using an ensemble of AI models, and sends push notifications when a significant bargain is found.

This project combines:

- 🔎 Web scraping + structured LLM extraction  
- 🧠 RAG-based price estimation  
- 🤖 Fine-tuned LLM inference (Modal deployment)  
- 🧮 Deep neural network regression  
- 📲 Push notifications via Pushover  
- 🗂 Persistent memory to prevent duplicate alerts  

---

# 🏗 Architecture Overview

RSS Feeds  
↓  
ScannerAgent (LLM filters + structures deals)  
↓  
PlanningAgent / AutonomousPlanningAgent  
↓  
EnsembleAgent  
├── FrontierAgent (RAG + OpenAI)  
├── SpecialistAgent (Fine-tuned LLM on Modal)  
└── NeuralNetworkAgent (Local deep net)  
↓  
MessagingAgent (Push notification)  
↓  
memory.json (Persistent deal history)

---

# 🧠 Core Components

## 🔎 ScannerAgent
- Scrapes RSS feeds
- Uses structured LLM outputs to select 5 high-quality deals
- Filters out previously seen URLs (persistent deduplication)

## 🧮 EnsembleAgent
Combines 3 independent price estimators:

| Agent | Description |
|--------|------------|
| FrontierAgent | RAG search over Chroma vector DB + LLM estimation |
| SpecialistAgent | Fine-tuned Llama model deployed on Modal |
| NeuralNetworkAgent | Local PyTorch deep residual network |

Final price =  
0.8 * Frontier + 0.1 * Specialist + 0.1 * NeuralNet

---

## 🤖 AutonomousPlanningAgent
LLM-driven orchestration using tool-calling:
- scan
- estimate
- notify

Ensures:
- Only one notification per run
- No duplicate deals across runs

---

## 📲 MessagingAgent
- Crafts short, exciting push alerts
- Sends via Pushover API

---

# 🗂 Persistent Memory

Deals already surfaced are stored in:

memory.json

This prevents:
- Duplicate alerts within the same run
- Re-alerting the same URL across future runs

---

# 🧾 Dataset & Training

## items.py
Defines the `Item` schema for training and evaluation.
Supports:
- Prompt formatting for supervised fine-tuning
- Pushing/loading datasets from Hugging Face Hub

## Fine-tuned Model
Loaded via Modal from Hugging Face:

HF_USER = "ed-donner"

---

# 🚀 Running the Project

## 1️⃣ Install dependencies
pip install -r requirements.txt

## 2️⃣ Set environment variables

OPENAI_API_KEY=
PUSHOVER_USER=
PUSHOVER_TOKEN=

(Optional for Modal fine-tuned model)
HUGGINGFACE_TOKEN=

## 3️⃣ Run the app
python price_is_right.py

---

# 📊 Evaluation

Use evaluator.py to:
- Compute MAE
- Compute MSE
- Plot predicted vs actual price
- View confidence intervals

---

# 🧪 Modes

You can run:

- Deterministic planning (PlanningAgent)
- Fully autonomous LLM tool-based planning (AutonomousPlanningAgent)

---

# 🎯 What This Project Demonstrates

- Real-world multi-agent orchestration
- RAG pipelines in production
- Tool-using autonomous LLM agents
- Hybrid ML + LLM ensemble systems
- Persistent state management
- Deployment-ready architecture