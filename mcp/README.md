The idea is to create a MCP fully functional, follow these steps:

1. Copy the content in mcp-builder-prompt.md into a chatbot that can generate good code and replace <SPECS GO HERE> with the specifications of the MCP do want to create, you can copy the format of roll-dice-example-specs.md

2. It will generate at least 4 files and the steps to follow:
- Dockerfile
- requirements.txt
- [SERVER_NAME]_server.py example dice_server.py
- readme.txt
- CAUDE.md (if working with claude)
copy all those files in a folder, I will called dice-mcp-server

3. Build the docker images with the command:
`docker build -t dice-mcp-server .`

4. Create Custom Catalog:
`mkdir -p ~/.docker/mcp/catalogs`
`nano ~/.docker/mcp/catalogs/custom.yaml`

The content of custom.yaml is in the answer and looks similar to this:
```
version: 2
name: custom
displayName: Custom MCP Servers
registry:
  dice:
    description: "Comprehensive dice rolling for tabletop games and RPGs"
    title: "Dice Roller"
    type: server
    dateAdded: "2025-01-15T00:00:00Z"
    image: dice-mcp-server:latest
    ref: ""
    readme: ""
    toolsUrl: ""
    source: ""
    upstream: ""
    icon: ""
    tools:
      - name: flip_coin
      - name: roll_dice
      - name: roll_custom
      - name: roll_stats
      - name: roll_advantage
      - name: roll_disadvantage
      - name: roll_check
      - name: roll_initiative
    secrets: []
    metadata:
      category: productivity
      tags:
        - gaming
        - dice
        - rpg
        - dnd
        - random
      license: MIT
      owner: local
```

5. Update Registry: adding app name, in this case is dice
`nano ~/.docker/mcp/registry.yaml`
```
registry:
  # ... existing servers ...
  dice:
    ref: ""
```

6. If you are using claude desktop you can update its configuration to use the new mcp:

Find your Claude Desktop config file:

macOS: ~/Library/Application Support/Claude/claude_desktop_config.json

Windows: %APPDATA%\Claude\claude_desktop_config.json

Linux: ~/.config/Claude/claude_desktop_config.json

update the content with this:
```
{
  "mcpServers": {
    "mcp-toolkit-gateway": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v", "/var/run/docker.sock:/var/run/docker.sock",
        "-v", "[YOUR_HOME]/.docker/mcp:/mcp",
        "docker/mcp-gateway",
        "--catalog=/mcp/catalogs/docker-mcp.yaml",
        "--catalog=/mcp/catalogs/custom.yaml",
        "--config=/mcp/config.yaml",
        "--registry=/mcp/registry.yaml",
        "--tools-config=/mcp/tools.yaml",
        "--transport=stdio"
      ]
    }
  }
}
```

Replace [YOUR_HOME] with:

macOS: /Users/your_username

Windows: C:\\Users\\your_username (use double backslashes)

Linux: /home/your_username

if you don't know
in your mac you can use the command pwd to get it

7. Restart Claude Desktop and now you should have access to it

8. You can test if the mcp is working with these commands:

`docker mcp server list`

`docker run --rm dice-mcp-server`

