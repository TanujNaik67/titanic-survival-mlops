# Titanic Survival ML Project — Development Setup

**Last updated:** 3 October 2026  
**Repository:** `titanic-survival-mlops`  
**Local path:** `D:\ML-Projects\titanic-survival-mlops`  
**GitHub:** `https://github.com/TanujNaik67/titanic-survival-mlops`

## Purpose

This document records the local development setup for the Titanic Survival ML project, including the problems encountered and their solutions. It should be updated whenever the development environment or setup process changes.

The project follows an industry-style workflow:

- VS Code is the main development environment.
- Jupyter notebooks run inside VS Code for exploration and experimentation.
- Python modules (`.py` files) contain reusable and production-style code.
- Conda provides an isolated environment for project dependencies.
- Git tracks local changes, and GitHub stores the shared repository history.

## Tools verified

| Tool | Verified version/state |
|---|---|
| Python | System Python 3.10.6 and Anaconda Python 3.12 available |
| Conda | 24.11.3 |
| Git | 2.55.0.windows.4 |
| VS Code | 1.133 |
| VS Code Python extension | Installed |
| VS Code Jupyter extension | Installed |
| GitHub repository | Created and cloned locally |

## Repository setup completed

1. Created the public GitHub repository `titanic-survival-mlops`.
2. Initialized it with:
   - `README.md`
   - Python `.gitignore`
   - MIT License
   - `main` as the default branch
3. Configured the Git username and email locally.
4. Created the parent project directory:

   ```text
   D:\ML-Projects
   ```

5. Cloned the GitHub repository into:

   ```text
   D:\ML-Projects\titanic-survival-mlops
   ```

6. Verified that the repository was on `main`, synchronized with `origin/main`, and had a clean working tree.
7. Opened the repository in VS Code and trusted only this repository workspace.

## Conda environment setup

### Why a separate environment is used

Each project should have its own isolated Python environment. This prevents package-version conflicts and makes the project reproducible on another computer.

The following environments were already present:

- `base` at `D:\anaconda3`
- An older path-based environment at `D:\Python ML\venv`

The older environment was left untouched because its purpose and dependencies were not verified. The Conda `base` environment is kept free from project-specific libraries. A new environment was therefore created specifically for this repository.

### Project environment

Environment name:

```text
titanic-ml
```

Creation command:

```powershell
conda create --name titanic-ml python=3.12 -y
```

Expected environment location:

```text
D:\anaconda3\envs\titanic-ml
```

Activation command:

```powershell
conda activate titanic-ml
```

Current confirmed terminal prompt:

```text
(titanic-ml) PS D:\ML-Projects\titanic-survival-mlops>
```

This confirms that the named environment is active in the VS Code terminal.

## Problems encountered and fixes

### 1. Conda package download failed during environment creation

The first environment-creation attempt failed with a network-related error similar to:

```text
Connection broken: IncompleteRead
```

Resolution:

1. Ran `conda env list` to confirm that no incomplete `titanic-ml` environment remained.
2. Re-ran the same `conda create` command.
3. The second attempt completed successfully with `Executing transaction: done`.

Lesson: transient download failures can occur. Before retrying, verify whether Conda created a partial environment.

### 2. `conda activate` did not change the terminal environment

Initially, running:

```powershell
conda activate titanic-ml
```

did not add `(titanic-ml)` to the prompt, and `conda info --envs` did not show an active-environment marker.

Cause: Conda had not initialized its PowerShell integration.

Fix:

```powershell
conda init powershell
```

Conda updated the current user's PowerShell profile. The terminal then needed to be closed and reopened.

### 3. PowerShell blocked the Conda profile script

After restarting the terminal, PowerShell reported that the profile could not be loaded because script execution was disabled.

Diagnosis command:

```powershell
Get-ExecutionPolicy -List
```

All displayed scopes were initially `Undefined`.

Fix applied only to the current Windows user:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Verification command:

```powershell
Get-ExecutionPolicy -Scope CurrentUser
```

Verified result:

```text
RemoteSigned
```

After opening a new VS Code terminal, Conda loaded correctly as `(base)`, and the project environment could then be activated as `(titanic-ml)`.

Security note: the policy was changed only for `CurrentUser`, not for the entire computer. `RemoteSigned` permits locally created scripts while requiring downloaded scripts to be signed unless explicitly unblocked.

## Starting a future development session

1. Open the repository in VS Code.
2. Open a new integrated PowerShell terminal.
3. Confirm that the terminal path is:

   ```text
   D:\ML-Projects\titanic-survival-mlops
   ```

4. Activate the project environment:

   ```powershell
   conda activate titanic-ml
   ```

5. Confirm that the prompt begins with `(titanic-ml)` before installing packages or running project code.

## Remaining setup checks

The foundational setup is complete, but the following items must be completed before beginning model development:

- [ ] Verify the Python version inside `titanic-ml`.
- [ ] Verify that `python` resolves to `D:\anaconda3\envs\titanic-ml\python.exe`.
- [ ] Select `titanic-ml` as the VS Code workspace interpreter.
- [ ] Install the initial ML and notebook dependencies in controlled stages.
- [ ] Register/select the environment as the Jupyter kernel.
- [ ] Create and test the project folder structure.
- [ ] Record dependencies in a reproducible environment file.
- [ ] Create a setup branch before committing project scaffolding.

## Repository hygiene rules

- Do not install project packages into Conda `base`.
- Do not reuse an unrelated environment for this project.
- Do not commit the Conda environment directory to Git.
- Do not commit credentials, API keys, tokens, or local secrets.
- Track setup instructions and dependency definitions in Git so another developer can reproduce the environment.
