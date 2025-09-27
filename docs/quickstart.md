Windexter Cheat Sheet

1. Open Ubuntu (WSL).
2. The shell auto-runs ~/.bashrc, so OPENAI_API_KEY and the cua() helper are ready.
3. Start a session:
   - With a starting instruction: cua "open bing and search for weather"
   - Without a starting instruction: cua
4. Watch the terminal output. Whenever you see the bare prompt `>`, type your reply (for example yes, continue, or another instruction) and press Enter.
5. Type `exit` or press Ctrl+C to finish.

Notes:
- The `cua` helper automatically changes into ~/windexter, activates .venv, and launches python cli.py --computer local-playwright.
- Rotate your API key by editing ~/.bashrc, then run `source ~/.bashrc` or open a new shell.
- To capture a transcript, run `script -aq ~/windexter-session.log cua` and interact as usual.
