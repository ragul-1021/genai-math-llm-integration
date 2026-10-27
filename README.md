# Integration of Mathematical Calculations with a Chat Completion System Using LLM Function Calling

## AIM

To implement mathematical calculations using Python and integrate them with a Large Language Model (LLM) chat completion system using tool calling with Groq API and LangChain's `init_chat_model`.

## PROBLEM STATEMENT

To develop a chat completion system that uses an LLM to identify mathematical operations, invoke the appropriate Python function through tool calling, process function arguments in JSON format, and return the calculated result to the user.

## DESIGN STEPS

### STEP 1: Initialize the Chat Model

- Install the required Python libraries.
- Configure the Groq API key using a `.env` file.
- Initialize the LLM using LangChain's `init_chat_model`.
- Configure the model to process user queries.

### STEP 2: Define and Bind the Tool

- Define a Python function to perform the required mathematical calculation.
- Register the function using LangChain's `@tool` decorator.
- Bind the tool to the language model using `bind_tools()`.
- Send the mathematical query to the model.

### STEP 3: Process Tool Calls Using JSON

- Receive the tool-call response from the LLM.
- Extract the function name and arguments.
- Process the arguments in JSON format.
- Execute the corresponding Python function.
- Display the calculated result.

## PROGRAM

The program is implemented in a Jupyter Notebook using Python, Groq API, LangChain, and JSON for handling tool-call arguments.

The implementation includes:
- LLM initialization using `init_chat_model()`
- Tool definition using `@tool`
- Tool binding using `bind_tools()`
- JSON-based argument handling
- Execution of the selected mathematical function

Refer to the Jupyter Notebook (`.ipynb`) in this repository for the complete source code.

## OUTPUT

<img width="717" height="265" alt="image" src="https://github.com/user-attachments/assets/b107f2af-ce0f-444d-a6dd-54d69d48c5c7" />

<img width="868" height="717" alt="image" src="https://github.com/user-attachments/assets/976f520a-edaa-42a2-a058-beb26a8150eb" />



## RESULT

Thus, a chat completion system was implemented using Groq API and LangChain's `init_chat_model`. The system demonstrates LLM tool calling, Python function execution, and JSON-based argument processing to perform mathematical calculations.
