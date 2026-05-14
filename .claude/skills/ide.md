# IDE Interaction

*If GUI interaction is required, read `.claude/skills/computer-use.md` first*

**Prefer keyboard over menus:**

- Find Action: `Ctrl+Shift+A` — trigger any action by name
- Settings: `Ctrl+Alt+S`

**Prefer direct file edits over IDE GUI for VM options and log config**

| Config               | Path                                                              |
| -------------------- | ----------------------------------------------------------------- |
| VM options           | `~/.config/JetBrains/<ProductVersion>/idea64.vmoptions`           |
| Debug log categories | `~/.config/JetBrains/<ProductVersion>/options/log-categories.xml` |

**Finding an IDEA installation** — if not under the standard Toolbox path, search broadly:

```
find ~ -name "product-info.json" 2>/dev/null | xargs grep -l "IntelliJIdea"
```

**Isolating the current session in idea.log** — the log accumulates across restarts:

```
grep -n "AppStarter.*JVM options" idea.log | tail -1   # get line N
tail -n +N idea.log | grep <pattern>
```

**IntelliJ IDEA docs:** https://www.jetbrains.com/help/idea/getting-started.html
