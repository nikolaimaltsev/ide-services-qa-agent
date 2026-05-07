- Put into .claude/skills/ide-services-qa/SKILL.md and ask claude to use the skill.
- This is tested on Linux(x11)
- Mac and Windows has their own computer use tool, which seem to be more precise. You may want to instuct claude to use it for UI interaction part
- You might need to install Youtrack and Notion MCPs manually.
- WIP

How to install mcp-steroid (https://github.com/JetBrains/mcp-steroid):

1. From Settings → Plugins → Marketplace search for MCP Steroid, or install from plugins.jetbrains.com/plugin/30019-mcp-steroid. 
2. Start the IDE; the plugin writes .idea/mcp-steroid.md with the server URL + ready-to-paste MCP config for agents. 
3. claude mcp add --transport http mcp-steroid http://127.0.0.1:6315/mcp
4. start claude, /mcp, mcp-steroid/connect
