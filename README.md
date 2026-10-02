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

## Architecture

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/stack-dark.svg">
  <img src="assets/stack-light.svg" alt="Layered diagram of the tools I use. Orchestration: LangGraph, LangChain. Retrieval: Chroma, FAISS, sentence-transformers, Tavily, Playwright. Models and ML: Groq, Gemini API, scikit-learn, LightGBM, XGBoost, pandas. Serving: FastAPI, Express, Celery, Redis, PostgreSQL, Docker. Frontend: Streamlit, Vue, Plotly." width="100%">
</picture>

## Evaluated Work

| Project | What it does | Stack | Link |
| --- | --- | --- | --- |
| **Claim Court** | Two LLM agents argue opposite sides of a claim from the same evidence, a judge rules, and a citation audit checks the sources. | LangGraph, Groq, Chroma, Streamlit | [repo](https://github.com/24f2000777/claim-court) |
| **LLM Quiz Solver** | Autonomous agent that scrapes quiz pages, runs generated Python and submits answers through a FastAPI service. | LangGraph, Groq, FastAPI, Playwright | [repo](https://github.com/24f2000777/llm-quiz-solver) |
| **LLM Code Deployment** | API that takes a task request, generates a web app with an LLM and deploys it to GitHub Pages. | Node.js, Express, Gemini API | [repo](https://github.com/24f2000777/llm-code-deployment) |
| **Cinema Audience Forecasting** | Predicts daily theater audience counts with a LightGBM and XGBoost ensemble. R2 0.5598 against a competition baseline of 0.3. | LightGBM, XGBoost, scikit-learn | [repo](https://github.com/24f2000777/cinema-audience-forecasting) |
| **NAGRIK AI** | Team civic complaint platform. Designed and built the AI layer: the ML priority scorer and the RAG chatbot. | FastAPI, Vue, PostgreSQL, LangGraph, FAISS | [repo](https://github.com/24f2000777/MAY2026-Team-059) |
| **Churn Dashboard** | RFM customer segmentation on retail transactions with a Streamlit dashboard. | pandas, Plotly, Streamlit | [repo](https://github.com/24f2000777/Churn_Dashboard) |

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

## Agent Trace

Illustrative trace of a Claim Court run, using the real node names and order. The claim is made up for the example.

```text
claim: "Cold showers boost immunity"
[00:00.0] retrieve_docs      searching document index
[00:00.6] grade_doc          grading retrieved passages
[00:01.4] web_search         query A: evidence for | query B: evidence against
[00:03.1] grade_web          evidence ok, no rewrite needed
[00:03.2] prosecutor         arguing the claim is false      (parallel)
[00:03.2] defender           arguing the claim is true       (parallel)
[00:06.8] interrupt          paused for human review
[00:09.0] judge_node         ruling: supported | disputed | unsupported
[00:11.5] verify_citations   checking each citation against its evidence
[00:12.4] done               verdict and citation audit saved to checkpoint
```

## Currently Training

- **Munim:** in progress.
- **LedgerLens:** in progress.
- **MoneyMentor:** in progress.

## Limitations and Honest Notes

- Still learning FastAPI async patterns, PostgreSQL and evaluation methodology.
- The NAGRIK priority scorer learns a formula I defined, so it approximates that formula and is not trained on real outcomes.
- Claim Court's evaluation set is small (12 claims). Building a larger one is on my roadmap.

## Contact

[LinkedIn](https://www.linkedin.com/in/akshitgarg-ds) | [akshitgarg928@gmail.com](mailto:akshitgarg928@gmail.com)
