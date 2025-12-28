# ADK Agent API: Smart POS Inventory Assistant

This project is a unified AI agent API designed for **Point of Sale (POS) Inventory Management**.  
It combines the power of the **Google Agent Development Kit (ADK)** with **FastAPI** into a single executable script.

---

## 🚀 Features

 
- **Natural Language Inventory**  
  Query stock levels, menu details, and production limits using LLM.

- **Smart Bottleneck Detection**  
  Automatically calculates how many units of an item can be made based on current raw material stock.

- **Multi-Model Support**  
  Powered by `LiteLLM` to support models like GPT-4o-mini or Gemini.

---

## 🛠️ Tech Stack

- **Framework**: FastAPI  
- **Agent Engine**: Google ADK  
- **LLM Gateway**: LiteLLM  
- **Server**: Uvicorn  

---

## 📁 Project Structure

```text
.
├── mock_data.py       # Static data 
├── agent.py           # The complete application (Agent + Tools + API)
├── server.py          # Expose the agent with fastapi
├── .env              # Your API keys (OPENAI_API_KEY)
└── requirements.txt  # Dependencies
```

---

## ⚙️ Quick Start

### 1. Install Dependencies

```bash
pip install fastapi pydantic python-dotenv litellm uvicorn google-genai
```

### 2. Setup Environment

Create a `.env` file and add your provider key:

```env
OPENAI_API_KEY=your_openai_key_here
GOOGLE_GENAI_USE_VERTEXAI=FALSE
```

### 3. Run the Application

```Terminal
uvicorn my_agent.server:app --reload
```

The server will start at:

```
http://127.0.0.1:8000
```

---

## 🔌 API Endpoints

### 1. Create Session

**POST** `/session`

Initializes a tracking session for a user to maintain conversation history.

```json
{
    "appName": "Inventory_agent",
    "userId": "user_4",
    "sessionId": "s_004"
}
```

---

### 2. Run Agent

**POST** `/run`

Send your inventory questions to the agent.

```json
 {
  "appName": "Inventory_agent",
  "userId": "user_4",
  "sessionId": "s_004",
  "newMessage": {
    "parts": [{"text": "what can you do?"}]
  }
}

```

---

## 🤖 Integrated Tools

The agent can automatically call these functions based on user input:

### get_menu_item
Returns specific item details and ingredients.

### get_all_menu
Returns a full status report of the entire menu.

### get_item_production_capacity
Identifies the bottleneck ingredient and calculates maximum production capacity.

