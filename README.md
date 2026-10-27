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

## Json model

```
import os
from dotenv import load_dotenv
from groq import Groq

load_dotenv()

client = Groq(api_key=os.getenv("GROQ_API_KEY"))

def get_weather(city):
    return f"The weather in {city} is sunny."

tools = [
    {
        "type": "function",
        "function": {
            "name": "get_weather",
            "description": "Get weather information for a city",
            "parameters": {
                "type": "object",
                "properties": {
                    "city": {
                        "type": "string",
                        "description": "Name of the city"
                    }
                },
                "required": ["city"]
            }
        }
    }
]

import json

response = client.chat.completions.create(
    model="openai/gpt-oss-20b",
    messages=[
        {
            "role": "user",
            "content": "What is the weather in Chennai?"
        }
    ],
    tools=tools,
    tool_choice="auto"
)

message = response.choices[0].message

if message.tool_calls:
    for tool_call in message.tool_calls:
        function_name = tool_call.function.name
        arguments = json.loads(tool_call.function.arguments)

        if function_name == "get_weather":
            result = get_weather(**arguments)
            print("Function result:", result)
else:
    print(message.content)
```

## init_chat_model

```
import os
from dotenv import load_dotenv
from langchain.chat_models import init_chat_model

load_dotenv()

llm = init_chat_model(
    "openai/gpt-oss-20b",
    model_provider="groq",
    api_key=os.getenv("GROQ_API_KEY"),
    temperature=0
)

from langchain_core.tools import tool

@tool
def multiply(a: int, b: int) -> int:
    """Multiply two numbers."""
    return a * b

llm_with_tools = llm.bind_tools([multiply])

response = llm_with_tools.invoke(
    "What is 10 multiplied by 20?"
)

print(response.tool_calls)

if response.tool_calls:
    for tool_call in response.tool_calls:
        if tool_call["name"] == "multiply":
            result = multiply.invoke(tool_call["args"])
            print("Function result:", result)
else:
    print(response.content)

```

## OUTPUT

<img width="717" height="265" alt="image" src="https://github.com/user-attachments/assets/b107f2af-ce0f-444d-a6dd-54d69d48c5c7" />

<img width="868" height="717" alt="image" src="https://github.com/user-attachments/assets/976f520a-edaa-42a2-a058-beb26a8150eb" />



## RESULT

Thus, a chat completion system was implemented using Groq API and LangChain's `init_chat_model`. The system demonstrates LLM tool calling, Python function execution, and JSON-based argument processing to perform mathematical calculations.
