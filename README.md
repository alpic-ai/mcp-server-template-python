# mcp-server-template-python

A very simple Python template for building MCP servers using Streamable HTTP transport.

## Overview
This template provides a foundation for creating MCP servers that can communicate with AI assistants and other MCP clients. It includes a simple HTTP server implementation with example tools, resources & prompts to help you get started building your own MCP integrations.

## Prerequisites
- Install uv (https://docs.astral.sh/uv/getting-started/installation/)

## Installation

1. Clone the repository:

```bash
git clone git@github.com:alpic-ai/mcp-server-template-python.git
cd mcp-server-template-python
```

2. Install python version & dependencies:

```bash
uv python install
uv sync --locked
```

## Usage

Start the server on port 3000:

```bash
uv run main.py
```

## Running the Inspector

### Requirements
- Node.js: ^22.7.5

### Quick Start (UI mode)
To get up and running right away with the UI, just execute the following:
```bash
npx @modelcontextprotocol/inspector
```

The inspector server will start up and the UI will be accessible at http://localhost:6274.

You can test your server locally by selecting:
- Transport Type: Streamable HTTP
- URL: http://127.0.0.1:3000/mcp

## Deploy

Use the following button to deploy the server to Alpic

[![Deploy on Alpic](https://assets.alpic.ai/button.svg)](https://app.alpic.ai/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Falpic-ai%2Fmcp-server-template-python)


## Development

### Adding New Tools

To add a new tool, modify `main.py`:

```python
@mcp.tool(
    title="Your Tool Name",
    description="Tool Description for the LLM",
)
async def new_tool(
    tool_param1: str = Field(description="The description of the param1 for the LLM"), 
    tool_param2: float = Field(description="The description of the param2 for the LLM") 
)-> str:
    """The new tool underlying method"""
    result = await some_api_call(tool_param1, tool_param2)
    return result
```

### Adding New Resources

To add a new resource, modify `main.py`:

```python
@mcp.resource(
    uri="your-scheme://{param1}/{param2}",
    description="Description of what this resource provides",
    name="Your Resource Name",
)
def your_resource(param1: str, param2: str) -> str:
    """The resource template implementation"""
    # Your resource logic here
    return f"Resource content for {param1} and {param2}"
```

The URI template uses `{param_name}` syntax to define parameters that will be extracted from the resource URI and passed to your function.

### Adding New Prompts

To add a new prompt , modify `main.py`:

```python
@mcp.prompt("")
async def your_prompt(
    prompt_param: str = Field(description="The description of the param for the user")
) -> str:
    """Generate a helpful prompt"""

    return f"You are a friendly assistant, help the user and don't forget to {prompt_param}."

```
