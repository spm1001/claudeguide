# Claude Setup Notes

## Step-by-Step Setup Guide

**New to Terminal?** Don't worry! Follow these steps in order, and we'll guide you through each decision.

### Step 1: Open Terminal

1. Press **Cmd+Space** to open Spotlight search
2. Type "Terminal" and press **Enter**
3. A black or white window will open - this is your Terminal

**Terminal Basics:**

- **Copy text:** Highlight text, then **Cmd+C**
- **Paste text:** **Cmd+V** (if this doesn't work, try right-clicking and selecting "Paste")
- **Run a command:** Type it and press **Enter**
- **Command history:** Press **Up arrow** to cycle through previous commands you've run
- **Edit previous commands:** Use **Up arrow**/**Down arrow** to find a command, then **Left**/**Right** arrows to edit it
- **Clear current line:** **Cmd+C** (this cancels the current command, doesn't copy)
- **Clear screen:** **Cmd+K** or type `clear` and press **Enter**

**⚠️ IMPORTANT - Copy/Paste Safety:**
- **Only copy ONE LINE at a time** - copying multiple lines can cause weird errors
- **If you see `dquote>` or `>` prompts:** You've pasted incomplete text. Press **Ctrl+C** to cancel, then try again
- **If Terminal looks "stuck":** Press **Ctrl+C** to cancel the current command and get back to normal
- **Can't click to move cursor:** This isn't broken! Use **Left**/**Right** arrow keys instead

**Pro tip:** The Terminal remembers hundreds of commands you've run. Use the **Up arrow** to quickly re-run or modify previous commands instead of retyping them!

### Step 2: Switch to zsh (Required)

**Why this matters:** If you've migrated between Mac computers, you might still be using the old `bash` shell. Claude Code works best with `zsh` (the modern default).

**Check what you're currently using:**
```bash
echo $SHELL
```

**If you see `/bin/bash`, switch to zsh:**
```bash
chsh -s /bin/zsh
```

**What happens:** You might be asked for your Mac password (the one you use to log in).

**Next:** Close Terminal completely (**Cmd+Q**) and reopen it.

**Verify it worked:** After reopening Terminal, type:
```bash
echo $SHELL
```
You should see `/bin/zsh`. If you still see `/bin/bash`, try the `chsh` command again and make sure you restart Terminal completely.

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

2. Restart Terminal completely (**Cmd+Q** then reopen)
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
- Your macOS version (any version is fine, but 10.15+ is recommended)
- Shell: /bin/zsh (if you see /bin/bash, go back to Step 2)
- Git version number (something like "git version 2.x.x")
- Claude version number (something like "claude 0.x.x")

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

## Step 6: Install Homebrew (Required for GitHub)

**What is Homebrew?** A package manager that makes installing developer tools easier. We need it to install the GitHub CLI for working with repositories.

**Why is this required?** If you want to create projects and push them to GitHub (which most developers do), you'll need the GitHub CLI tool. While you can use Claude Code without GitHub, you won't be able to:
- Push code to GitHub repositories
- Collaborate with others on projects
- Follow modern development workflows

The GitHub CLI is the simplest way to authenticate with GitHub - the alternatives (SSH keys, personal access tokens) are much more complex for beginners.

### Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**What will happen:**

1. You'll be asked for your Mac password
2. Press **Enter** when it asks "Press **Return** to continue"
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
1. Copy an image to your clipboard (**Cmd+C** from any app, or **Cmd+Shift+Ctrl+4** for screenshot to clipboard)
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

### Claude Code Input Modes (**Shift+Tab** to Switch)

Claude Code has three different input modes that control how it responds to your requests. Think of these like the editing modes in Google Docs (Edit/Suggest/View), but for AI assistance:

**🔧 Execute Mode (Default)**
- Claude **immediately runs commands and makes changes** 
- Best for: When you trust Claude and want things done quickly
- **Use when:** "Just fix this bug" or "Set up my git repository"

**📋 Plan Mode** 
- Claude **creates a plan first, then asks for approval** before doing anything
- Best for: Complex tasks where you want to review the approach first  
- **Use when:** "Help me refactor this code" or "Set up a new project structure"

**💬 Chat Mode**
- Claude **only provides advice and explanations** - never runs commands
- Best for: Learning, understanding code, or getting guidance
- **Use when:** "Explain this error" or "What's the best way to approach this?"

**How to switch modes:**
- Press **Shift+Tab** to cycle through the three modes
- The current mode shows at the bottom of your Claude Code interface
- **Tip:** Start in Plan Mode when you're unsure - you can always approve Claude's plan and let it execute

**Why this matters:** You stay in control! If Claude starts doing things too fast, press **Shift+Tab** to switch to Plan Mode and review its approach first.

**Command History:**
- **Up/Down arrows** - Browse through your previous prompts
- Great for tweaking and re-running similar requests

**File References:**
- Type `@` to see a searchable list of files in your project tree
- **Navigate the list:** Use **arrow keys** to highlight files (purple highlight shows selection)
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

Now that you have Claude Code and GitHub CLI set up, let's walk through turning your local files into a GitHub repository. This is where Claude Code really shines!

### Step 1: Navigate to Your Project

Most likely, you already have some files you want to put on GitHub. Here's how to navigate to them:

**Finding your project folder:**
1. **If it's on your Desktop:** `cd ~/Desktop/your-folder-name`
2. **If it's in Documents:** `cd ~/Documents/your-folder-name`
3. **If you're not sure where it is:** 
   - Open Finder, find your folder
   - Right-click the folder and choose "New Terminal at Folder"
   - This opens Terminal already in the right place!

**Or if you're starting fresh**, create a new directory:

```bash
mkdir my-first-project
cd my-first-project
echo "# My First Project" > README.md
```

**Tip:** You can always type `pwd` (print working directory) to see exactly where you are, and `ls` to see what files are in the current folder.

### Step 2: Configure Git Identity (Important!)

Before creating commits, git needs to know who you are. **Important:** Using your real email address will make it publicly visible in your commit history on GitHub!

**First, check your current git configuration:**
```bash
git config --global user.name
git config --global user.email
```

If these return nothing or show unwanted information, you need to set them up.

**Option A: Set up manually with privacy protection**

1. **Get your GitHub noreply email address:**
   - Go to [github.com/settings/emails](https://github.com/settings/emails)
   - Look for your noreply address (looks like `123456789+username@users.noreply.github.com`)

2. **Configure git:**
```bash
git config --global user.name "Your Name"
git config --global user.email "123456789+username@users.noreply.github.com"
```

3. **Set up global gitignore (recommended for Mac users):**
```bash
echo .DS_Store >> ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global
```

**Option B: Ask Claude to help** (recommended)

Start Claude Code and ask:
```
Help me set up git configuration for macOS, including privacy settings and .DS_Store handling
```

**What Claude will do:**
- Check your current git configuration
- Guide you to find your GitHub noreply email
- Set up user identity and global gitignore
- Explain why each setting matters

**Why this matters:**
- **Identity:** Without user config, git will refuse to create commits
- **Privacy:** Using your real email makes it visible to anyone who views your GitHub repositories
- **Mac-specific:** `.DS_Store` files are created by macOS and shouldn't be committed to repositories

### Step 3: Set Up the Git Repository

You have two approaches here:

**Option A: Do it manually** (good for learning)
```bash
git init                    # Initialize git repository
git add .                   # Add all files to staging
git commit -m "Initial commit"   # Create first commit
```

**Option B: Ask Claude to help** (recommended for beginners)

Start Claude Code and ask it to help:
```bash
claude
```

**⚠️ Important:** You're now in Claude Code's interactive mode - this is like a chat interface inside Terminal. You can't click to move the cursor here either!

In the Claude prompt, you can ask:
```
Help me turn this directory into a git repository and create a CLAUDE.md file for it
```

**What Claude will do:**
- Run the git commands for you
- Use the `/init` command to analyze your project and create a CLAUDE.md file
- Explain each step as it goes

**Key point:** If you exit Claude Code (type `/quit`) and restart it later, Claude won't remember this conversation. Each time you start `claude`, it starts fresh.

### Step 4: Authenticate with GitHub

**Don't have a GitHub account yet?** Create one at [github.com](https://github.com) first - it's free!

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

**Option A: Do it manually** (understanding the commands)
```bash
# Create the repository on GitHub and set up the connection
gh repo create my-first-project --public --source=. --remote=origin --push
```

**Breaking down this command:**
- `gh repo create` - Creates a new repository on GitHub
- `my-first-project` - The name of your repository
- `--public` - Makes it public (use `--private` for private repos)
- `--source=.` - Uses current directory as source
- `--remote=origin` - Sets up GitHub as your "origin" remote
- `--push` - Pushes your code immediately

**Option B: Ask Claude to help** (recommended)
```
Help me create a GitHub repository and push my code. I want it to be public and called "my-first-project"
```

**What Claude will do:**
- Run the GitHub CLI commands for you
- Explain what each flag does
- Handle any errors that come up
- Verify the connection worked

**Important:** Either way, this sets GitHub as your "origin" remote, which allows you to push and pull changes between your local files and GitHub.

### Step 6: Verify Everything Worked

Check that everything is set up correctly:

```bash
git remote -v
git status
```

You should see your GitHub repository URL and a clean working directory.

**Visit your repository:** Go to `https://github.com/yourusername/my-first-project` to see your code online!

### Getting Help from Claude

Remember, at any point in this process, you can ask Claude for help. Here are examples of both manual commands and how to ask Claude:

**Making changes and committing:**
- Manual: `git add . && git commit -m "Your commit message"`
- Ask Claude: "Help me commit my changes with a good commit message"

**Pushing changes:**
- Manual: `git push origin main`
- Ask Claude: "Help me push my latest changes to GitHub"

**Understanding errors:**
- Manual: Read git documentation or Stack Overflow
- Ask Claude: "I got this error: [paste error message]. What does it mean?"

**Project setup:**
- Manual: Research .gitignore templates online
- Ask Claude: "Create a .gitignore file for my Python project"

**The advantage of asking Claude:** It explains what the commands do, adapts to your specific situation, and helps you learn while getting things done.

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

---

## Troubleshooting Common Errors

### Terminal Prompt Issues

**Problem:** You see weird prompts like `dquote>` or `>` instead of your normal prompt

**Cause:** Usually from copying/pasting incomplete commands or commands with unmatched quotes

**Solution:**
1. Press **Ctrl+C** to cancel the current command
2. You should see your normal prompt return
3. Try typing the command again, carefully

### Copy/Paste Problems

**Problem:** Commands seem to work but produce unexpected results

**Cause:** Copying multiple lines at once or copying invisible characters

**Solutions:**
- **Only copy one line at a time** from these instructions
- If copying from a website, paste into a text editor first, then copy from there
- Type commands manually if copy/paste continues to cause issues

### "Command not found" Errors

**Problem:** `claude: command not found` even after installation

**Solutions:**
1. **Restart Terminal completely:** **Cmd+Q** then reopen (most common fix)
2. Check if installed correctly: `ls ~/.local/bin/claude`
3. If file exists, add to PATH:
   ```bash
   echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
   ```
4. Restart Terminal again

**Problem:** `gh: command not found`

**Solution:** Make sure Homebrew installed correctly:
```bash
brew --version
```
If this fails, Homebrew didn't install properly. Try the Homebrew installation step again.

### Git Configuration Errors

**Problem:** `Please tell me who you are` when trying to commit

**Solution:** You skipped the git configuration step. Go back to Step 2 in the repository creation section and set up your git identity.

**Problem:** Permission denied when pushing to GitHub

**Solution:** You haven't authenticated with GitHub. Run:
```bash
gh auth login
```

### When to Ask for Help

**Don't struggle alone!** If you encounter any error:

1. **Try the specific solutions above first**
2. **Ask Claude for help:** Start `claude` and describe the error you're seeing
3. **Remember:** Claude starts fresh each time, so describe your situation completely

**Example of asking Claude for help:**
```
I'm setting up git for the first time and got this error: [paste the exact error message here]
```

## Troubleshooting

### Installation Issues

#### Apple Command Line Tools Issues

**Problem:** Installation popup doesn't appear

- **Solution:** Tools may already be installed. Try `git --version` to check

#### Claude Code Installation Issues

**Problem:** "claude: command not found" after installation

- **Solution:** Restart Terminal completely (**Cmd+Q** then reopen)

#### Shell Environment Issues

**Problem:** Commands work in one terminal tab but not another

- **Solution:** Restart Terminal completely (**Cmd+Q** then reopen)

**Problem:** "command not found" after installation

- **Solution:** Run `source ~/.zprofile` then try the command again

#### Copy/Paste Issues in Terminal

**Problem:** **Cmd+V** doesn't work in Terminal

- **Solution:** Right-click and select "Paste" instead

### Common Mistakes to Avoid

1. **Using sudo** - Don't use `sudo` with these installation commands
2. **Not restarting Terminal** - Always restart Terminal (**Cmd+Q** then reopen) after installations
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
