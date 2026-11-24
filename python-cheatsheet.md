# Python and venv Cheatsheet (Windows, PowerShell)

## Why a virtual environment?
A virtual environment (venv) is a private folder of Python packages for ONE project. Installing pytest into the venv means it never clashes with anything else on your laptop, and anyone (or any CI server) can rebuild the same setup. Rule: **every project gets its own `.venv`.**

## Create it (once per project)
Run this from the project's root folder (for `workbench`, the folder that contains `tasks/`):

```powershell
python -m venv .venv
```

## Activate it (every new terminal)
```powershell
.\.venv\Scripts\Activate.ps1
```
Your prompt now starts with `(.venv)`. That means python and pip now belong to the venv.

If PowerShell says "running scripts is disabled on this system", run this once (no admin needed), answer `Y`, then try again:
```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```
If your device policy blocks even that, skip activating and call the venv's Python directly:
```powershell
.\.venv\Scripts\python.exe -m pytest tasks/1-1-hello
```

## Let VS Code use it
1. Install the Python extension (once).
2. Press `Ctrl+Shift+P`, type `Python: Select Interpreter`, and pick the one inside `.venv`.
3. Open a NEW terminal in VS Code. It should activate the venv automatically and show `(.venv)`.

## Check you're really inside it
```powershell
python --version
python -c "import sys; print(sys.prefix)"
```
The path printed should end in `.venv`.

## pip: install and manage packages
Always call it as `python -m pip` so you know which Python it belongs to.

```powershell
python -m pip install --upgrade pip   # update pip itself
python -m pip install pytest          # install a package
python -m pip list                    # what's installed
python -m pip freeze                  # exact versions, in a shareable format
python -m pip uninstall pytest        # remove a package
```

## Run tests
```powershell
python -m pytest tasks/1-1-hello
```

## Leave the venv
```powershell
deactivate
```

## Never
- Never commit `.venv` to git. It is listed in `.gitignore`. Check with `git status`.
- Never install packages while the venv is NOT active (no `(.venv)` in the prompt).
- Never copy a `.venv` folder to another machine. Rebuild it instead.

## Troubleshooting
| Symptom | Likely cause | Fix |
|---|---|---|
| `python` opens the Microsoft Store or says not found | Python isn't on PATH, or the terminal was open during install | Close and reopen the terminal; try `py --version`; ask the product owner |
| `No module named pytest` | venv not active, or pytest installed somewhere else | Activate `.venv`, then `python -m pip install pytest` |
| `(.venv)` missing in a new terminal | VS Code didn't pick the interpreter | `Ctrl+Shift+P`, `Python: Select Interpreter`, choose `.venv`, open a new terminal |
| venv is broken or confusing | It happens | Delete the `.venv` folder and recreate it. Nothing precious lives in it. |
