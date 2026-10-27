## Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

### AIM:
To design and implement a Python function for calculating the volume of a cylinder, integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).

### PROBLEM STATEMENT:

### DESIGN STEPS:

#### STEP 1:Import the required libraries

#### STEP 2:Define the function to calculate the volume of the cyclinder.The formula to calculate the volume of the cyclinder is Pi*radius**2*height.

#### STEP 3:

### PROGRAM:
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
<img width="1089" height="162" alt="image" src="https://github.com/user-attachments/assets/470ec947-fcd1-4806-ac79-06ed0c423de9" />

### RESULT:
Thus ,the above program to calculate the volume of the cyclinder executed successfully.
