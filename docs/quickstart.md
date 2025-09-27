# Windexter Quick Start (WSL example)

1. Clone the repo and enter it:
```bash
git clone https://github.com/BranchManager69/windexter.git
cd windexter
```
2. Create and activate a virtual environment, then install dependencies:
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python -m playwright install
# Ubuntu / Debian desktops also need Playwright system deps:
sudo ./.venv/bin/playwright install-deps
```
3. Provide credentials. Either export an API key before every session:
```bash
export OPENAI_API_KEY="sk-..."
```
or create a `.env` file based on `.env.example`.
4. Launch Windexter:
```bash
python cli.py --computer local-playwright
# or add an opening directive:
python cli.py --computer local-playwright --input "open bing and search for weather"
```
5. Watch the terminal. Every agent turn prints there. When you see a bare `>` prompt the agent is waiting-type your reply (for example `yes`, `continue`, or a new instruction) and press Enter.
6. Type `exit` or press `Ctrl+C` to stop the session.

## Optional Bash helper
Add this snippet to your shell profile if you want a single command:
```bash
cua() {
  cd ~/windexter || return
  source .venv/bin/activate
  if [ "$#" -gt 0 ]; then
    python cli.py --computer local-playwright --input "$*"
  else
    python cli.py --computer local-playwright
  fi
}
```
Reload your shell (or run `source ~/.bashrc`) and use `cua "your instruction"` to start a session quickly.

## Capturing transcripts
Run Windexter through `script` to keep a log alongside the interactive session:
```bash
script -aq ~/windexter-session.log cua "summarize https://news.ycombinator.com"
```
