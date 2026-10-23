# Introduction to Git

## 1. What is Git?

> Git is a free and open source distributed version control system

Source: [Git — official website](https://git-scm.com/about#free-and-open-source)

- Track changes in project files.
- Save versions of your code (**commits**).
- Restore earlier versions.
- Work on separate versions (**branches**).
- Work locally — no GitHub account required.

<!-- Screenshot: Git website -->

## 2. Install Git

### Windows

- Download: [Git for Windows](https://git-scm.com/install/windows).
- Run the installer (default options are sufficient for this exercise).
- Open termiall (*PowerShell*)

### Linux (Debian / Ubuntu)
  - open termiall and write:

    ```bash
    sudo apt update
    sudo apt install git
    ```

  - other distributions: [Git for Linux](https://git-scm.com/install/linux).

### macOS

  - open termiall and write:
    ```bash
    xcode-select --install
    ```

  - or, with Homebrew:

    ```bash
    brew install git
    ```

See [Git for macOS](https://git-scm.com/install/mac).


### Check installation

  - interminal write:

    ```bash
    git --version
    ```

<!-- Screenshot: git --version -->


## 3. First-time configuration

  - set your name and email address:

    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"
    git config --global init.defaultBranch main
    ```

  - check:

    ```bash
    git config --global --list
    ```

  - `--global`: settings for your user account.
  - Name and email are stored in commits.
  - No online account or connection is needed.

See [First-Time Git Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup).

<!-- Screenshot: Git configuration -->

---



# Python project and Git

## 1. Create a Python project

  - Project structure (simple directory with app.py file):

    ```text
    git-demo/
    └── app.py
    ```

  - open termiall
  - create and enter a folder:

    ```bash
    mkdir git-demo
    cd git-demo
    ```

  - create `app.py` in your editor (e.g. `micro app.py`):
    ```bash
    micro app.py
    ```
  - write example functions and save file:

    ```python
    def hello():
        pass
    
    
    def goodbye():
        pass
    ```


## 5. Start a local repository
  - in terminal write:

    ```bash
    git init
    git status
    ```

    >- `.git/`: hidden directory with Git history and settings.
    >- `app.py`: untracked file.

  - add the file and save the first version:

    ```bash
    git add app.py
    git status
    git commit -m "Add two functions"
    git log --oneline
    ```

    >- `add`: select changes for the next commit (**stage**).
    >- `commit`: save a version in Git history.
    >- `log`: show saved commits.

See [Recording Changes](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository).

<!-- Screenshot: first commit and git status -->


## 6. Change the code and commit again

  - delete `goodbye()` from `app.py`:

    ```python
    def hello():
        pass
    ```

  - inspect and save:

    ```bash
    git status
    git diff
    git add app.py
    git commit -m "Remove goodbye function"
    git log --oneline
    ```

    >- `status`: changed files.
    >- `diff`: changes not yet staged.
    >- `log --oneline`: short commit history.

<!-- Screenshot: git diff and two commits -->



## 7. Restore an earlier version

  - show commit history:

    ```bash
    git log --oneline
    ```

  - restore files from a selected commit:

    ```bash
    git restore --source=<commit-id> <file>
    ```
    
    Example:
    
    ```bash
    git restore --source=abc1234 app.py
    ```

### Option A: keep the restored version

  - save the restoration as a new commit:

    ```bash
    git add app.py
    git commit -m "Restore previous version of app.py"
    git log --oneline
    ```

### Option B: cancel the restoration

  - discard the restoration and return to the current version (before `git add`):

    ```bash
    git restore <file>
    ```

    Example:

    ```bash
    git restore app.py
    ```

    >- `git restore --source=<commit-id> <file>`: restore a file from a selected commit.
    >- `git restore <file>`: restore a file from the staging area (normally the current committed version).
    >- Restoring files does not change commit history.
    >- A new commit saves the restored version in history.


See [git restore](https://git-scm.com/docs/git-restore).

---



# `.gitignore` - ignore unnecessary files

A `.gitignore` file lists files and folders Git should not track.

Python projects often contain:

  - Virtual environments (`.venv/`).
  - Python cache files (`__pycache__/`).
  - Build output (`build/`, `dist/`).
  - Jupyter checkpoints (`.ipynb_checkpoints/`).


  1. Create `.gitignore` in the project folder:

      ```bash
      micro .gitignore
      ```
  
  2. put to .gitignore:
      ```gitignore
      .venv/
      venv/
      __pycache__/
      *.py[cod]
      .ipynb_checkpoints/
      build/
      dist/
      *.egg-info/
      ```

  3. Test it:

      ```bash
      python -c "import app"
      git status
      ```

      >- Python may create `__pycache__/`.
      >- Git should not list cache files as untracked.
      >- Git should list `.gitignore` as untracked.

  4. Save `.gitignore`:

      ```bash
      git add .gitignore
      git commit -m "Add Python gitignore"
      git status
      ```


See [Ignoring Files](https://git-scm.com/docs/gitignore) and [Python .gitignore examples](https://github.com/github/gitignore/blob/main/Python.gitignore).

<!-- Screenshot: git status with ignored cache -->

---


# Commands used

| Command | Purpose |
|---|---|
| `git init` | Create a repository |
| `git status` | Check file status |
| `git diff` | Show unstaged changes |
| `git add app.py` | Stage a file |
| `git commit -m "..."` | Save a commit |
| `git log --oneline` | Show commit history |
| `git restore ...` | Restore file contents |

<!-- Screenshot: final project folder and git log --oneline --graph --all -->
