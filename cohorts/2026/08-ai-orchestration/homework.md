## Module 8 Homework: AI Orchestration and Agents

ATTENTION: At the end of the submission form, you will be required to include a link to your GitHub repository or other public code-hosting site. This repository should contain your code for solving the homework. If your solution includes code that is not in file format, please include these directly in the README file of your repository.

> In case you don't get one option exactly, select the closest one

---

## Prerequisites

Before starting this homework, ensure you have:
2. Kestra running locally
3. Google Gemini API key (get it from https://aistudio.google.com/app/apikey)
4. (Optional) Tavily API key for web search examples (get it from https://tavily.com/)
5. Imported/added all flows from the `08-ai-orchestration/flows/` directory

---

## Assignment Overview

This homework explores AI workflows and agents in Kestra. You'll experiment with:
- Context engineering and why it matters
- RAG (Retrieval Augmented Generation) for grounded AI responses
- AI Agents for autonomous task execution
- Multi-agent systems for complex AI workflows

---

## Setup Instructions

1. **Export your API keys as secrets before starting Kestra:**

⚠️ **Important**: Never commit API keys to Git! Export them as environment variables — Kestra picks them up automatically.

```bash
export SECRET_GEMINI_API_KEY=$(echo -n "your-gemini-api-key-here" | base64)
export SECRET_TAVILY_API_KEY=$(echo -n "your-tavily-api-key-here" | base64)  # optional, for web search examples
```

Then start Kestra:

```bash
cd 08-ai-orchestration
docker compose up -d
```

In flows, these are referenced as `{{ secret('GEMINI_API_KEY') }}` — omit the `SECRET_` prefix when calling `secret()`.

2. **Import the homework flows:**

```bash
cd 08-ai-orchestration

# Import flows: assuming username admin@kestra.io and password Admin1234 (adjust to match your username and password)
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/1_chat_without_rag.yaml
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/2_chat_with_rag.yaml
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/3_simple_agent.yaml
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/4_web_research_agent.yaml
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/5_multi_agent_research.yaml
```

---

## Quiz Questions

### Question 1: Context Engineering

First, try the following experiment:
1. Open ChatGPT in a private browser window: https://chatgpt.com
2. Enter this prompt: "Create a Kestra flow that loads NYC taxi data from CSV to BigQuery"
3. Then, use Kestra's AI Copilot with the same prompt

After trying the same prompt in ChatGPT vs Kestra Copilot, what is the primary reason Copilot generates better Kestra flows?

- a) Copilot uses a more powerful model
- b) Copilot has access to current Kestra plugin documentation
- c) Copilot uses more tokens
- d) Copilot has internet access

---

### Question 2: RAG Comparison

Run both `1_chat_without_rag.yaml` and `2_chat_with_rag.yaml` flows and compare their outputs. Both ask: "Which features were released in Kestra 1.1?"

When comparing the outputs, what difference do you observe?

- a) RAG version provides specific, accurate feature details grounded in the documentation
- b) Both produce identical results
- c) Non-RAG version is more detailed and accurate
- d) RAG version hallucinates more features than the non-RAG version

---

### Question 3: Token Usage

Run the `3_simple_agent.yaml` flow twice:
1. First with `summary_length` = "short"
2. Second with `summary_length` = "long"

Check the token usage logged at the end of each execution. How does token usage differ between short and long summaries for the `multilingual_agent` task?

- a) No significant difference (within 10% variance)
- b) Long summary uses 2-4x more output tokens than short summary
- c) Short summary uses more tokens due to compression complexity
- d) Token usage is identical regardless of length

---

### Question 4: Agent Autonomy

Run the `4_web_research_agent.yaml` flow with the default research topic about data orchestration trends.

In this flow, who decides when to use the web search tool?

- a) The workflow designer specifies exact tool usage order in YAML
- b) The agent autonomously decides based on the prompt and system message
- c) Tools are called randomly by the LLM
- d) Web search runs on every agent execution automatically

---

### Question 5: Multi-Agent Collaboration

Examine the `5_multi_agent_research.yaml` flow and run it with the default company (kestra.io).

What is the role of the research agent in this multi-agent system?

- a) It makes final decisions about company analysis and structures the output
- b) It serves as a tool for the main agent to gather web data
- c) It summarizes the main agent's findings into a report
- d) It validates the main agent's output for accuracy

---

### Question 6: Best Practices

Based on what you learned in this module, for production workflows requiring deterministic, repeatable results with strict compliance requirements (e.g., financial reporting, workflows in highly regulated industries), which approach is most appropriate?

- a) Always use AI agents for maximum flexibility and adaptation
- b) Use traditional task-based workflows for predictability and auditability
- c) Use only RAG without agents for better performance
- d) Use web search tools exclusively to ensure current data

---

## Submitting the Solutions

* Form for submitting: [Link will be provided by course organizers]
* Check the link above to see the due date

Submit your answers to the 6 quiz questions above via the course submission form.

---

## Solution

Will be added after the due date.

---

## Tips for Success

1. **API Keys**: Make sure your `SECRET_GEMINI_API_KEY` environment variable is exported before running `docker compose up -d`
2. **Free Tier Limits**: If you hit rate limits, wait a few minutes and try again
3. **Debugging**: Enable `logRequests` and `logResponses` in your provider configuration to see what's being sent to the LLM
4. **Cost Monitoring**: Check token usage in execution logs to understand costs
5. **Community**: Ask questions in the course Slack channel if you get stuck

---

## Additional Resources

- [Kestra AI Documentation](https://kestra.io/docs/ai-tools)
- [Gemini API Documentation](https://ai.google.dev/docs)
- [Module 8 README](../../../08-ai-orchestration/README.md)
- [Kestra Slack Community](https://kestra.io/slack)

Good luck! 🚀