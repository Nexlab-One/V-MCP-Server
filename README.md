# V MCP Server

A Model Context Protocol (MCP) server that provides comprehensive V programming language support for Cursor IDE and other MCP-compatible editors.

## Overview

This MCP server enhances V development by providing:

- Instant access to V documentation without leaving your editor
- 300+ code examples for common patterns and use cases
- Smart search through documentation and examples
- Fast responses through intelligent caching
- Clear error messages and troubleshooting guidance

## Features for V Developers

The server is designed to improve the V development workflow:

- Quick syntax lookups while coding
- Example code for common patterns
- Standard library exploration without context switching
- Syntax explanations with practical examples
- Performance optimizations through smart caching

## Quick Setup

### Prerequisites
- Python 3.10+
- V repository (you're already here!)

### Install Dependencies
```bash
cd v-mcp-server
pip install -r requirements.txt
```

### Start the Server
```bash
python main.py
```

The server is now running and ready to use.

## Available Tools

### Documentation & Learning
- **`get_v_documentation()`** - Browse V language documentation
- **`explain_v_syntax(feature)`** - Learn specific V language features
- **`get_v_quick_reference()`** - Quick V syntax reference

### Code Examples
- **`list_v_examples()`** - Browse available code examples
- **`get_v_example(name)`** - Get complete example source code
- **`search_v_examples(query)`** - Find examples by pattern

### Standard Library
- **`list_v_stdlib_modules()`** - Explore V's standard library
- **`get_v_module_info(module)`** - Detailed module information

### Search & Discovery
- **`search_v_docs(query)`** - Search documentation
- **`get_v_config()`** - View server configuration
- **`clear_v_cache()`** - Refresh cached content

## Configuration

Customize the server with environment variables:

```bash
export V_CACHE_TTL_SECONDS=300      # Cache lifetime (default: 300s)
export V_MAX_SEARCH_RESULTS=50      # Max search results (default: 50)
export V_LOG_LEVEL=INFO             # Logging level (default: INFO)
```

## Cursor IDE Integration

To use the V MCP server with Cursor IDE, add the following configuration to your Cursor MCP settings:

### MCP Configuration

Add this to your `.cursor/mcp.json` file:

```json
{
  "mcpServers": {
    "v-language-assistant": {
      "command": "python",
      "args": [
        "/path/to/v-mcp/v-mcp-server/main.py"
      ],
      "env": {
        "V_REPO_PATH": "/path/to/v-mcp"
      }
    }
  }
}
```

Replace `/path/to/v-mcp` with the actual path to your V MCP directory.

### Usage

Once configured, you can ask questions like:

- "How do I work with arrays in V?"
- "Show me V struct examples"
- "What modules are in V's standard library?"
- "Explain V error handling"

## Performance Features

- Smart caching for frequently accessed content
- Relevance scoring for better search results
- Graceful degradation when parts of V repository are missing
- Configurable performance limits

## Troubleshooting

### Server Not Starting?
```bash
# Check Python version
python --version  # Should be 3.10+

# Verify dependencies
cd v-mcp-server
python -m pip install -r requirements.txt

# Test server
python main.py
```

### Missing Documentation?
- Ensure you're in the V repository root
- Check that `doc/`, `examples/`, and `vlib/` directories exist
- Set `V_REPO_PATH` if running from different location

### Slow Performance?
- Increase cache TTL: `export V_CACHE_TTL_SECONDS=600`
- Clear cache: Use `clear_v_cache()` tool
- Restart server to refresh all content

## Next Steps

Once configured, you can start using the V MCP server immediately. Try asking questions like:

- "What are the basic data types in V?"
- "Show me how to create a struct"
- "How do I handle errors in V?"
- "What functions are available in the os module?"

For detailed documentation and advanced configuration options, see [v-mcp-server/README.md](v-mcp-server/README.md).