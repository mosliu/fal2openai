# FAL to OpenAI API Proxy (Python Version)

This is a Python implementation of the FAL to OpenAI API proxy. It provides a compatibility layer that allows you to use FAL AI models with OpenAI-compatible API clients.

## Features

- Supports all FAL AI models
- Implements OpenAI-compatible endpoints:
  - GET `/v1/models` - Lists available models
  - POST `/v1/chat/completions` - Handles chat completions
- Supports both streaming and non-streaming responses
- Implements the "System Top + Separator + Recency" message handling strategy
- Handles error cases gracefully

## Installation

1. Clone this repository
2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

## Configuration

Set your FAL AI API key as an environment variable:

```bash
export FAL_KEY=your-fal-ai-api-key
```

You can also use a `.env` file with python-dotenv:

```
FAL_KEY=your-fal-ai-api-key
PORT=3000
```

## Usage

Start the server:

```bash
python example.py
```

The server will start on port 3000 by default. You can change this by setting the `PORT` environment variable.

## API Endpoints

### GET `/v1/models`

Returns a list of available models in OpenAI format.

### POST `/v1/chat/completions`

Accepts chat completion requests in OpenAI format and forwards them to FAL AI.

Parameters:
- `model`: The model to use (e.g., "anthropic/claude-3.7-sonnet")
- `messages`: An array of message objects with `role` and `content`
- `stream`: (Optional) Whether to stream the response (default: false)
- `reasoning`: (Optional) Whether to include reasoning in the response (default: false)

## Message Handling Strategy

This implementation uses the "System Top + Separator + Recency" strategy:

1. System messages are prioritized and placed at the top
2. A separator is added between system messages and older conversation history
3. Recent messages are included in the prompt, with older messages in the system prompt

This ensures that the most important context is preserved while maintaining the most recent conversation history.
