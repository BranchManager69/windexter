# Windexter

![License](https://img.shields.io/github/license/BranchManager69/windexter.svg) ![Release](https://img.shields.io/github/v/release/BranchManager69/windexter.svg) ![Built with](https://img.shields.io/badge/built%20with-Playwright-45ba4b.svg)

Windexter packages the OpenAI Computer-Using Agent sample into a ready-to-ship toolkit. It gives you a polished CLI for driving browser automation with Codex, a guard-railed step loop, and a foundation for wiring in richer "computer" backends.

## Features
- **Guided agent loop** – Every turn runs through a confirmable `>` prompt so you can stop or redirect the model on the fly.
- **Multiple computer targets** – Playwright (local), Docker desktops, Browserbase, and Scrapybara configs are built in.
- **Extensible interface** – Implement new `Computer` subclasses or tools to expose custom actions beyond the browser.
- **Summaries & history ready** – Works seamlessly with Codextendo helpers for session recall and transcripts.
- **Docs & quickstart included** – `docs/quickstart.md` walks through the full setup on WSL/Ubuntu.

## Table of Contents
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Sample Session](#sample-session)
- [Configuration](#configuration)
- [Extending Computers](#extending-computers)
- [Roadmap](#roadmap)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Requirements
- **OS**: macOS 12+, Ubuntu 20.04+/Debian 10+, or Windows 11 via WSL2.
- **Python**: 3.10 or newer with `venv` support.
- **Playwright**: Browser binaries plus system dependencies (install steps below).
- **Optional**: Docker Desktop (for the `docker` computer), Browserbase/Scrapybara accounts for hosted targets.

## Installation
```bash
git clone https://github.com/BranchManager69/windexter.git
cd windexter
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python -m playwright install
# Ubuntu/Debian: install system deps once
sudo ./.venv/bin/playwright install-deps
```
Need more detail? Follow the shell-by-shell walkthrough in [docs/quickstart.md](docs/quickstart.md).

## Usage
Start the CLI with the default Playwright computer:
```bash
python cli.py --computer local-playwright
```
Run once with an opening directive:
```bash
python cli.py --computer local-playwright --input "open bing and search for weather"
```
Prompt-only sessions work too—just launch the command and type your first instruction at the `>` prompt. Hit `Ctrl+C` or type `exit` to stop.

## Sample Session
```
$ python cli.py --computer local-playwright --input "open bing and search for weather"
New page created
screenshot({})
A browser is open with a blank search field. How would you like me to proceed?
> type "weather" and press enter
click({'button': 'left', 'x': 190, 'y': 178})
type({'text': 'weather'})
keypress({'keys': ['ENTER']})
wait({})
The Bing results show weather information for Palm City, FL. Would you like more detail or a different location?
>
```

## Configuration
Key CLI flags:
- `--computer <name>` – Selects a computer backend (see [computers/config.py](computers/config.py)).
- `--input "..."` – Seeds the first turn with a prompt.
- `--debug` / `--show` – Print raw responses or display screenshots.
- `--start-url` – Override the initial browser URL (browser computers only).

Environment variables:
- `OPENAI_API_KEY` – Required for Codex access.
- `CODEX_*` variables – Any Codex CLI settings you already use carry over.

## Extending Computers
Add new environments by creating subclasses under `computers/contrib/`:
1. Implement the methods defined in `computers/computer.py` or subclass `BasePlaywrightComputer`.
2. Register the class in `computers/contrib/__init__.py` and `computers/config.py`.
3. Document the option in the README and `docs/`.

## Roadmap
- Auto-continue mode for longer unattended runs.
- GPT-5 sidecar for automated follow-up instructions.
- Richer computer actions (file system, shell, MCP integrations).
- Tutorial videos and screenshots.

## Troubleshooting
- **Playwright fails to launch** – rerun `python -m playwright install` and, on Linux, `sudo ./.venv/bin/playwright install-deps`.
- **401 Invalid API key** – ensure `OPENAI_API_KEY` is exported in the shell running Windexter.
- **Browser never continues** – respond at the bare `>` prompt with `continue`, a new directive, or update `cli.py` to auto-continue.

## Contributing
Issues and pull requests are welcome. See open tasks in the [Roadmap](#roadmap) section or propose your own ideas.

## License
Windexter is released under the MIT License. See [LICENSE](LICENSE) for details.
