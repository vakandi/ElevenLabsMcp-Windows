# ElevenLabs MCP Server - Windows Setup Guide

This guide explains how to set up and use the local ElevenLabs MCP server on Windows.

## Overview

This is a modified version of the ElevenLabs MCP server that fixes Windows path handling issues. The server will automatically use the `audio` directory in the project root for saving generated audio files.

## Prerequisites

1. Python 3.11 or higher
2. ElevenLabs API key (get one from https://elevenlabs.io/app/settings/api-keys)
3. Cursor IDE with MCP support

## Installation

1. Navigate to the `elevenlabs-mcp` directory:
   ```powershell
   cd elevenlabs-mcp
   ```

2. Create a virtual environment:
   ```powershell
   python -m venv venv
   ```

3. Activate the virtual environment:
   ```powershell
   venv\Scripts\activate
   ```

4. Install dependencies:
   ```powershell
   pip install -e ".[dev]"
   ```

5. Create a `.env` file in the `elevenlabs-mcp` directory (optional, if you want to set API key here):
   ```
   ELEVENLABS_API_KEY=your-api-key-here
   ELEVENLABS_MCP_BASE_PATH=C:\Users\vakandi\Documents\projects\AdForgeMain\audio
   ```

## Configuration for Cursor

### Option 1: Using the configuration generator

Run the configuration generator:
```powershell
python -m elevenlabs_mcp --print --api-key YOUR_API_KEY
```

This will print a configuration that you can add to Cursor's MCP settings.

### Option 2: Manual configuration

1. Find Cursor's MCP configuration file. It's typically located at:
   - `%APPDATA%\Cursor\User\globalStorage\` (check for MCP-related JSON files)

2. Add the following configuration:
   ```json
   {
     "mcpServers": {
       "ElevenLabs": {
         "command": "C:\\Users\\vakandi\\Documents\\projects\\AdForgeMain\\elevenlabs-mcp\\venv\\Scripts\\python.exe",
         "args": [
           "-m",
           "elevenlabs_mcp.server"
         ],
         "env": {
           "ELEVENLABS_API_KEY": "your-api-key-here",
           "ELEVENLABS_MCP_BASE_PATH": "C:\\Users\\vakandi\\Documents\\projects\\AdForgeMain\\audio"
         }
       }
     }
   }
   ```

   **Note:** Replace:
   - `C:\\Users\\vakandi\\Documents\\projects\\AdForgeMain\\elevenlabs-mcp\\venv\\Scripts\\python.exe` with your actual Python path
   - `your-api-key-here` with your actual ElevenLabs API key
   - The base path if you want to use a different directory

## Testing

1. Make sure the virtual environment is activated
2. Test the server directly:
   ```powershell
   python -m elevenlabs_mcp.server
   ```

3. In Cursor, try using the MCP tools to generate audio:
   - "Generate audio saying 'hello world'"
   - The audio file should be saved to the `audio` directory in the project root

## Troubleshooting

### Error: "Directory is not writeable"
- Make sure the `audio` directory exists in the project root
- Check that you have write permissions to the directory
- Try running Cursor as administrator (not recommended, but can help diagnose permission issues)

### Error: "Failed to create directory"
- Check that the path doesn't contain invalid characters
- Make sure the parent directory exists
- Try setting `ELEVENLABS_MCP_BASE_PATH` to a simpler path like `C:\Users\YourName\Documents\audio`

### Audio files not appearing
- Check the `audio` directory in the project root
- Check Cursor's MCP logs for errors
- Verify that the API key is correct and has credits

## Windows-Specific Improvements

This version includes the following Windows-specific fixes:

1. **Better path handling**: Uses `Path.resolve()` to handle Windows path formats correctly
2. **Fallback directories**: If Desktop doesn't exist, falls back to Documents/audio or temp directory
3. **Error handling**: Better error messages for Windows-specific path issues
4. **Directory creation**: Ensures directories are created with proper permissions on Windows

## Output Directory

By default, audio files are saved to:
- `C:\Users\vakandi\Documents\projects\AdForgeMain\audio` (when running from this project)

You can override this by setting the `ELEVENLABS_MCP_BASE_PATH` environment variable.

## Additional Configuration

### Output Modes

You can control how files are returned by setting `ELEVENLABS_MCP_OUTPUT_MODE`:

- `files` (default): Save files to disk and return file paths
- `resources`: Return files as base64-encoded MCP resources
- `both`: Save files to disk AND return as MCP resources

Example:
```json
"env": {
  "ELEVENLABS_API_KEY": "your-api-key",
  "ELEVENLABS_MCP_BASE_PATH": "C:\\path\\to\\audio",
  "ELEVENLABS_MCP_OUTPUT_MODE": "files"
}
```

## Support

For issues specific to this Windows version, check the modifications made to:
- `elevenlabs_mcp/utils.py` - Path handling improvements
- `elevenlabs_mcp/server.py` - Default path detection
- `elevenlabs_mcp/__main__.py` - Configuration generation

For general ElevenLabs MCP issues, refer to the original repository: https://github.com/elevenlabs/elevenlabs-mcp

