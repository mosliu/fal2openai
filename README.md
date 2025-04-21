# FAL to OpenAI API Proxy (Node.js Version)

This is a Node.js implementation of the FAL to OpenAI API proxy. It provides a compatibility layer that allows you to use FAL AI models with OpenAI-compatible API clients.

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
   ```bash
   npm install
   # or
   pnpm install
   ```

## Configuration

Set your FAL AI API key and custom API key as environment variables:

```bash
export FAL_KEY=your-fal-ai-api-key
export API_KEY=your-custom-api-key
```

You can also use a `.env` file:

```
FAL_KEY=your-fal-ai-api-key
API_KEY=your-custom-api-key
PORT=3000
```

## Usage

Start the server:

```bash
node example.js
# or
npm start
```

The server will start on port 3000 by default. You can change this by setting the `PORT` environment variable.

## Docker Support

Build and run with Docker:

```bash
docker build -t fal-proxy .
docker run -p 3000:3000 --env-file .env fal-proxy
```

Or use Docker Compose:

```bash
docker-compose up
```

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
