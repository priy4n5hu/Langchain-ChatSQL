# Chat with SQL DB

A Streamlit app that lets you ask questions about a SQL database in plain English. It uses LangChain's SQL agent with Groq's LLaMA 3.3 70B model to translate your questions into SQL queries, run them, and explain the results back to you.

## What it does

You type something like "show me all students with marks above 80" and the app figures out the SQL, runs it against your database, and gives you a readable answer. No SQL knowledge required.

Works with either a local SQLite database (a `student.db` file bundled with the project) or your own MySQL database, switchable from the sidebar.

try it here: [https://langchain-chatsql-123.streamlit.app/](https://langchain-chatsql-123.streamlit.app/)
## Setup

Clone the repo and install dependencies:

```bash
git clone <your-repo-url>
cd 6-ChatSQL
python -m venv .venv
source .venv/bin/activate  # on Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

You'll need a free Groq API key. Get one at [console.groq.com](https://console.groq.com) and paste it into the sidebar when you run the app — it's not stored anywhere.

## Running it

```bash
streamlit run app.py
```

This opens the app in your browser, usually at `http://localhost:8501`.

From the sidebar:
1. Choose SQLite (uses the local `student.db`) or MySQL (you'll need to provide host, user, password, and database name).
2. Enter your Groq API key.
3. Start asking questions in the chat box.

## Project structure

```
.
├── app.py              # main Streamlit app
├── student.db           # sample SQLite database
├── requirements.txt
└── README.md
```

## Notes on the model

The app uses `llama-3.3-70b-versatile` via Groq. Smaller/faster Groq models (like the 8B instant one) tend to struggle with the multi-step reasoning the SQL agent needs — they'll often misread the schema or return half-baked answers. Stick with the 70B model unless you're specifically optimizing for speed over accuracy.

## A few known limitations

- The agent occasionally needs a fairly specific question to know which table you mean if your database has several.
- The SQLite connection is opened read-only, so write queries against the local DB won't work (and generally shouldn't, for a chat interface like this).
- There's no query result caching, so repeated questions re-run against the database each time.

## License

MIT — do whatever you want with it.
