To set up Git in Obsidian for version control, you’ll need to install Git on your computer and use either the Obsidian Git plugin or run Git commands manually. Here’s a step-by-step guide:

### 1. Install Git
If you haven’t already installed Git, download and install it:

- **Windows:** [Download Git for Windows](https://gitforwindows.org/), then follow the installation instructions.
- **Mac:** Git is usually pre-installed, but you can download the latest version from [git-scm.com](https://git-scm.com/).
- **Linux:** Use your package manager to install Git. For example: `sudo apt install git` on Ubuntu.

![](IMG/Set%20up%20Git/Pasted%20image%2020250224185033.png)
### 2. Configure Git
After installing Git, set up your global username and email (needed for version control).

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
![](IMG/Set%20up%20Git/Pasted%20image%2020250224185104.png)
### 3. Initialize a Git Repository in Your Obsidian Vault
1. Open a terminal (Command Prompt, Git Bash, Terminal, etc.).
2. Navigate to your Obsidian vault folder.

   ```bash
   cd path/to/your/obsidian/vault
   ```



3. Initialize a Git repository in the vault:

   ```bash
   git init
   ```

4. Create a `.gitignore` file to exclude files or folders (e.g., Obsidian’s workspace settings).

   ```bash
   echo "/.obsidian/" >> .gitignore
   ```

![](IMG/Set%20up%20Git/Pasted%20image%2020250224190405.png)

![](IMG/Set%20up%20Git/Pasted%20image%2020250224190527.png)

### 4. Commit Changes to Your Repository
1. **Add files** to the repository:

   ```bash
   git add .
   ```

2. **Commit** the changes:

   ```bash
   git commit -m "Initial commit"
   ```

![](IMG/Set%20up%20Git/Pasted%20image%2020250224190507.png)

### 5. Install the Obsidian Git Plugin (Optional)
To automate Git tasks, you can install the Obsidian Git plugin, which provides automatic commits, push, and pull:

1. Open **Settings** in Obsidian, go to **Community plugins**, and turn off Safe mode if it’s enabled.
2. Search for **Obsidian Git** in the community plugin browser and install it.
3. Enable the plugin and configure its settings:
   - Set up **auto-pull** and **auto-push** to automatically sync changes.
   - Configure **commit interval** (e.g., every 10 minutes) to save changes regularly.

### 6. Sync with a Remote Repository (Optional)
If you want to back up your vault online, set up a remote repository (e.g., on GitHub, GitLab):

1. Create a new repository on GitHub/GitLab.
2. Link it to your Obsidian vault repository:

   ```bash
   git remote add origin https://github.com/yourusername/your-repo.git
   ```

![](IMG/Set%20up%20Git/Pasted%20image%2020250224190611.png)
3. **Push** your local repository to the remote:

   ```bash
   git push -u origin main
   ```

Now, you’ll have Git version control set up for your Obsidian vault, with the option to automate it via the Obsidian Git plugin.



```r
If you get any error like this:
```
![](IMG/Set%20up%20Git/Pasted%20image%2020250224190627.png)

run :

```powershell
git pull origin main --rebase

# Add all changes:
	git add .

# Commit the changes:
	git commit -m "Save changes before pull with rebase"

# Pull with Rebase: After committing, you can
	git pull --rebase origin main

#Push the Changes: Once the pull with rebase completes successfully, push your changes:
	git push origin main
```

![](IMG/Set%20up%20Git/Pasted%20image%2020250224190640.png)
