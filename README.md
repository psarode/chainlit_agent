# Chainlit Starter App

This project is a starter Chainlit application that demonstrates a simple integration with OpenAI's API. It showcases the following key features:

1. **OpenAI Integration**: The app is connected to OpenAI's API, allowing it to leverage state-of-the-art language models for generating responses.

2. **Streaming Responses**: Instead of waiting for the entire response to be generated, the app streams the AI's response in real-time, providing a more interactive and engaging user experience.

3. **Chat History**: The application maintains a conversation history, enabling context-aware responses and allowing for more coherent and meaningful interactions.

4. **Environment Variable Management**: Sensitive information like API keys are managed securely using environment variables.

5. **LangSmith Integration**: The app includes LangSmith for tracing and monitoring AI interactions, which can be useful for debugging and optimizing your AI application.

As a convenience, on start of a new chat session, a system prompt is added as the first message in the chat history.

## Getting Started

### 1. Create a virtual environment

First, create a virtual environment to isolate the project dependencies:
```bash
python -m venv .venv
```

### 2. Activate the virtual environment:

- On Windows:
  ```bash
  .venv\Scripts\activate
  ```
- On macOS and Linux:
  ```bash
  source .venv/bin/activate
  ```

### 3. Install dependencies

Install the project dependencies from the `requirements.txt` file:

```bash
pip install -r requirements.txt
```

### 4. Set up environment variables

- Copy the `.env.sample` file to a new file named `.env`
- Fill in the `.env` file with your API keys

## Running the app

To run the app, use the following command:

```bash
chainlit run app.py -w
``` 

## Updating dependencies

If you need to update the project dependencies, follow these steps:

1. Update the `requirements.in` file with the new package or version.

2. Install `pip-tools` if you haven't already:
   ```bash
   pip install pip-tools
   ```

3. Compile the new `requirements.txt` file:
   ```bash
   pip-compile requirements.in
   ```

4. Install the updated dependencies:
   ```bash
   pip install -r requirements.txt
   ```

This process ensures that all dependencies are properly resolved and pinned to specific versions for reproducibility.


The current code in base_agent.py is implementing a base Agent class with an asynchronous execute method. Here's a breakdown of what the code is doing:
Class Definition:
Defines a base Agent class with a class attribute tools that includes a function definition for updateArtifact.
Initialization:
The __init__ method sets up the agent with a name, client, prompt, and generation parameters.
Execute Method:
The execute method is the main functionality of the agent. It processes a message history and generates a response.
Message History Preparation:
Copies the input message history and ensures the system prompt is set correctly.
Response Generation:
Creates a streaming completion request to the AI model (likely GPT-4) with the prepared message history and tools.
Streaming and Processing:
Asynchronously streams the response, handling both regular content and potential tool calls.
For regular content, it streams tokens to a Chainlit message.
For tool calls, it accumulates the function name and arguments.
Tool Call Handling:
If a tool call is detected (specifically for updateArtifact):
It parses the arguments.
Creates an "artifacts" directory if it doesn't exist.
Writes the provided content to a file in the artifacts directory.
Adds a system message to the history about the artifact update.
Generates an additional response acknowledging the artifact update.
Debugging:
Includes debug print statements to log information about function calls.
Response Finalization:
Updates the Chainlit message with the full response.
Returns the content of the response.
The code is designed to work with an AI model that can make function calls (tool use) and handle streaming responses. It's integrated with Chainlit for real-time message updates in a chat interface. The specific tool implemented (updateArtifact) allows the AI to create or update files with HTML, CSS, or Markdown content.
