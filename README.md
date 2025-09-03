# AIAgent_ChatBot_using_LangGraph

# 🚀 Advanced Chatbot with LangGraph, Streamlit, and Tools

This project showcases the development of a conversational AI application, building up from a basic chatbot to a feature-rich platform. It leverages the power of **LangGraph** for creating robust, stateful LLM agents and **Streamlit** for a reactive, user-friendly web interface.

The repository illustrates a clear progression through different versions, each adding a new layer of functionality.

## ✨ Key Features

* **Stateful Conversations**: Remembers chat history within a session and across sessions.
* **Persistent Memory**: Uses **SQLite** to save and load conversation threads, allowing users to resume past interactions.
* **Multi-Threaded Interface**: A clean sidebar allows users to switch between different conversations or start a new one.
* **LLM Tool Integration**: The agent can use external tools like **DuckDuckGo Search**, a **calculator**, and a **stock price fetcher** to answer complex queries.
* **Real-time Streaming**: Responses from the language model are streamed token-by-token for an interactive, real-time feel.
* **Dynamic UI for Tool Usage**: The interface provides real-time feedback when a tool is being used by the agent, showing the user what's happening behind the scenes.

---

## 📈 Project Evolution

The provided files demonstrate a step-by-step evolution of the chatbot:

1.  **Version 1: Basic In-Memory Chat**
    * `langgraph_backend.py`: A simple LangGraph graph with one node that calls the LLM. It uses `InMemorySaver` for the checkpointer, meaning history is lost when the app restarts.
    * `streamlit_frontend.py`: A basic Streamlit UI that sends a user's query to the backend and displays the response. It has a hardcoded `thread_id`.

2.  **Version 2: Adding Streaming**
    * `streamlit_frontend_streaming.py`: The frontend is updated to use `st.write_stream` to display the AI's response as it's being generated, improving user experience.

3.  **Version 3: Persistent Database & Multi-Threading**
    * `langgraph_database_backend.py`: The backend is upgraded to use `SqliteSaver`, saving conversation checkpoints to a `chatbot.db` file. A helper function `retrieve_all_threads` is added.
    * `streamlit_frontend_database.py` & `streamlit_frontend_threading.py`: The frontend now features a sidebar to list all saved conversation threads. Users can start new chats or load previous ones. `uuid` is used to generate unique thread IDs.

4.  **Version 4: The Complete Tool-Using Agent (Final Version)**
    * `langgraph_tool_backend.py`: The backend is significantly enhanced. It now includes tools (`DuckDuckGoSearchRun`, `calculator`, `get_stock_price`). The graph is updated with a `ToolNode` and conditional edges (`tools_condition`) to create an autonomous agent that can decide when to call a tool.
    * `streamlit_frontend_tool.py`: This is the most advanced frontend. It not only handles streaming and multi-threaded conversations but also intelligently detects when a `ToolMessage` is part of the stream. It then uses `st.status()` to display which tool the agent is currently using, providing excellent transparency to the user.

---

## ⚙️ Technology Stack

* **Backend Framework**: LangGraph
* **LLM Orchestration**: LangChain
* **LLM Provider**: OpenAI
* **Web Framework**: Streamlit
* **Database**: SQLite for conversation history
* **Tools**: DuckDuckGo Search, Requests (for APIs)

---

## 📦 Setup and Installation

Follow these steps to get the project running on your local machine.

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd <your-repository-directory>
```


Create a Virtual Environment

```
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```
3. Install Dependencies

```
pip install -r requirements.txt
```

4. Set Up Environment Variables
The application requires an OpenAI API key. Create a file named .env in the root directory and add your key:

OPENAI_API_KEY="sk-YourSecretOpenAIKeyGoesHere"
Note: The get_stock_price tool in langgraph_tool_backend.py has a hardcoded Alpha Vantage API key. For production use, you should move this to the .env file as well.

▶️ How to Run the Application
You can run any version of the application. To run the most complete version with tool integration, use the following command:

```
streamlit run streamlit_frontend_tool.py
```
Your web browser will open a new tab with the chatbot interface.

To run simpler versions, simply replace the filename:

streamlit run streamlit_frontend.py (Basic, in-memory)

streamlit run streamlit_frontend_database.py (Database persistence)

📂 Code Overview
---
langgraph_*_backend.py: These files define the LangGraph agent's logic, state, and tools.

streamlit_*_frontend.py: These files contain all the Streamlit code for building the user interface, handling user input, and managing session state.

requirements.txt: Lists all project dependencies.

chatbot.db: The SQLite database file that will be automatically created to store conversation history when running the database or tool-enabled versions.

💡 Future Improvements
---
Error Handling: Implement more robust error handling on both the frontend and backend.

Deploy to Cloud: Containerize the application using Docker and deploy it to a cloud service like Streamlit Community Cloud or Hugging Face Spaces.

Add More Tools: Expand the agent's capabilities by integrating more APIs and custom functions.

Enhanced UI: Add features like copying code blocks, displaying structured tool outputs, and user feedback mechanisms.
