# Coding Challenge: Building an Agent Swarm

## Introduction

Welcome to our coding challenge! This task is designed to assess your software engineering skills, your understanding of AI agent concepts, and your ability to build a robust, containerized application. You will be designing and building a multi-agent system where agents collaborate to process user requests and generate responses.

## The Challenge: Agent Swarm Implementation

Your task is to design and build an Agent Swarm. This swarm will consist of at least **three distinct types of agents** working together to process user messages.

### Core Requirements:
![image](https://gist.github.com/user-attachments/assets/3fb186ce-2e36-42eb-b06e-ba04d392ead9)

1.  **Agent Swarm Architecture:**
    * Implement a system with at least **three distinct types of agents**:

        * **Agent 1: Router Agent:**
            * This agent will be the primary entry point for user messages.
            * It should analyze the incoming message and decide which specialized agent (or sequence of agents) is best suited to handle it.
            * It will manage the workflow and data flow between other agents.

        * **Agent 2: Knowledge Agent:**
            * This agent will be responsible for handling queries that require information retrieval (Internal/External) and generation.
            * It must answer questions about the company’s products and services based on information primarily sourced from the company’s website: `https://www.infinitepay.io` (and its subpages).
            * The agent should implement or utilize a Retrieval Augmented Generation (RAG) approach to ensure responses are grounded in the provided website content.
            * Web Search tool for general purpose questions.
            * You can use the following webpages as data sources for the knowledge base:
              * `https://www.infinitepay.io`
              * `https://www.infinitepay.io/maquininha`
              * `https://www.infinitepay.io/maquininha-celular`
              * `https://www.infinitepay.io/tap-to-pay`
              * `https://www.infinitepay.io/pdv`
              * `https://www.infinitepay.io/receba-na-hora`
              * `https://www.infinitepay.io/gestao-de-cobranca-2` (and `/gestao-de-cobranca`)
              * `https://www.infinitepay.io/link-de-pagamento`
              * `https://www.infinitepay.io/loja-online`
              * `https://www.infinitepay.io/boleto`
              * `https://www.infinitepay.io/conta-digital` (and `/conta-pj`)
              * `https://www.infinitepay.io/pix` (and `/pix-parcelado`)
              * `https://www.infinitepay.io/emprestimo`
              * `https://www.infinitepay.io/cartao`
              * `https://www.infinitepay.io/rendimento`

        * **Agent 3: Customer Support Agent:**
            * This agent will provide customer support, retrieving relevant user data to answer the inquiries.
            * Create at least 2 tools for this agent.

    * Define a clear mechanism for these agents to communicate (e.g., direct function calls, internal message queue, event-driven).
    * Apply a Personality layer (workfow) in the final answer. This will allow to make it more like a human.

2.  **API Endpoint:**
    * Expose an HTTP endpoint (e.g., using FastAPI).
    * This endpoint should accept `POST` requests with a JSON payload in the following format:
        ```json
        {
          "message": "Your query or statement here",
          "user_id": "some_user_identifier"
        }
        ```
    * The endpoint should process the message through your agent swarm and return a meaningful JSON response. The final response should be from the Personality layer. Example:
        ```json
        {
          "response": "The personality-infused reply or final output",
          "source_agent_response": "The original response from RAG Agent before personality was applied.",
          "agent_workflow": [{"agent_name": "agent_one", "tool_calls": {"tool_a": "tool answer"}}], // Illustrative list of agents and tool_calls involved
        }
        ```

3.  **Dockerization:**
    * Provide a `Dockerfile` (and `docker-compose.yml` if necessary) to build and run your application.
    * The application should be easily runnable using standard Docker commands.

4.  **Testing:**
    * Write unit tests for your individual agents (e.g., testing the RAG agent's retrieval logic, the customer support agent, the Orchestrator's routing and the Personality transformation).
    * Write a few end-to-end (e2e) tests for the API endpoint, covering a couple of typical user queries.
    * Briefly describe in your documentation your overall testing strategy and how you would approach more comprehensive integration testing for the agent swarm.

5.  **Language & Frameworks:**
    * You are free to use any programming language for this challenge, though Python or Node.js/TypeScript are common choices for such tasks.
    * Choose appropriate libraries and frameworks for building the API, agents, RAG pipeline (e.g., Langchain, LlamaIndex, or others).

### What We're Looking For:

* **Code Quality:** Clean, well-structured, modular, and maintainable code.
* **Design & Architecture:** A logical and well-explained design for the agent swarm, their responsibilities, and interactions.
* **Good Quality Prompts:** High quality prompts that are able to properly express the Agent capabilities and scope.
* **RAG Implementation:** A functional RAG pipeline that can ingest content from the specified URLs and use it to answer questions.
* **Problem Solving:** How you approach the task of creating a multi-agent system and the specific challenges of RAG.
* **Testing:** The thoroughness and effectiveness of your tests.
* **Dockerization:** A working and easy-to-use Docker setup.
* **Documentation (`README.md`):**
    * Clear instructions on how to build, configure and run the application.
    * Explanation of your agent swarm architecture, design choices, and the workflow of a message.
    * Explain how you leveraged LLM tools to complete the case.
    * Details about how to run the tests.
    * Description of the RAG pipeline (how data is ingested, stored, retrieved, and used for generation).

### Submission:

* Please provide a link to a GitHub repository containing your solution.
* Ensure your `README.md` is comprehensive.

### Bonus Challenges:

* Introduce a fourth, distinct custom agent of your preference (e.g., a "Slack Agent" that can perform a specific action like asking for humans on slack).
* Consider an implementation of a Guardrails, that would enable us to handle undesired questions / responses.
* Consider an implementation of a Redirect mechanism, that would enable to redirect to a human.

Good luck, and we look forward to seeing your solution!

---

### Example Test Scenarios:

**User Sends:**
```json
{
  "message": "What are the fees of the Maquininha Smart",
  "user_id": "client789"
}

{
  "message": "What is the cost of the Maquininha Smart?",
  "user_id": "client789"
}

{
  "message": "What are the rates for debit and credit card transactions?",
  "user_id": "client789"
}

{
  "message": "How can I use my phone as a card machine?",
  "user_id": "client789"
}

{
  "message": "Quando foi o último jogo do Palmeiras?",
  "user_id": "client789"
}

{
  "message": "Quais as principais notícias de São Paulo hoje?",
  "user_id": "client789"
}

{
  "message": "Why I am not able to make transfers?",
  "user_id": "client789"
}

{
  "message": "I can't sign in to my account.",
  "user_id": "client789"
}
```