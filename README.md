# SQL Query Generator API

## Overview

This project provides an API for generating SQL queries using LangChain's LLMChain and an Ollama LLM model. The API takes natural language questions as input and returns a valid SQL query based on a predefined schema and menu mappings.

## Features

- Uses **LangChain** to generate SQL queries.
- **Ollama LLM** for natural language processing.
- **FastAPI** for serving the API.
- **Date placeholders** automatically injected into queries.
- **Customizable prompt templates**.

## Installation

### Prerequisites

Ensure you have Python installed (>=3.8) and required dependencies:

```sh
pip install fastapi pydantic langchain langchain_community ollama
```

### Running the API

1. Clone the repository:

```sh
git clone <your-repo-url>
cd <your-project-directory>
```

2. Ensure that the following files exist in the project directory:

   - `schema.sql` (Contains the database schema)
   - `menu_mappings.txt` (Contains menu mapping information)
   - `prompt_template2.txt` (Contains the prompt template)

3. Start the FastAPI server:

```sh
uvicorn main:app --reload
```

## API Endpoints

### Generate SQL Query

**Endpoint:**

```
POST /generate_sql/
```

**Request Body:**

```json
{
  "question": "In which area is the biggest sales this month?"
}
```

**Response:**

```json
{
  "sql_query": "SELECT area, SUM(sales) as total_sales FROM sales_table WHERE sale_date BETWEEN '2024-03-01' AND '2024-03-31' GROUP BY area ORDER BY total_sales DESC LIMIT 1;"
}
```

## Code Structure

- **`get_date_placeholders()`**: Generates date placeholders for the SQL query.
- **`generate_sql_query(question)`**: Uses LangChain to generate an SQL query based on the schema, menu mappings, and question.
- **FastAPI Endpoint (`/generate_sql/`)**: Exposes the SQL generation function as an API.

## Customization

- **Change the LLM model**: Modify `model="llama3.2:3b"` in the `Ollama` instance.
- **Modify prompt template**: Update `prompt_template2.txt`.
- **Extend date placeholders**: Modify `get_date_placeholders()`.
