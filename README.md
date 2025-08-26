# GitHub Tutorial

This guide is for members of the Global Environmental Change Lab at UC Davis working on developing and using code, primarly on the FARM Linux-based supercomputing cluster managed by the College of Agricultural and Environmental Sciences at UC Davis, but it is also useful if working with code on your desktop/laptop.
It walks you through how to set up a GitHub account, set up Git, create a new repository, contribute code, and stay in sync when collaborating.

---

## 1. Create a GitHub Account and Join the UCDglobalchange Organization

1. Go to [https://github.com](https://github.com) and create a GitHub account if you don’t already have one.
2. Send your GitHub username to the lab manager or PI to receive an invitation to the **UCDglobalchange** organization.
3. Accept the invitation via email or by logging into GitHub and checking [https://github.com/notifications](https://github.com/notifications).

---

## 2. Create the Repository on GitHub

1. Go to [https://github.com](https://github.com) and log in.
2. Click the **"+"** icon in the upper right, then select **"New repository"**.
3. Fill in the details:

   * **Repository name**: `test-repo`
   * **Optional**: Add a short description
   * Choose **Private** or **Public** depending on access needs
   * ✅ Check **"Add a README file"**
4. Click **"Create repository"**

---

## 3. Set Up Git on Your Local Machine (it is already installed on FARM)

### Install Git:

```bash
sudo apt install git    # On Linux
brew install git        # On macOS
```

### Configure Git with your identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

---

## 4. Set Up SSH Access to GitHub on FARM (One-Time Setup)

### Check if you already have an SSH key:

```bash
ls ~/.ssh
```

Look for files named `id_ed25519` or `id_rsa`. If you don't see them:

### Generate a new SSH key:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Press Enter to accept the default file location. You can optionally set a passphrase.

### Add the SSH key to GitHub:

```bash
cat ~/.ssh/id_ed25519.pub
```

1. Copy the output.
2. Go to [https://github.com/settings/keys](https://github.com/settings/keys)
3. Click **"New SSH key"**, give it a name (e.g., "FARM"), and paste the key.

### Test your SSH connection:

```bash
ssh -T git@github.com
```

If successful, you’ll see:

> Hi your\_username! You've successfully authenticated, but GitHub does not provide shell access.

---

## 5. Clone the GitHub Repository to FARM (or to Your Local Machine)

```bash
git clone git@github.com:UCDglobalchange/test-repo.git
cd test-repo
```

---

## 6. Add Your Existing Code

If your scripts are in another folder, copy them into the repository:

```bash
cp -r /path/to/your/code/* .
```

If you're starting in a non-Git folder and want to connect it to GitHub:

```bash
git init
git remote add origin git@github.com:UCDglobalchange/test-repo.git
```

---

## 7. Commit and Push Your Code

```bash
git add .
git commit -m "Initial commit of preprocessing scripts"
git push origin main
```

---

## 8. Keeping Your FARM Copy (or Local Copy) Up to Date (Pull Changes)

If other people are working on the repo (or you're working from multiple machines), always **pull new changes before working**:

```bash
git pull origin main --rebase
```

> 🔁 **Best Practice:** Do this at the start of each work session, and always before pushing.

---

## 9. Daily Git Workflow Summary

```bash
# Step 1: Get the latest version
git pull origin main --rebase

# Step 2: Do your work and modify files

# Step 3: Stage your changes
git add .

# Step 4: Commit with a message
git commit -m "Short description of changes"

# Step 5: Push your changes to GitHub
git push origin main
```

---

## 10. Resetting Local Repository to Match Remote

If you want to discard all your local changes and make your local repository exactly match the remote `main` branch, follow these steps. This is useful when things get messy or out of sync, and you just want to start fresh without recloning the repo.

⚠️ **Warning**: This will permanently delete local changes that haven't been committed or pushed.

### Step-by-step instructions:

```bash
# Step 1: Discard any local changes
git reset --hard

# Step 2: Remove any untracked files or directories (e.g., temp files)
git clean -fd

# Step 3: Fetch the latest from the remote repository
git fetch origin

# Step 4: Reset your local main branch to match the remote
git reset --hard origin/main
```

---

## 11. Handling Push Errors

If you see this error:

```bash
error: failed to push some refs to 'github.com:UCDglobalchange/test-repo.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
```

It means someone else pushed updates to GitHub. Run:

```bash
git pull origin main --rebase
```

Then push again:

```bash
git push origin main
```

If the same files were changed both remotely and locally, you'll need to resolve the conflicts manually.
Git will tell you which files need attention.

---

## 12. Repository Structure

It is helpful to maintain a consistent directory structure across projects. A suggested format is:

```
test-repo/
├── data/          # Input data files (do not commit large files)
├── scripts/       # Python or shell scripts used in processing
├── results/       # Output files, usually excluded from Git
├── docs/          # Documentation or notes
├── README.md      # Project description and instructions
├── .gitignore     # Files or folders to exclude from Git
└── LICENSE        # Licensing information
```

Feel free to adjust this structure to fit the needs of your specific project. Just be consistent and clear in how files are organized.

## 13. Managing Branches and Resolving Merge Conflicts

### Working with Branches

Using branches is helpful when making experimental changes or working on features separately from the main codebase.

```bash
# Create and switch to a new branch
git checkout -b my-feature-branch

# Do your work and commit as usual
git add .
git commit -m "Work on my new feature"

# Push the branch to GitHub
git push origin my-feature-branch
```

Once your changes are reviewed or complete, you can merge them into the `main` branch:

```bash
# Switch to main branch
git checkout main

# Pull the latest changes
git pull origin main

# Merge your feature branch
git merge my-feature-branch

# Push the updated main branch
git push origin main
```

### Resolving Merge Conflicts

If the same lines in the same file were changed in both branches (or on GitHub vs your local copy), Git will pause the merge and mark the conflict:

```bash
git pull origin main --rebase
```

You will see conflict markers like this in the file:

```
<<<<<<< HEAD
Your local changes
=======
Changes from GitHub
>>>>>>> origin/main
```

Edit the file to keep what you want, then mark the conflict as resolved:

```bash
git add conflicted_file.py

# If you were rebasing:
git rebase --continue

# Or if you were merging:
git commit -m "Resolve merge conflict"
```

---

## 14. Optional: Add a .gitignore

Add a `.gitignore` file for Python projects:

```bash
curl https://raw.githubusercontent.com/github/gitignore/main/Python.gitignore -o .gitignore
git add .gitignore
git commit -m "Add .gitignore"
git push origin main
```

You should use `.gitignore` to exclude files that don't need to be tracked, such as large data files, compiled code, temporary logs, or machine-specific settings.

**Example .gitignore entries**:

````
*.nc
*.log
__pycache__/
temp/
````

## 15. Add a License

Add a license (MIT recommended for academic code):

```bash
echo "MIT License..." > LICENSE
git add LICENSE
git commit -m "Add license"
git push origin main
```
