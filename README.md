<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/header-dark.svg">
  <img src="assets/header-light.svg" alt="Akshit Garg. Building LLM agents and RAG systems. An animated graph of the Claim Court agent nodes sits on the right." width="100%">
</picture>

## Model Details

| | |
| --- | --- |
| **Name** | Akshit Garg |
| **Role** | Data Science and CS student, building LLM agents and RAG systems |
| **Education** | B.S. Data Science and Applications, IIT Madras; B.Tech Computer Science, Surendera Group of Institutions |
| **Graduating** | 2027 |
| **Focus** | LLM agents, RAG, evaluation, backend services |
| **Location** | Sri Ganganagar, Rajasthan, India |

## Intended Use

Looking for AI/ML engineering roles where I can build LLM agents and RAG systems, evaluate them properly, and ship them behind solid backend services.


<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/divider-dark.svg">
  <img src="assets/divider-light.svg" alt="Section divider" width="100%">
</picture>
</p>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/metrics-dark.svg">
  <img src="assets/metrics-light.svg" alt="Three verified numbers. Validation R2 0.5598 vs 0.3 competition baseline, drawn as two bars to scale. 6 featured projects. 10 graph nodes in Claim Court." width="100%">
</picture>

<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/divider-dark.svg">
  <img src="assets/divider-light.svg" alt="Section divider" width="100%">
</picture>
</p>

## Architecture

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/stack-dark.svg">
  <img src="assets/stack-light.svg" alt="Layered diagram of the tools I use. Orchestration: LangGraph, LangChain. Retrieval: Chroma, FAISS, sentence-transformers, Tavily, Playwright. Models and ML: Groq, Gemini API, scikit-learn, LightGBM, XGBoost, pandas. Serving: FastAPI, Express, Celery, Redis, PostgreSQL, Docker. Frontend: Streamlit, Vue, Plotly." width="100%">
</picture>

<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/divider-dark.svg">
  <img src="assets/divider-light.svg" alt="Section divider" width="100%">
</picture>
</p>

## Evaluated Work

<p align="center">
<a href="https://github.com/24f2000777/claim-court">
<picture>
<source media="(prefers-color-scheme: dark)" srcset="assets/cards/claim-court-dark.svg">
<img src="assets/cards/claim-court-light.svg" alt="Claim Court card. Pipeline: retrieve_docs, grade_doc, web_search, grade_web, then prosecutor and defender in parallel, judge_node and verify_citations. Stack: LangGraph, Groq, Chroma, Streamlit." width="400">
</picture>
</a>
<a href="https://github.com/24f2000777/llm-quiz-solver">
<picture>
<source media="(prefers-color-scheme: dark)" srcset="assets/cards/llm-quiz-solver-dark.svg">
<img src="assets/cards/llm-quiz-solver-light.svg" alt="LLM Quiz Solver card. Pipeline: FastAPI endpoint, LangGraph loop, scrape_page, run_code, send_post. Stack: LangGraph, Groq, FastAPI, Playwright." width="400">
</picture>
</a>
<a href="https://github.com/24f2000777/llm-code-deployment">
<picture>
<source media="(prefers-color-scheme: dark)" srcset="assets/cards/llm-code-deployment-dark.svg">
<img src="assets/cards/llm-code-deployment-light.svg" alt="LLM Code Deployment card. Pipeline: request, Gemini generates app, GitHub Pages deploy. Stack: Node.js, Express, Gemini API." width="400">
</picture>
</a>
<a href="https://github.com/24f2000777/cinema-audience-forecasting">
<picture>
<source media="(prefers-color-scheme: dark)" srcset="assets/cards/cinema-audience-forecasting-dark.svg">
<img src="assets/cards/cinema-audience-forecasting-light.svg" alt="Cinema Audience Forecasting card. Features feed LightGBM and XGBoost, combined into an ensemble. Validation R2 0.5598 vs 0.3 competition baseline. Stack: LightGBM, XGBoost, scikit-learn." width="400">
</picture>
</a>
<a href="https://github.com/24f2000777/MAY2026-Team-059">
<picture>
<source media="(prefers-color-scheme: dark)" srcset="assets/cards/nagrik-ai-dark.svg">
<img src="assets/cards/nagrik-ai-light.svg" alt="NAGRIK AI card. Pipeline: complaint in, classify_intent, RAG chatbot, with the priority scorer alongside. Stack: FastAPI, Vue, PostgreSQL, LangGraph, FAISS." width="400">
</picture>
</a>
<a href="https://github.com/24f2000777/Churn_Dashboard">
<picture>
<source media="(prefers-color-scheme: dark)" srcset="assets/cards/churn-dashboard-dark.svg">
<img src="assets/cards/churn-dashboard-light.svg" alt="Churn Dashboard card. Pipeline: transactions, RFM, segments, Streamlit. Stack: pandas, Plotly, Streamlit." width="400">
</picture>
</a>
</p>

