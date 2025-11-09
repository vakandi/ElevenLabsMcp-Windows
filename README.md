# MAKE YOUR IDE SPEAK
# MAKE CURSOR SPEAK

![export](https://github.com/user-attachments/assets/ee379feb-348d-48e7-899c-134f7f7cd74f)

<div class="title-block" style="text-align: center;" align="center">

  [![Discord Community](https://img.shields.io/badge/discord-@elevenlabs-000000.svg?style=for-the-badge&logo=discord&labelColor=000)](https://discord.gg/elevenlabs)
  [![Twitter](https://img.shields.io/badge/Twitter-@elevenlabsio-000000.svg?style=for-the-badge&logo=twitter&labelColor=000)](https://x.com/ElevenLabsDevs)
  [![PyPI](https://img.shields.io/badge/PyPI-elevenlabs--mcp-000000.svg?style=for-the-badge&logo=pypi&labelColor=000)](https://pypi.org/project/elevenlabs-mcp)
  [![Tests](https://img.shields.io/badge/tests-passing-000000.svg?style=for-the-badge&logo=github&labelColor=000)](https://github.com/elevenlabs/elevenlabs-mcp-server/actions/workflows/test.yml)

</div>

## 🪟 Windows Fork - Enhanced for Cursor IDE

**This is a Windows-optimized fork** of the official ElevenLabs MCP server, specifically designed to work seamlessly on Windows and provide an enhanced experience with **Cursor IDE**.

### 🎤 What Makes This Fork Special?

**🔧 Windows File Path Fixes**: The **primary difference** between this fork and any other fork is that this fork **fixes critical file and directory path issues on Windows**. The original MCP server **simply did not work on Windows** when dealing with files - this fork resolves those issues completely:
- ✅ Proper Windows path handling for file operations
- ✅ Correct file saving and loading on Windows systems
- ✅ Reliable directory management for ElevenLabs audio files
- ✅ Future-proof file organization for documentation and archiving

**✨ Cursor Rules Integration**: This fork includes a `.cursorrules` file that enables Cursor AI to automatically:
- Generate speech using ElevenLabs MCP when you ask it to speak
- Play audio files using VLC in the background (no visible windows)
- Handle all audio operations seamlessly through natural language commands
- Properly manage and save all generated files on Windows

**Just ask Cursor to "speak" or "say something" and it will automatically:**
1. Generate audio using ElevenLabs text-to-speech
2. Save the file correctly on Windows (unlike the original MCP)
3. Play it using VLC in the background
4. Handle all the technical details for you

<p align="center">
  Official ElevenLabs <a href="https://github.com/modelcontextprotocol">Model Context Protocol (MCP)</a> server that enables interaction with powerful Text to Speech and audio processing APIs. This server allows MCP clients like <a href="https://www.anthropic.com/claude">Claude Desktop</a>, <a href="https://www.cursor.so">Cursor</a>, <a href="https://codeium.com/windsurf">Windsurf</a>, <a href="https://github.com/openai/openai-agents-python">OpenAI Agents</a> and others to generate speech, clone voices, transcribe audio, and more.
</p>

<!--
mcp-name: io.github.elevenlabs/elevenlabs-mcp
-->

## 🚀 Quickstart with Cursor (Windows)

### Step 1: Clone and Setup
Clone this repository and set up a virtual environment:

```powershell
git clone <your-repo-url>
cd ElevenLabsMcp
python -m venv venv
.\venv\Scripts\activate
pip install -e ".[dev]"
```

### Step 2: Get Your API Key
Get your API key from [ElevenLabs](https://elevenlabs.io/app/settings/api-keys). There is a free tier with 10k credits per month.

### Step 3: Configure Cursor MCP
1. Open Cursor Settings (or edit `%USERPROFILE%\.cursor\mcp.json` directly)
2. Add the ElevenLabs MCP server configuration pointing to your local server:

```json
{
  "mcpServers": {
    "elevenlabs": {
      "command": "C:\\path\\to\\ElevenLabsMcp\\venv\\Scripts\\python.exe",
      "args": [
        "C:\\path\\to\\ElevenLabsMcp\\elevenlabs_mcp\\server.py"
      ],
      "env": {
        "ELEVENLABS_API_KEY": "<your-api-key-here>",
        "ELEVENLABS_VOICE_ID": "<optional-voice-id>",
        "ELEVENLABS_MODEL_ID": "eleven_flash_v2",
        "ELEVENLABS_STABILITY": "0.5",
        "ELEVENLABS_SIMILARITY_BOOST": "0.75",
        "ELEVENLABS_STYLE": "0.1",
        "ELEVENLABS_API_RESIDENCY": "global",
        "ELEVENLABS_MCP_OUTPUT_MODE": "files",
        "ELEVENLABS_MCP_BASE_PATH": "C:\\path\\to\\ElevenLabsMcp\\audio"
      }
    }
  }
}
```

**Important:** 
- Replace `C:\\path\\to\\ElevenLabsMcp` with the actual path to your cloned repository
- The `ELEVENLABS_VOICE_ID` is optional - if not provided, the default voice will be used
- Adjust `ELEVENLABS_MCP_BASE_PATH` to where you want audio files saved (defaults to `audio` folder in the project)
- All environment variables are optional except `ELEVENLABS_API_KEY`

### Step 4: Copy the Cursor Rules
The `.cursorrules` file in this repository contains pre-configured rules that make Cursor automatically use ElevenLabs MCP for speech generation and VLC for playback. Simply copy the `.cursorrules` file to your project root, or ensure it's in your workspace.

### Step 5: Restart Cursor
After configuring the MCP server, **restart Cursor** to load the new MCP configuration.

**That's it!** Now you can simply ask Cursor:
- "Speak this: Hello, world!"
- "Say something about artificial intelligence"
- "Read this text aloud: [your text]"
- "Say hi to me"

Cursor will automatically generate the audio using ElevenLabs MCP and play it using VLC in the background.

## 🎯 Quickstart with Claude Desktop (Windows)

1. Get your API key from [ElevenLabs](https://elevenlabs.io/app/settings/api-keys).
2. Install `uv` (Python package manager). For Windows, see the `uv` [repo](https://github.com/astral-sh/uv) for installation methods.
3. **Enable Developer Mode** in Claude Desktop: Click "Help" in the hamburger menu at the top left and select "Enable Developer Mode".
4. Go to Claude > Settings > Developer > Edit Config > `claude_desktop_config.json` to include the following:

```json
{
  "mcpServers": {
    "ElevenLabs": {
      "command": "uvx",
      "args": ["elevenlabs-mcp"],
      "env": {
        "ELEVENLABS_API_KEY": "<insert-your-api-key-here>"
      }
    }
  }
}
```

## 📋 Alternative: Using Published Package (Other MCP Clients)

If you prefer to use the published package instead of running from source (for other clients like Windsurf):

1. Install the package: `pip install elevenlabs-mcp`
2. Run: `python -m elevenlabs_mcp --api-key={{PUT_YOUR_API_KEY_HERE}} --print` to get the configuration
3. Paste it into the appropriate configuration directory specified by your MCP client

**Note:** For Cursor on Windows, we recommend using the local server setup (see Quickstart above) for better control and customization.

## 💬 Example Usage

⚠️ Warning: ElevenLabs credits are needed to use these tools.

Try asking your AI assistant:

- "Create an AI agent that speaks like a film noir detective and can answer questions about classic movies"
- "Generate three voice variations for a wise, ancient dragon character, then I will choose my favorite voice to add to my voice library"
- "Convert this recording of my voice to sound like a medieval knight"
- "Create a soundscape of a thunderstorm in a dense jungle with animals reacting to the weather"
- "Turn this speech into text, identify different speakers, then convert it back using unique voices for each person"
- **"Speak this text: [your text here]"** (Cursor will automatically use ElevenLabs + VLC)

## 🔧 Optional Features

### File Output Configuration

**✅ Windows-Compatible File Handling**: Unlike the original MCP, this fork properly handles all file operations on Windows. All file paths, directory creation, and file saving work correctly on Windows systems.

You can configure how the MCP server handles file outputs using these environment variables in your configuration:

- **`ELEVENLABS_MCP_BASE_PATH`**: Specify the base path for file operations with relative paths (default: `~/Desktop`). **Works correctly on Windows with proper path handling.**
- **`ELEVENLABS_MCP_OUTPUT_MODE`**: Control how generated files are returned (default: `files`). **All modes work reliably on Windows.**

#### Output Modes

The `ELEVENLABS_MCP_OUTPUT_MODE` environment variable supports three modes:

1. **`files`** (default): Save files to disk and return file paths
   ```json
   "env": {
     "ELEVENLABS_API_KEY": "your-api-key",
     "ELEVENLABS_MCP_OUTPUT_MODE": "files"
   }
   ```

2. **`resources`**: Return files as MCP resources; binary data is base64-encoded, text is returned as UTF-8 text
   ```json
   "env": {
     "ELEVENLABS_API_KEY": "your-api-key",
     "ELEVENLABS_MCP_OUTPUT_MODE": "resources"
   }
   ```

3. **`both`**: Save files to disk AND return as MCP resources
   ```json
   "env": {
     "ELEVENLABS_API_KEY": "your-api-key",
     "ELEVENLABS_MCP_OUTPUT_MODE": "both"
   }
   ```

**Resource Mode Benefits:**
- Files are returned directly in the MCP response as base64-encoded data
- No disk I/O required - useful for containerized or serverless environments
- MCP clients can access file content immediately without file system access
- In `both` mode, resources can be fetched later using the `elevenlabs://filename` URI pattern

**Use Cases:**
- `files`: Traditional file-based workflows, local development
- `resources`: Cloud environments, MCP clients without file system access
- `both`: Maximum flexibility, caching, and resource sharing scenarios

### Data residency keys

You can specify the data residency region with the `ELEVENLABS_API_RESIDENCY` environment variable. Defaults to `"us"`.

**Note:** Data residency is an enterprise only feature. See [the docs](https://elevenlabs.io/docs/product-guides/administration/data-residency#overview) for more details.

## 🛠️ Contributing

If you want to contribute or run from source:

1. Clone the repository:

```powershell
git clone https://github.com/elevenlabs/elevenlabs-mcp
cd elevenlabs-mcp
```

2. Create a virtual environment and install dependencies:

```powershell
python -m venv venv
.\venv\Scripts\activate
pip install -e ".[dev]"
```

3. Copy `.env.example` to `.env` and add your ElevenLabs API key:

```powershell
copy .env.example .env
# Edit .env and add your API key
```

4. Run the tests to make sure everything is working:

```powershell
pytest tests/
```

5. Install the server in Claude Desktop: `mcp install elevenlabs_mcp/server.py`

6. Debug and test locally with MCP Inspector: `mcp dev elevenlabs_mcp/server.py`

## 🎧 VLC Setup (For Audio Playback)

The `.cursorrules` file automatically uses VLC for background audio playback. To ensure it works:

1. **Install VLC Media Player** from [videolan.org](https://www.videolan.org/vlc/)
2. The rules will automatically detect VLC in these locations:
   - `C:\Program Files\VideoLAN\VLC\vlc.exe`
   - `C:\Program Files (x86)\VideoLAN\VLC\vlc.exe`
   - Or if VLC is in your system PATH

If VLC is installed in a different location, the AI will ask you for the path when needed.

## 🔍 Why This Fork Exists

### Windows File Path Issues - SOLVED

The original ElevenLabs MCP server had **critical file path handling issues on Windows** that made it unusable:

- ❌ **Original MCP**: File paths using Unix-style separators (`/`) that failed on Windows
- ❌ **Original MCP**: Directory creation and file saving errors on Windows
- ❌ **Original MCP**: Inability to properly manage audio files for documentation
- ❌ **Original MCP**: Path resolution issues causing file operations to fail silently

**✅ This Fork Fixes All Of That:**
- ✅ Proper Windows path handling with correct separators (`\`)
- ✅ Reliable file saving and directory management
- ✅ Correct path resolution for all Windows file operations
- ✅ Proper handling of audio files for future documentation and archiving
- ✅ Full compatibility with Windows file system operations

**This is why this fork is essential for Windows users** - the original simply doesn't work correctly with files on Windows systems.

## 🐛 Troubleshooting

### Windows-Specific Issues

**Logs when running with Claude Desktop:**
- **Windows**: `%APPDATA%\Claude\logs\mcp-server-elevenlabs.log`

### Timeouts when using certain tools

Certain ElevenLabs API operations, like voice design and audio isolation, can take a long time to resolve. When using the MCP inspector in dev mode, you might get timeout errors despite the tool completing its intended task.

This shouldn't occur when using a client like Claude or Cursor.

### MCP ElevenLabs: spawn uvx ENOENT

If you encounter the error "MCP ElevenLabs: spawn uvx ENOENT", confirm its absolute path by running this command in PowerShell:

```powershell
Get-Command uvx
```

Once you obtain the absolute path (e.g., `C:\Users\YourName\AppData\Local\Programs\uv\uvx.exe`), update your configuration to use that path (e.g., `"command": "C:\\Users\\YourName\\AppData\\Local\\Programs\\uv\\uvx.exe"`). This ensures that the correct executable is referenced.

### VLC Not Found

If the AI cannot find VLC:
1. Make sure VLC is installed
2. If installed in a custom location, provide the path to `vlc.exe` when prompted
3. Alternatively, add VLC to your system PATH for automatic detection

## 📄 License

See [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

This is a Windows-optimized fork of the official [ElevenLabs MCP Server](https://github.com/elevenlabs/elevenlabs-mcp-server). Special thanks to the ElevenLabs team for creating this amazing MCP server.

---

**Make your IDE speak. Make Cursor speak. Experience the future of AI-powered development.**
