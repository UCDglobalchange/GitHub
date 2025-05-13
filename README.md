# GitHub Tutorial members of the Global Environmental Change Lab at UC Davis

This guide is for lab members working with the GDSTEM-preprocessing repository.
It walks you through how to set up Git, clone the repository, contribute code, and stay in sync when collaborating.

---

## 1. Create the Repository on GitHub

1. Go to [https://github.com](https://github.com) and log in.
2. Click the **"+"** icon in the upper right, then select **"New repository"**.
3. Fill in the details:

   * **Repository name**: `GDSTEM-preprocessing`
   * **Optional**: Add a short description
   * Choose **Private** or **Public** depending on access needs
   * ✅ Check **"Add a README file"**
4. Click **"Create repository"**

---

## 2. Set Up Git on Your Local Machine or FARM (if not already installed)

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

## 3. Clone the GitHub Repository to Your Local Machine

```bash
git clone git@github.com:UCDglobalchange/GDSTEM-preprocessing.git
cd GDSTEM-preprocessing
```

---

## 4. Add Your Existing Code

If your scripts are in another folder, copy them into the repository:

```bash
cp -r /path/to/your/code/* .
```

If you're starting in a non-Git folder and want to connect it to GitHub:

```bash
git init
git remote add origin git@github.com:UCDglobalchange/GDSTEM-preprocessing.git
```

---

## 5. Commit and Push Your Code

```bash
git add .
git commit -m "Initial commit of preprocessing scripts"
git push origin main
```

---

## 6. Keeping Your Local Copy Up to Date (Pull Changes)

If other people are working on the repo (or you're working from multiple machines), always **pull new changes before working**:

```bash
git pull origin main --rebase
```

> 🔁 **Best Practice:** Do this at the start of each work session, and always before pushing.

---

## 7. Daily Git Workflow Summary

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

## 8. Handling Push Errors

If you see this error:

```bash
error: failed to push some refs to 'github.com:UCDglobalchange/GDSTEM-preprocessing.git'
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

## 9. Optional: Add a .gitignore and LICENSE

Add a `.gitignore` file for Python projects:

```bash
curl https://raw.githubusercontent.com/github/gitignore/main/Python.gitignore -o .gitignore
git add .gitignore
git commit -m "Add .gitignore"
git push origin main
```

Add a license (MIT recommended for academic code):

```bash
echo "MIT License..." > LICENSE
git add LICENSE
git commit -m "Add license"
git push origin main
```

---

Let me know if you'd like help with GitHub issues, managing branches, or resolving merge conflicts!
