# EX 01 - Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling
## NAME: MANOJ KUMAR N
## REG NO : 212225230168


## AIM:
To develop a Python program that calculates the volume of a cylinder using its radius and height. The program uses the OpenAI API and function calling to identify the user's request, execute the mathematical function, and return the calculated result through the chat completion system.

## DESIGN STEPS:

### STEP 1:
Import the required libraries, such as `math` and `OpenAI`, and initialize the OpenAI client.

### STEP 2:
Define a Python function named `cylinder_volume()` that accepts the radius and height as arguments and calculates the volume using the formula:

V = π × radius² × height

### STEP 3:
Define the function schema and provide it to the chat completion system. When the LLM identifies a request to calculate the cylinder's volume, it calls the Python function with the required arguments and returns the calculated result to the user.

## PROGRAM:

```
import math
from openai import OpenAI
import json

client = OpenAI()

def cylinder_volume(radius, height):
    return math.pi * radius * radius * height

tools = [{
    "type": "function",
    "name": "cylinder_volume",
    "description": "Calculate the volume of a cylinder",
    "parameters": {
        "type": "object",
        "properties": {
            "radius": {
                "type": "number",
                "description": "Radius of the cylinder"
            },
            "height": {
                "type": "number",
                "description": "Height of the cylinder"
            }
        },
        "required": ["radius", "height"],
        "additionalProperties": False
    },
    "strict": True
}]

response = client.responses.create(
    model="gpt-4.1",
    input="Calculate the volume of a cylinder with radius 5 and height 10.",
    tools=tools
)

for item in response.output:
    if item.type == "function_call":
        args = json.loads(item.arguments)
        result = cylinder_volume(
            args["radius"],
            args["height"]
        )
        print("Volume of cylinder:", result)
```

## OUTPUT:
<img width="1261" height="661" alt="Screenshot 2026-10-27 223550" src="https://github.com/user-attachments/assets/22cd1e60-4933-4459-b95d-d49b0dc12274" />


## RESULT:
Thus, a Python function for calculating the volume of a cylinder was implemented and successfully integrated with an LLM chat completion system using function calling.
