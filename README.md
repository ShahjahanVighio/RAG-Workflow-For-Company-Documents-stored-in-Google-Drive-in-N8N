# 📂 RAG Workflow For Company Documents stored in Google Drive

An enterprise-grade, event-driven **Retrieval-Augmented Generation (RAG) pipeline** built inside **n8n**. This workflow automates the ingestion, chunking, and embedding of internal corporate documents directly from a monitored **Google Drive** folder into a **Pinecone Vector Database**. It simultaneously exposes an interactive AI chat interface powered by **Google Gemini 2.0 Flash**, acting as an intelligent HR or internal operations assistant.

---

## 🛠️ Architecture & Core Components

The pipeline is structurally divided into two autonomous segments running within a single canvas[cite: 3]:

### 1. 🔄 Automated Document Ingestion Pipeline
* **Trigger:** Listens continuously for `fileCreated` or `fileUpdated` events within a targeted Google Drive directory.
* **Downloader:** Streams binary file payloads into the local staging execution context.
* **Text Splitter:** Uses a `Recursive Character Text Splitter` with a custom chunk overlap boundary (100 tokens) to ensure high contextual integration.
* **Vector Vector Store Ingestion:** Generates dense geometric representations via `Embeddings Google Gemini` and logs them natively to a dedicated `company-files` Pinecone index.

### 2. 💬 Cognitive RAG Retrieval Engine
* **Chat Interface Trigger:** Intercepts real-time internal user strings or questions.
* **AI Reasoning Agent:** Orchestrates structured system prompts instructing it to run exclusively as a helpful corporate assistant.
* **Vector Store Tool:** Dynamically acts as a semantic search bridge, connecting the agent queries to the contextual lookup system in Pinecone.
* **Window Buffer Memory:** Retains continuous multi-turn dialogue histories to provide context-aware responses.

---

## 🏗️ Setup & Environment Configuration

To deploy this workflow blueprint seamlessly, ensure you fulfill the following environmental setup conditions:

### 1. Google Cloud Platform & Vertex AI
* Establish a standard GCP development project space.
* Enable the **Vertex AI API** inside your platform service window.
* Generate a secure operational API key through **Google AI Studio**.

### 2. Pinecone Infrastructure
* Provision an account over at the Pinecone console portal.
* Capture your global account secret host API Key.
* Spin up a dedicated search vector database index explicitly named **`company-files`**.

### 3. Google Drive Setup
* Dedicate a single folder instance within your Google Drive system to isolate your internal business policy manuals.

---
<img width="378" height="357" alt="image" src="https://github.com/user-attachments/assets/1c74c547-2994-4a27-939d-7326e00f12c4" />
---

## 🚀 Installation & Activation

1. **Import the JSON File:** Clone or download the associated workflow file `RAG Workflow For Company Documents stored in Google Drive.json`, go to your n8n canvas screen, click the options menu (`...`), and hit **Import from File**.
2. **Configure n8n Global Credentials:**
   * **Google Drive OAuth2:** Connect an authorized access grant to query your target Drive.
   * **Google Gemini (PaLM) API:** Attach your explicit Google AI Studio developer secret keys.
   * **Pinecone API:** Match your account authorization headers to interact with the database index.
3. **Map Local Variable Handles:**
   * Adjust both the **Google Drive File Created** and **Updated** trigger nodes to focus cleanly on your target operational folder ID.
   * Validate that the vector embedding configuration properties reference your `company-files` database token target.
4. **Deploy the Pipeline:** Turn the execution toggle state to **Active** to start parsing documents completely on autopilot[cite: 3]!

---

## 🛡️ Guardrail Configuration
The underlying AI assistant agent is engineered with defensive strict system guidelines[cite: 3]:
> If the specific, granular answer cannot be completely synthesized from the verified vector payload returns, the agent is restricted to responding with a standardized fallback string: *"I cannot find the answer in the available resources."*[cite: 3]
