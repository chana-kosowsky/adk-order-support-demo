# Amazon Support Agent Demo

A lightweight customer support agent built with Google ADK that demonstrates tool calling, ReAct-style reasoning, and context engineering for order tracking requests.

## What this project demonstrates

- ReAct-style reasoning loop
- Tool selection based on user intent and available schema
- Mock order lookup using realistic sample data
- Context engineering so the model sees only relevant tracking details
- Structured JSON responses that match a strict output contract

## Why this project is useful

This project is a simple but practical example of how an LLM agent can be connected to a tool and grounded in a narrow, relevant context instead of guessing or hallucinating answers.

It is designed to showcase:

- tool calling
- function-based orchestration
- controlled output structure
- safe handling when required context is missing

## Project structure

```text
.
├── amazon_support/
│   ├── __init__.py
│   ├── agent.py
│   └── mock_data.py
├── .env
├── .gitignore
├── requirements.txt
├── README.md
└── try.py
```

## How it works

The agent receives a conversational customer request such as:

> "I am furious! Where is order 12345?!"

It then:

1. Recognizes that the user needs order tracking information.
2. Calls the `get_order_status` tool with the order ID.
3. Receives only the relevant data returned by the mock backend.
4. Produces a structured JSON response using the configured schema.

## Example mock data

The mock backend includes a few sample orders such as:

```python
MOCK_ORDERS = {
    "12345": {
        "status": "Delayed in transit",
        "reason": "Severe weather event in East Coast hub",
        "new_expected_delivery": "Thursday, Oct 12"
    },
    "98765": {
        "status": "Delivered",
        "reason": "Left at front porch",
        "new_expected_delivery": "None"
    }
}
```

## Example response

```json
{
  "request_type": "delay",
  "customer_sentiment": "angry",
  "requires_human_escalation": false,
  "response_message": "I sincerely apologize for the frustration. I have checked on order 12345, and it is currently delayed in transit due to a severe weather event at our East Coast hub. The new expected delivery date is Thursday, Oct 12."
}
```

## Run locally

1. Create and activate a virtual environment.
2. Install the dependencies:

```bash
pip install -r requirements.txt
```

3. Start the ADK web app:

```bash
adk web --port 9000
```

4. Open the local web UI and try prompts such as:

- "Where is my order 12345?"
- "Can you check on my order? I don't remember the number."
- "I am furious! Where is order 12345?!"

## Current limitations

- This is a mock demo and not connected to a real Amazon backend.
- There is no real authentication or customer account system.
- Data is static and intentionally simplified for demonstration purposes.
- The project is designed to illustrate agent orchestration and tool use, not production e-commerce infrastructure.

## Future improvements

- Connect to a real order API or database
- Add more tools for returns, refunds, and shipping
- Add authentication and authorization
- Expand the mock data set for more realistic scenarios
- Improve UI and observability for demo use

## License

This project is intended for educational and portfolio/demo purposes.
