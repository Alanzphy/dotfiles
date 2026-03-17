This repository contains my personal configuration (dotfiles) managed through [chezmoi](https://chezmoi.io/). It is structured to keep my development environments synchronized smartly, applying specific configurations depending on whether I'm working on **Arch Linux** or **macOS**.

---

## Chezmoi Workflow (Cheatsheet)

Chezmoi doesn't work with direct symlinks like other tools. Instead, it maintains an internal Git repository (usually in `~/.local/share/chezmoi`) that acts as the **"source of truth"**. 

Here are the main commands for daily use:

### 1. Adding and Editing Files
* **`chezmoi add ~/.path/to/file`**
  Tracks a new file. **Note:** If the file is already in chezmoi and is a template (`.tmpl`), running `add` will overwrite the template with the static version from your local system. Only use it for new files.

* **`chezmoi edit ~/.path/to/file`**
  Opens the "source" version of the file in your default editor (`$EDITOR`). If the file is a template, you'll see the source code with the conditionals (e.g., `{{ if ... }}`). This is the correct way to make changes.

### 2. Templates and Multi-OS Logic
For the same file to have different configurations on Mac and Linux, it must be a template.

* **`chezmoi chattr +template ~/.path/to/file`**
  Converts a normal file into a template. Internally, chezmoi appends the `.tmpl` extension. After doing this, use `chezmoi edit` to add the conditionals.

**Syntax Example (Go Templates):**
```ini
{{- if eq .chezmoi.os "darwin" }}
# macOS specific configuration
alias rm='trash -v'
{{- else if eq .chezmoi.os "linux" }}
# Linux (Arch) specific configuration
alias uu='yay -Syyu'
{{- end }}
```

### 3. Verifying and Applying Changes
Never apply changes blindly. Always verify what chezmoi is going to modify on your local system.

* **`chezmoi diff`**
  Shows the differences between the source state (your chezmoi repository) and your local system. You can specify a file: chezmoi diff ~/.zshrc.

* **`chezmoi apply`**
  Applies the changes from the source repository to your local system.

To apply everything: `chezmoi apply`

To apply a single file: `chezmoi apply ~/.ssh/config`

### 4. Version Control (Pushing to GitHub)
Your dotfiles live in a Git repository managed by chezmoi. To commit and push to GitHub:

chezmoi cd → Moves you directly to the repository folder (~/.local/share/chezmoi).

Use standard Git commands:

```Bash
git status
git add .
git commit -m "feat: update zsh configurations"
git push
Type exit (or press Ctrl + D) to leave that folder and return to where you were originally.
```

### Installation on a New Machine
To clone and apply these dotfiles on a fresh machine:
```Bash
chezmoi init --apply https://github.com/Alanzphy/dotfiles.git
```
