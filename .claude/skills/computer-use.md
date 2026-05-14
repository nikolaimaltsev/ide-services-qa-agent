# Computer Use / GUI Precision

- use opendesk mcp as a primary computer use tool

- before using check that you have all the preferrable tools for the task and if missing, consider it a BLOCKER and ask user to install them

**Before any GUI interaction**, check the screen resolution — screenshots are full-resolution and coordinates map 1:1 to screen coords:

```
xdpyinfo | grep dimensions
```

**For IDE / desktop interactions:** 
- Take a screenshot first to orient before acting.

**Clicking a dialog button reliably:**

1. Get window geometry: `xdotool getwindowgeometry <wid>`
2. Crop to the button area to locate its exact center:
   ```
   convert screenshot.png -crop WxH+X+Y /tmp/button.png
   ```
3. Compute screen coords from the crop offset + button center in the crop
4. If the click still misses, use keyboard instead: `xdotool key alt+Return` (OK), `alt+c` (Cancel), or `Tab` / `Space` to navigate and press
