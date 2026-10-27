## Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

### AIM:
To design and implement a Python function for calculating the volume of a cylinder, integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).

### PROBLEM STATEMENT:
Design and implement a system where a user can input dimensions of a cylinder (radius and height),
and the system calculates its volume by invoking a Python function using the function-calling capabilities of an LLM
### DESIGN STEPS:

#### STEP 1:Import necessary libraries, including OpenAI for LLM integration and math for mathematical operations.

#### STEP 2:Define a Python function to calculate the volume of a cylinder based on its radius and height.

#### STEP 3:Integrate the function into an LLM-based chat completion system with function-calling capabilities.


## PROGRAM:
```
import os
import openai
import math
import json
from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) 
openai.api_key = os.environ['OPENAI_API_KEY']
def volume_cyclinder(radius,height):
    return math.pi*radius*radius*height
functions = [
    {
        "name": "volume_cyclinder",
        "description": "Calculate the volume of the cyclinder",
        "parameters": {
            "type": "object",
            "properties": {
                "radius":{"type":"number"},
                "height":{"type":"number"},
            },
            "required": ["radius","height"],
        },
    }
]
messages = [
    {
        "role": "user",
        "content": "calculate the volume of cyclinder with radius of 8 and height of 12"
    }
]
# Call the ChatCompletion endpoint
response = openai.ChatCompletion.create(
    model="gpt-4.1-mini",
    messages=messages,
    functions=functions
)
call = response.choices[0].message.function_call
args = json.loads(call.arguments)
result = volume_cyclinder(args["radius"], args["height"])
print("volume of the cyclinder:",round(result,2))
```
### OUTPUT:
<img width="1461" height="549" alt="image" src="https://github.com/user-attachments/assets/24e52567-9472-40cc-9579-27683c8be94c" />

### RESULT:
Hence,the python program to design and implement a Python function for calculating the volume of a cylinder,integrating it with a chat completion system utilizing the function-calling feature of a large language model (LLM) is written successfully and executed.
