# 🤖 Personalized Learning Path Creator

## Project Overview
This project is a dynamic, serverless workflow built on **n8n** that converts a single text input (a user's learning goal) into a structured, actionable, and ready-to-execute project plan on a **Trello** board.

It solves the problem of information overload by synthesizing real-time web search results into a clean, prioritized, step-by-step curriculum.

## ✨ Features

* **Dynamic Input:** Triggered by a public N8N form URL.
* **AI Synthesis:** Uses a **Groq/LLM Agent** to synthesize information and structure the learning path.
* **Real-Time Research:** Integrates with **Serper.dev** (Google SERP API) to fetch current, highly-rated tutorials and documentation.
* **Dynamic Trello Setup:** Automatically creates a **new, uniquely named Trello list** for every new learning request to keep projects organized.
* **Actionable Output:** Creates **five separate Trello cards** per request, each containing a specific learning step, description, and direct resource links.

## 🛠️ Tech Stack & Requirements

| Tool/Service | Purpose | Implementation |
| :--- | :--- | :--- |
| **n8n** | Workflow Orchestration | Workflow JSON file |
| **Groq / LLM** | AI Reasoning, Synthesis, JSON Output | `lmChatGroq` Node |
| **Serper.dev** | Real-time Web Search Results | `HTTP Request` Node |
| **Trello** | Project Management Output | `Create a list`, `Create a card` Nodes |

### Prerequisites

To run this workflow on your own N8N instance, you must have the following credentials configured:

1.  **Groq API Key:** Required for the AI Agent.
2.  **Serper.dev API Key:** Required for the HTTP Request (must be set in the `X-API-KEY` header).
3.  **Trello API Key & Token:** Required to create lists and cards.

## 🚀 Getting Started (Deployment)

### 1. Import the Workflow

1.  Download the `personalized-learning-path-creator.json` file from this repository.
2.  Log into your N8N instance.
3.  Click **"Add workflow"** and select **"Import from JSON"** to upload the file.

### 2. Configure Credentials

* Update the credentials in the **Groq Chat Model** and **Trello** nodes with your own API keys.
* In the **HTTP Request** node, update the **`X-API-KEY`** header with your Serper.dev API key.

### 3. Run the Workflow

1.  Switch the entire workflow to **"Active."**
2.  Open the **Production URL** of the **'On form submission'** node in your browser.
3.  Enter a new skill (e.g., "Learn Next.js authentication") and submit the form.

The entire process will execute, and a new list containing the five learning steps will appear instantly on your configured Trello board.

---

## 📈 Challenges Overcome

The complexity of this project involved solving a **Multi-Branch Data Merging** problem:

* The crucial fix involved using the **Merge** node (set to **Combine** with **All Possible Combinations**) and the explicit index reference (`{{ $node["Create a list"].json[0].id }}`) to reliably attach the List ID to every individual card item, ensuring all 5 cards landed in the single, newly created list.

---

### Author
Yashasvi Pandey 