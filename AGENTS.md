# AGENTS.md

This repository is a small browser-based Web Bluetooth prototype for LEGO/Pybricks-style gamepad control. It is intentionally lightweight and does not use a framework or build system.

## Project layout

- [bots.html](bots.html): main controller page. Connects to gamepads and sends control data to a hub over Bluetooth.
- [lwp_test.html](lwp_test.html): focused LWP protocol test page used to validate lower-level hub messaging.

## Working conventions

- Keep changes in plain HTML, CSS, and JavaScript unless there is a clear need for a different approach.
- Prefer direct browser APIs such as `navigator.bluetooth`, `Gamepad`, `TextEncoder`, and `TextDecoder`.
- Keep protocol constants and Bluetooth connection logic near the relevant functions instead of splitting them across many files.
- Preserve compatibility with the existing hub communication patterns; this code is hardware-integration code, not a generic web app.
- Avoid adding package managers, bundlers, or dependencies unless the task truly requires them.

## Validation guidance

- There is no automated test suite in this repository.
- Validate browser behavior by serving the folder locally and opening the page in a Chromium-based browser that supports Web Bluetooth.
- Use a local static server rather than opening raw files directly when possible, because Web Bluetooth requires a secure context.

Example:

```bash
cd "c:/Users/StrayCat/Documents/PybricksGamepads"
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/bots.html
```

## Project-specific notes

- The Bluetooth UUIDs and characteristic logic are central to the app; changing these values can break hub communication.
- When editing connection, reconnect, or send-data code, verify behavior against the actual hardware and keep the existing reconnect logic intact unless the bug requires a targeted change.
- Keep the project portable and minimal; this repo appears to be a small prototype and not a production application framework.
