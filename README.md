I want to build an AI-powered SQL Analytics Agent from scratch using Python and LangGraph.

The goal is to create a schema-aware, agentic SQL assistant that allows users to ask questions about a relational database using natural language. The agent should understand the database structure, identify the relevant tables and columns, generate accurate SQL queries, validate them, execute them safely, and explain the results in natural language.

Important: This should be built as a real LangGraph agent, not as a simple linear LLM → SQL pipeline.

Core architecture:

User Question
    ↓
Intent Understanding
    ↓
Schema Discovery / Schema Knowledge
    ↓
Relevant Schema Retrieval
    ↓
SQL Generation
    ↓
SQL Validation
    ↓
Decision / Routing
    ├── Valid → Execute SQL
    └── Invalid → Analyze Error → Correct SQL → Validate Again
    ↓
Result Analysis
    ↓
Final Natural Language Response

Requirements:

1. Use LangGraph as the primary agent orchestration framework.
2. Use Python for the implementation.
3. Use SQLAlchemy for database connectivity.
4. Initially support a relational SQL database such as PostgreSQL or SQLite.
5. The agent should inspect the database schema and understand:
   - Tables
   - Columns
   - Data types
   - Primary keys
   - Foreign keys
   - Relationships
6. Do not send the entire database schema to the LLM for every user query.
7. Build a schema retrieval mechanism that identifies the most relevant tables and columns based on the user's question.
8. The agent should generate SQL using the retrieved schema context.
9. Add a SQL validation step before execution.
10. Only allow safe/read-only SQL operations initially. Do not allow INSERT, UPDATE, DELETE, DROP, ALTER, TRUNCATE, or other destructive operations.
11. If SQL execution fails, the agent should inspect the error, correct the query, and retry through the LangGraph workflow.
12. Add routing/conditional edges so the graph can decide what action to take based on the current state.
13. The agent should handle ambiguous questions appropriately instead of blindly generating SQL.
14. After execution, analyze the returned data and provide a clear natural-language answer.
15. Initially run everything through a terminal/CLI interface. Do not build a UI yet.
16. Keep the architecture modular so a web UI can be added later without changing the core agent.
17. Maintain a clean LangGraph State object containing the user question, schema information, selected tables, generated SQL, validation status, execution results, errors, retry count, and final response.
18. Add logging/debug output so I can clearly see how the agent moves through each LangGraph node during development.
19. Design the system so the LLM does not have unrestricted access to the database.
20. Keep database credentials and configuration in environment variables.

Development approach:

First, design the architecture and explain each LangGraph node, state field, edge, and routing decision.

Then create the project structure.

Then implement the minimum working version.

Do NOT build the entire advanced system at once. Build it incrementally and test each stage before moving to the next stage.

The first milestone should be:

User enters a natural-language question in the terminal
→ Agent understands the question
→ Agent identifies relevant schema
→ Agent generates SQL
→ Agent validates SQL
→ Agent executes the query
→ Agent explains the result.

After the basic version works, we will progressively add schema retrieval improvements, self-correction, caching, query optimization, evaluation, and eventually a UI.

Before writing code, provide:
1. Complete architecture
2. LangGraph node design
3. State design
4. Graph flow
5. Project folder structure
6. Technology choices
7. Development milestones
8. Then start implementation step-by-step.
