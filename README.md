# Supabase MCP Server

A Model Context Protocol (MCP) server that enables AI tools to interact with Supabase databases. This server provides tools for reading, creating, updating, and deleting records in Supabase tables.

## Features

- Read rows from any Supabase table with filtering and column selection
- Create single or multiple records in tables
- Update records based on filter conditions
- Delete records based on filter conditions
- Comprehensive tool descriptions for AI model understanding
- Type-safe request/response handling with Pydantic

## Prerequisites

- Python 3.9+
- Supabase project with service role key
- FastMCP-compatible AI tool (e.g., Cursor)

## Installation

1. Clone the repository:

```bash
git clone https://github.com/yourusername/supabase-mcp.git
cd supabase-mcp
```

2. Create and activate a virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Set up environment variables:

```bash
export SUPABASE_URL="your-project-url"
export SUPABASE_KEY="your-service-role-key"
```

## Usage

1. Start the MCP server:

```bash
python src/server/supabase_mcp.py
```

2. Configure your AI tool to use the MCP server:

```json
{
  "mcpServers": {
    "supabase": {
      "command": "python",
      "args": ["src/server/supabase_mcp.py"]
    }
  }
}
```

## Available Tools

### read_rows

Read rows from a Supabase table with optional filtering and column selection.

Example usage:

```json
{
  "table_name": "users",
  "columns": ["id", "name"],
  "filters": { "age": { "gt": 18 } },
  "limit": 10
}
```

### create_records

Create one or more records in a Supabase table.

Example usage:

```json
{
  "table_name": "users",
  "records": [
    { "name": "John", "age": 30 },
    { "name": "Jane", "age": 25 }
  ]
}
```

### update_records

Update records in a Supabase table based on filter conditions.

Example usage:

```json
{
  "table_name": "users",
  "filters": { "status": "inactive" },
  "updates": { "status": "active" }
}
```

### delete_records

Delete records from a Supabase table based on filter conditions.

Example usage:

```json
{
  "table_name": "users",
  "filters": { "id": 1 }
}
```

## Security Considerations

- Always use the service role key in a secure environment
- Never expose the service role key in client-side code
- Use appropriate row-level security policies in Supabase
- Consider implementing rate limiting for production use

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT
