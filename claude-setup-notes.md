# Claude Setup Notes

## Step-by-Step Setup Guide

**New to Terminal?** Don't worry! Follow these steps in order, and we'll guide you through each decision.

### Step 1: Open Terminal

1. Press **Cmd+Space** to open Spotlight search
2. Type "Terminal" and press Enter
3. A black or white window will open - this is your Terminal

**Terminal Basics:**

- **Copy text:** Highlight text, then **Cmd+C**
- **Paste text:** **Cmd+V** (if this doesn't work, try right-clicking and selecting "Paste")
- **Run a command:** Type it and press **Enter**
- **Command history:** Press **Up arrow** to cycle through previous commands you've run
- **Edit previous commands:** Use Up arrow to find a command, then Left/Right arrows to edit it
- **Clear current line:** **Cmd+C** (this cancels the current command, doesn't copy)
- **Clear screen:** **Cmd+K** or type `clear` and press Enter

**Pro tip:** The Terminal remembers hundreds of commands you've run. Use the Up arrow to quickly re-run or modify previous commands instead of retyping them!

### Step 2: Switch to zsh (Required)

Modern macOS uses zsh as the default shell. We'll ensure you're using it:

```bash
chsh -s /bin/zsh
```

**What happens:** You might be asked for your Mac password (the one you use to log in).

**Next:** Close Terminal completely (Cmd+Q) and reopen it.

### Step 3: Install Apple Command Line Tools

These tools include git and other essentials that Claude Code needs:

```bash
xcode-select --install
```

**What will happen:**

1. A popup window will appear asking to install developer tools
2. Click "Install" and wait 5-10 minutes for download
3. You'll see a confirmation when it's complete

### Step 4: Install Claude Code

**What is Claude Code?** It's the command-line tool that lets you interact with Claude AI from Terminal.

#### 4a. Install Claude Code

Copy and paste this command:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**What will happen:**

- Claude Code will download and install
- The installer will guide you through connecting your Anthropic account
- No password required for this step

**Don't have a Claude account yet?** Create one at [claude.ai](https://claude.ai) first.

#### 4b. Verify Claude Code installation

Close and reopen Terminal, then run:

```bash
claude --version
```

**Expected result:** You should see a version number like "claude 0.x.x"

**If you see "command not found":**

1. Add Claude to your PATH permanently:

   ```bash
   echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
   ```

2. Restart Terminal completely (Cmd+Q then reopen)
3. Try `claude --version` again

### Step 5: Final Verification

**Everything installed correctly?** Run this final check:

```bash
echo "macOS: $(sw_vers -productVersion)"
echo "Shell: $SHELL"
git --version
claude --version
```

**What you should see:**
- Your macOS version 
- Shell: /bin/zsh
- Git version number
- Claude version number

**Final test:**
```bash
claude --help
```

If this shows Claude's help menu, you're all set! 🎉

**If any of these commands fail:** Check the troubleshooting section below.

### Your AI Assistant is Ready!

Now that Claude Code is installed, remember that you have an AI assistant ready to help with:
- Terminal commands and git workflows
- Explaining error messages
- Writing code and debugging
- Setting up projects and repositories
- Learning new programming concepts

**Try it now:** Run `claude` and ask something like:
- "Help me understand what git is"
- "What should I do next to start coding?"
- "Explain the files in this directory"

Claude learns from your codebase and adapts to your projects, so the more you use it, the more helpful it becomes!

---

## Step 6: Install Homebrew (Recommended)

**What is Homebrew?** A package manager that makes installing developer tools easier. We'll need it to install the GitHub CLI for working with repositories.

**Why do we need this?** If you want to create projects and push them to GitHub (which most developers do), you'll need the GitHub CLI tool, which is easiest to install via Homebrew.

### Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**What will happen:**

1. You'll be asked for your Mac password
2. Press **Enter** when it asks "Press RETURN to continue"
3. Wait 5-15 minutes for installation

### Add Homebrew to your PATH

Check your Mac type:

```bash
uname -m
```

**If "arm64"** (Apple Silicon):

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

**If "x86_64"** (Intel Mac):

```bash
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/usr/local/bin/brew shellenv)"
```

### Test Homebrew

```bash
brew --version
```

You should see something like "Homebrew 4.x.x".

### Install GitHub CLI

Now that Homebrew is working, let's install the GitHub CLI (command-line tool for GitHub):

```bash
brew install gh
```

**What will happen:**
- Homebrew will download and install the GitHub CLI
- This might take a few minutes
- You'll see progress messages as it installs

### Test GitHub CLI

```bash
gh --version
```

You should see something like "gh version 2.x.x".

---

## Claude Code Tips & Features

Now that Claude Code is installed, here are some useful features and CLI basics that aren't immediately obvious:

### Pasting Images
You can paste images directly from your clipboard into Claude Code prompts:
1. Copy an image to your clipboard (Cmd+C from any app, or **Cmd+Shift+Ctrl+4** for screenshot to clipboard)
2. In the Claude Code prompt, just paste with **Ctrl+V** (note: Ctrl, not Cmd in the prompt)
3. Claude can analyze screenshots, diagrams, code snippets, etc.

### CLI Navigation Basics
If you're new to command-line interfaces, these keyboard shortcuts are essential:

**Tip:** If any of these concepts are confusing, just ask Claude! Try: "Explain Terminal keyboard shortcuts" or "What does Ctrl+C do in Terminal?"

**Text Navigation:**
- **Arrow keys** - Move cursor left/right, up/down through command history
- **Cmd+A** - Select all text in current line
- **Cmd+Left/Right** - Jump to beginning/end of line
- **Option+Left/Right** - Jump word by word

**Important Differences from Regular Apps:**
- **Can't click to move cursor** - Use arrow keys instead
- **Ctrl+C** - Cancels/interrupts the current command (doesn't copy text!)
- **Copy/Paste varies by context:**
  - Terminal commands: **Cmd+C/V**  
  - Claude Code prompts: **Ctrl+C/V**

### Interactive Mode Features
When you run `claude` without arguments, you enter interactive mode:

**Multi-line Input:**
- Type your question normally
- Press **Enter** to send the message
- For multi-line prompts, use **Shift+Enter** for new lines without sending

**Command History:**
- **Up/Down arrows** - Browse through your previous prompts
- Great for tweaking and re-running similar requests

**File References:**
- Type `@` to see a searchable list of files in your project tree
- **Navigate the list:** Use arrow keys to highlight files (purple highlight shows selection)
- **Search/Filter:** Keep typing after `@` to find files anywhere in the tree (e.g., `@fig` finds all files containing "fig")
- **Select file:** Press **Enter** to select the highlighted file
- **Cancel:** Press **Escape twice** to close the chooser
- Claude will read and include the selected file content in the conversation
- **Tip:** The search looks through the entire project tree below your current directory

### Useful Commands
```bash
# Start interactive session
claude

# Run a single command
claude "What's in this directory?"

# Get help
claude --help

# Check version
claude --version
```

---

## Creating Your First Project with Git and GitHub

Now that you have Claude Code and GitHub CLI set up, let's walk through creating a project and pushing it to GitHub. This is where Claude Code really shines!

### Step 1: Create a Project Directory

First, let's create a directory for your project:

```bash
mkdir my-first-project
cd my-first-project
```

### Step 2: Add Some Files

Create a simple file to get started:

```bash
echo "# My First Project" > README.md
```

### Step 3: Let Claude Help You Set Up the Repository

Here's where it gets interesting! Start Claude Code and ask it to help:

```bash
claude
```

In the Claude prompt, you can ask:
```
Help me turn this directory into a git repository and create a CLAUDE.md file for it
```

**What Claude will do:**
- Run `git init` to initialize the repository
- Use the `/init` command to analyze your project and create a CLAUDE.md file
- Guide you through the setup process

### Step 4: Authenticate with GitHub

Before pushing to GitHub, you need to authenticate:

```bash
gh auth login
```

**What will happen:**
1. You'll be asked how you want to authenticate
2. Choose "GitHub.com" 
3. Choose "HTTPS" as the protocol
4. Choose "Login with a web browser"
5. Follow the prompts to authenticate in your browser

### Step 5: Create a GitHub Repository

You can either:

**Option A: Ask Claude to help**
```
Help me create a GitHub repository and push my code
```

**Option B: Do it manually**
```bash
gh repo create my-first-project --public --source=. --remote=origin --push
```

**What this does:**
- Creates a new public repository on GitHub called "my-first-project"
- Sets up the remote origin
- Pushes your code to GitHub

### Step 6: Verify Everything Worked

Check that everything is set up correctly:

```bash
git remote -v
git status
```

You should see your GitHub repository URL and a clean working directory.

**Visit your repository:** Go to `https://github.com/yourusername/my-first-project` to see your code online!

### Getting Help from Claude

Remember, at any point in this process, you can ask Claude for help:
- "How do I commit my changes?"
- "Help me push this to GitHub"
- "What does this git error mean?"
- "Create a .gitignore file for my Python project"

Claude understands git, GitHub, and development workflows, so don't hesitate to ask for guidance!

---

## Configuration Files

Claude Code uses CLAUDE.md files to understand your projects better. These files tell Claude about your codebase, build commands, and project structure.

#### Project-Specific CLAUDE.md (Recommended)

**Location:** Project root directory  
**Purpose:** Project-specific instructions and context

**Easy way to create one:** In any project directory, run:
```bash
claude /init
```

**What `/init` does:**
- Analyzes your codebase structure
- Identifies build/test commands from package.json, Makefile, etc.
- Creates a CLAUDE.md file with project-specific guidance
- Makes future Claude interactions more helpful and context-aware

**Manual creation:** You can also create CLAUDE.md yourself with information like:
- How to build/test your project
- Key architectural decisions
- Important conventions to follow

#### Global CLAUDE.md (Optional)

**Location:** `~/.claude/CLAUDE.md`  
**Purpose:** Global instructions that apply to all projects  
**Use for:** Personal coding preferences, general guidelines that override Claude's defaults

## Common Commands

```bash
# Check Claude Code version
claude --version

# Get help
claude --help

# Interactive mode
claude
```

## Troubleshooting

### Installation Issues

#### Apple Command Line Tools Issues

**Problem:** Installation popup doesn't appear

- **Solution:** Tools may already be installed. Try `git --version` to check

#### Claude Code Installation Issues

**Problem:** "claude: command not found" after installation

- **Solution:** Restart Terminal completely (Cmd+Q then reopen)

#### Shell Environment Issues

**Problem:** Commands work in one terminal tab but not another

- **Solution:** Restart Terminal completely (Cmd+Q then reopen)

**Problem:** "command not found" after installation

- **Solution:** Run `source ~/.zprofile` then try the command again

#### Copy/Paste Issues in Terminal

**Problem:** Cmd+V doesn't work in Terminal

- **Solution:** Right-click and select "Paste" instead

### Common Mistakes to Avoid

1. **Using sudo** - Don't use `sudo` with these installation commands
2. **Not restarting Terminal** - Always restart Terminal (Cmd+Q then reopen) after installations
3. **Skipping steps** - Follow the steps in order, don't skip ahead

### Getting Help

**If something isn't working:** 
1. Run the verification script from Step 5 again and check which parts show "Missing"
2. **Ask Claude for help!** If Claude Code is working, run `claude` and describe your problem:
   - "I'm getting an error when I try to run brew"
   - "Claude command not found, what should I do?"
   - "Help me troubleshoot my Terminal setup"

Claude can often provide personalized troubleshooting based on your specific error messages.

### Resources

- Official documentation: [https://docs.anthropic.com/en/docs/claude-code](https://docs.anthropic.com/en/docs/claude-code)
- GitHub issues: [https://github.com/anthropics/claude-code/issues](https://github.com/anthropics/claude-code/issues)