<details>
<summary>Claim Court: how it works</summary>

<br>

`retrieve_docs` searches the document in Chroma and `grade_doc` grades each passage.<br>
`web_search` runs two Tavily searches, one for support and one for contradiction, and `grade_web` scores the evidence. Weak evidence goes to `rewrite` and the search is retried.<br>
`prosecutor` and `defender` run in parallel, then the graph pauses so a human can review both cases before `judge_node`.<br>
`judge_node` returns supported, disputed or unsupported, and `verify_citations` checks each citation against the evidence it points to.<br>
State is saved in a SQLite checkpointer, so trials can be resumed.

</details>

<details>
<summary>LLM Quiz Solver: how it works</summary>

<br>

A FastAPI endpoint receives a quiz URL, checks a shared secret and starts the agent in the background.<br>
The agent is a LangGraph loop between a Groq model and four tools: `scrape_page` (Playwright), `install_package`, `run_code` and `send_post`.<br>
The model scrapes the page, writes and runs Python to answer the questions, and submits the answers.<br>
If the server's response includes another quiz URL, the agent solves that one next. Otherwise it stops.

</details>

<details>
<summary>NAGRIK AI: how my part works</summary>

<br>

The chatbot is a LangGraph conversation graph. `classify_intent` routes each message to a handler for filing a complaint, answering a location or photo follow-up, answering a question, app help or small talk.<br>
Complaint details are extracted into a structured schema by a Groq model, with Gemini and Hugging Face providers available as fallbacks.<br>
Questions about city rules are answered from a FAISS index of BMC documents (OCR, text splitting, MiniLM embeddings), retrieving the top 5 chunks.<br>
The priority scorer is a scikit-learn `HistGradientBoostingRegressor` served through a FastAPI endpoint. It is trained on a BMC complaints dataset using a priority formula I wrote, because the data has no priority label.

</details>

<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/divider-dark.svg">
  <img src="assets/divider-light.svg" alt="Section divider" width="100%">
</picture>
</p>

## Agent Trace

Illustrative trace. The claim is made up for the example.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/trace-dark.svg">
  <img src="assets/trace-light.svg" alt="Animated terminal replaying an illustrative Claim Court run. It steps through retrieve_docs, grade_doc, web_search, grade_web, prosecutor and defender in parallel, a pause for human review, judge_node and verify_citations, then saves the verdict and citation audit to the checkpoint." width="100%">
</picture>

<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/divider-dark.svg">
  <img src="assets/divider-light.svg" alt="Section divider" width="100%">
</picture>
</p>

## Currently Training

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/training-dark.svg">
  <img src="assets/training-light.svg" alt="Three projects in progress: Munim, LedgerLens and MoneyMentor." width="100%">
</picture>

## Limitations and Honest Notes

- Still learning FastAPI async patterns, PostgreSQL and evaluation methodology.
- The NAGRIK priority scorer learns a formula I defined, so it approximates that formula and is not trained on real outcomes.
- Claim Court's evaluation set is small (12 claims). Building a larger one is on my roadmap.

## Contact

[LinkedIn](https://www.linkedin.com/in/akshitgarg-ds) | [akshitgarg928@gmail.com](mailto:akshitgarg928@gmail.com)
