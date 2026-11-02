# Contributing

Thanks for helping! The project is a single static page, so setup is simple.

1. Fork and clone the repo.
2. Serve it: `python3 -m http.server 8000`, then open http://localhost:8000.
3. Edit `index.html`. Test with **Try with sample files** and with a small folder of real photos.
4. Open a pull request describing what changed and how you tested it.

Guidelines:

- Keep it dependency-free and in one file unless there is a strong reason.
- Never delete user files. Any feature that writes to a folder must be optional, non-overwriting and undoable.
- Respect `prefers-reduced-motion`.
- Do not add tracking or send data anywhere new without documenting it in `docs/PRIVACY.md`.
