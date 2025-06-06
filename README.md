# MCP Ollama Server

[![npm version](https://img.shields.io/npm/v/mcp-ollama.svg)](https://www.npmjs.com/package/mcp-ollama)
[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

## Build Status
[![CI Build](https://github.com/Mearman/mcp-ollama/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/Mearman/mcp-ollama/actions/workflows/ci.yml)
[![Tests](https://img.shields.io/badge/tests-passing-brightgreen)](https://github.com/Mearman/mcp-ollama/actions/workflows/ci.yml)

## Release Status
[![Release](https://github.com/Mearman/mcp-ollama/actions/workflows/semantic-release.yml/badge.svg)](https://github.com/Mearman/mcp-ollama/actions/workflows/semantic-release.yml)

A Model Context Protocol (MCP) server for integrating with [Ollama](https://ollama.ai) local LLM instances.

**Built with**: [MCP TypeScript Template](https://github.com/Mearman/mcp-template)

## Features

- 🤖 **Local LLM Integration** - Connect to your local Ollama instance
- 🚀 **TypeScript with ES Modules** - Modern JavaScript with full type safety
- 🧪 **Comprehensive Testing** - Vitest with coverage reporting
- 🔧 **Code Quality** - Biome for linting and formatting
- 📦 **Automated Publishing** - Semantic versioning and NPM publishing
- 🛠️ **Development Tools** - Hot reload, watch mode, and CLI support

## Status: In Development

This server is currently under development. When complete, it will provide tools for:

- 📋 **Model Management** - List, pull, and manage Ollama models
- 💬 **Text Generation** - Generate completions and chat responses
- 🔄 **Streaming Support** - Real-time streaming responses
- ⚙️ **Configuration** - Customizable model parameters and settings

## Planned Tools

### `list_models`
List all available models in your Ollama instance.

**Response:** Array of model objects with names, sizes, and metadata.

### `generate_completion`
Generate text completions using a specified model.

**Parameters:**
- `model` (string, required): Model name (e.g., "llama2", "codellama")
- `prompt` (string, required): Input prompt for completion
- `max_tokens` (number, optional): Maximum tokens to generate
- `temperature` (number, optional): Sampling temperature (0.0-1.0)
- `stream` (boolean, optional): Enable streaming responses

### `chat_completion`
Generate chat responses with conversation context.

**Parameters:**
- `model` (string, required): Model name
- `messages` (array, required): Array of message objects
- `max_tokens` (number, optional): Maximum tokens to generate
- `temperature` (number, optional): Sampling temperature

### `pull_model`
Download and install a new model from the Ollama library.

**Parameters:**
- `model` (string, required): Model name to download
- `insecure` (boolean, optional): Allow insecure connections

### `delete_model`
Remove a model from your local Ollama instance.

**Parameters:**
- `model` (string, required): Model name to delete

### `model_info`
Get detailed information about a specific model.

**Parameters:**
- `model` (string, required): Model name to query

## Prerequisites

- [Ollama](https://ollama.ai) installed and running locally
- Node.js 18 or higher
- At least one Ollama model installed

### Installing Ollama

Visit [https://ollama.ai](https://ollama.ai) to download and install Ollama for your platform.

After installation, pull a model:
```bash
ollama pull llama2
```

Start the Ollama service:
```bash
ollama serve
```

## Installation

### Using NPM
```bash
npm install -g mcp-ollama
```

### Using Yarn
```bash
yarn global add mcp-ollama
```

### From Source
```bash
git clone https://github.com/Mearman/mcp-ollama.git
cd mcp-ollama
yarn install
yarn build
```

## Usage

### As MCP Server

Add to your MCP client configuration:

```json
{
  "mcpServers": {
    "ollama": {
      "command": "mcp-ollama",
      "args": [],
      "env": {
        "OLLAMA_HOST": "http://localhost:11434"
      }
    }
  }
}
```

### Configuration

Configure the Ollama connection using environment variables:

- `OLLAMA_HOST`: Ollama server URL (default: `http://localhost:11434`)
- `OLLAMA_TIMEOUT`: Request timeout in milliseconds (default: `30000`)

### Development

```bash
# Start development server with hot reload
yarn dev

# Run tests
yarn test

# Run tests in watch mode
yarn test:watch

# Build the project
yarn build

# Run linting
yarn lint

# Auto-fix linting issues
yarn lint:fix
```

## Examples

### Basic Text Generation
```typescript
// Using the MCP client
const response = await mcpClient.callTool('generate_completion', {
  model: 'llama2',
  prompt: 'Explain quantum computing in simple terms',
  max_tokens: 200,
  temperature: 0.7
});
```

### Chat Conversation
```typescript
const response = await mcpClient.callTool('chat_completion', {
  model: 'llama2',
  messages: [
    { role: 'user', content: 'What is the capital of France?' },
    { role: 'assistant', content: 'The capital of France is Paris.' },
    { role: 'user', content: 'What is its population?' }
  ],
  max_tokens: 100
});
```

### Model Management
```typescript
// List available models
const models = await mcpClient.callTool('list_models', {});

// Pull a new model
await mcpClient.callTool('pull_model', {
  model: 'codellama'
});

// Get model information
const info = await mcpClient.callTool('model_info', {
  model: 'llama2'
});
```

## Development Roadmap

- [ ] Implement core Ollama API integration
- [ ] Add model management tools (list, pull, delete)
- [ ] Implement text generation tools
- [ ] Add chat completion support
- [ ] Support streaming responses
- [ ] Add comprehensive error handling
- [ ] Implement configuration validation
- [ ] Add model parameter customization
- [ ] Support for embeddings and vector operations
- [ ] Add performance monitoring and metrics

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'feat: add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## License

This project is licensed under the [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) license.

## Related Projects

- [Ollama](https://ollama.ai) - Run large language models locally
- [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [MCP Template](https://github.com/Mearman/mcp-template)