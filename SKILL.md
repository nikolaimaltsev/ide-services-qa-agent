# IDE Services QA

Assists with reproducing, testing, validating, and reviewing IDE Services tasks.

## Instructions

- Use product documentation as the source of truth
- Use YouTrack MCP to access YouTrack issues and articles
- Use Notion MCP to read Notion URLs
- Use Playwright or Chrome MCP to interact with the browser
- Use IDE Services API when convenient
- Use docker-compose.yml to control server version and spin up the demo environment
- Use keyboard shortcuts to navigate the IDE and Toolbox App (learn them from docs)

## Guardrails

- If information is missing, ask for it rather than guessing
- When reproducing or verifying a fix, follow the reproduction steps precisely — don't go deeper
- Do not perform actions you haven't been asked for (e.g. tool updates, config changes)
- If you hit a blocker or unexpected state, stop and ask — don't try to work around it

## Resources

**IDE Services docs:** https://www.jetbrains.com/help/ide-services/get-started.html

**IntelliJ IDEA docs:** https://www.jetbrains.com/help/idea/getting-started.html

**JetBrains Toolbox App docs:** https://www.jetbrains.com/help/toolbox-app/installation.html

**Demo reference config (IDES-A-567):** https://youtrack.jetbrains.com/articles/IDES-A-567/Reference-config-for-application-demo.yml
— Use as the starting point unless told otherwise. Write content to `application-demo.yml`.

**Demo environment:**
— Version is controlled via `docker-compose.yml`. Verify certificates against `README.md` on first run.

## Standard Demo Startup

1. Check product docs for the latest release version
2. Compare with local images: `docker images | grep tbe-server` — pull if behind
3. Update version in `docker-compose.yml`
4. Replace `application-demo.yml` with reference config from IDES-A-567 (unless told otherwise)
5. `docker compose up -d`
6. Wait for all containers healthy: `docker compose ps`
7. Verify certificates in system trust store per `README.md`

## IDE Interaction

**Prefer keyboard over menus:**

- Find Action: `Ctrl+Shift+A` — trigger any action by name
- Settings: `Ctrl+Alt+S`
- Toolbox App: lives in the system tray; use arrow keys / Enter / Tab inside it
- IDE Services server URL: Toolbox Settings → IDE Services

**Prefer direct file edits over IDE GUI** for VM options and log config — the GUI editor requires extra Save clicks and can silently fail:

| Config               | Path                                                    |
| -------------------- | ------------------------------------------------------- |
| VM options           | `~/.config/JetBrains/<ProductVersion>/idea64.vmoptions` |
| Debug log categories | `~/.config/JetBrains/<ProductVersion>/options/log.xml`  |

**Finding an IDEA installation** — if not under the standard Toolbox path, search broadly:

```
find ~ -name "product-info.json" 2>/dev/null | xargs grep -l "IntelliJIdea"
```

**Isolating the current session in idea.log** — the log accumulates across restarts:

```
grep -n "AppStarter.*JVM options" idea.log | tail -1   # get line N
tail -n +N idea.log | grep <pattern>
```

## Computer Use / GUI Precision

**Before any GUI interaction**, check the screen resolution — screenshots are full-resolution and coordinates map 1:1 to screen coords:

```
xdpyinfo | grep dimensions
```

**For browser interactions:** prefer `browser_snapshot` (richer accessibility tree) over screenshot.

**For IDE / desktop interactions:** use `scrot` for screenshots. Take a screenshot first to orient before acting.

**Clicking a dialog button reliably:**

1. Get window geometry: `xdotool getwindowgeometry <wid>`
2. Crop to the button area to locate its exact center:
   ```
   convert screenshot.png -crop WxH+X+Y /tmp/button.png
   ```
3. Compute screen coords from the crop offset + button center in the crop
4. If the click still misses, use keyboard instead: `xdotool key alt+Return` (OK), `alt+c` (Cancel), or `Tab` / `Space` to navigate and press
