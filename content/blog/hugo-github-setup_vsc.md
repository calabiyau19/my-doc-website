---
title: "Hugo + GitHub Pages + CI/CD: A Complete Guide"
date: 2025-02-06T12:00:00
draft: false
---

# 🚀 Hugo + GitHub Pages + CI/CD: A Complete Guide  

This guide walks you through **setting up Hugo**, **deploying to GitHub Pages**, and **automating deployment with GitHub Actions**.  

## 📌 Prerequisites  
- **OS**: Xubuntu Minimal (on LPT-DELL)  
- **GitHub Account**: `calabiyau19`  
- **Project Name**: `my-doc-website`  
- **Local Directory**: `/home/mark/my-doc-website`  

---

## 🛠 Step 1: Start Fresh  

Before setting up Hugo, we need to **delete any old files and repositories** from a previous attempt.  

### **1.1 Delete the Local Hugo Project**  
Run the following command on LPT-DELL to remove the old project directory:  

```sh
rm -rf ~/my-doc-website

Verify that the folder has been removed by listing the home directory:

sh
Copy
Edit
ls ~/

1.2 Delete the GitHub Repository
Go to GitHub.com and log in.
Navigate to Repositories and find my-doc-website.
Click Settings, scroll down, and click Delete this repository.
Confirm the deletion.
📦 Step 2: Create a New GitHub Repository
Go to GitHub.com → Click + → New repository
Name it: my-doc-website
Set it as Public
Check "Add a README file"
Click Create repository
💻 Step 3: Clone Repository to Local Machine
Navigate to where you want to store the project:

sh
Copy
Edit
cd /home/mark
Clone your new repository:

sh
Copy
Edit
git clone https://github.com/calabiyau19/my-doc-website.git
Enter the directory:

sh
Copy
Edit
cd my-doc-website
📥 Step 4: Install Necessary Software
4.1 Update the System
sh
Copy
Edit
sudo apt update && sudo apt upgrade -y
4.2 Install Git
Check if Git is installed:

sh
Copy
Edit
git --version
If not installed, run:

sh
Copy
Edit
sudo apt install git -y
🚀 Step 5: Install Hugo
sh
Copy
Edit
cd /home/mark
sudo dpkg -i hugo_extended_0.143.1_linux-amd64.deb
Verify installation:

sh
Copy
Edit
hugo version
📂 Step 6: Initialize Hugo Site
sh
Copy
Edit
cd /home/mark/my-doc-website
hugo new site . --force
ls -l
🎨 Step 7: Install and Configure a Hugo Theme
7.1 Add the Theme
sh
Copy
Edit
git submodule add https://github.com/lxndrblz/anatole.git themes/anatole
ls themes
7.2 Configure Hugo (hugo.toml)
sh
Copy
Edit
nano hugo.toml
Paste this:

toml
Copy
Edit
baseURL = "https://calabiyau19.github.io/my-doc-website/"
languageCode = "en-us"
title = "My Doc Website"
theme = "anatole"

[params]
  author = "calabiyau19"
  description = "A personal documentation website"
  enableEmoji = true
Save & Exit: CTRL+X → Y → ENTER

🖼 Step 8: Add a Profile Picture
8.1 Move Image to Static Folder
sh
Copy
Edit
mkdir -p static/images
cp /path/to/your-image.jpg static/images/profile.jpg
ls static/images/
8.2 Update hugo.toml
sh
Copy
Edit
nano hugo.toml
Add this line:

toml
Copy
Edit
profilePicture = "images/profile.jpg"
Save & Exit.

🔍 Step 9: Run Hugo Locally
sh
Copy
Edit
hugo server -D
Visit:
👉 http://localhost:1313/my-doc-website/

📝 Step 10: Add a First Blog Post
10.1 Create the Post
sh
Copy
Edit
hugo new blog/my-first-post.md
10.2 Edit the Post
sh
Copy
Edit
nano content/blog/my-first-post.md
Modify:

md
Copy
Edit
---
title: "My First Post"
date: 2025-02-06T12:00:00
draft: false
---

# Welcome to My Blog

This is my first post using Hugo! 🚀
Save & Exit.

10.3 Restart Hugo
sh
Copy
Edit
hugo server -D
Verify the post is visible.

💾 Step 11: Commit Changes to Git
sh
Copy
Edit
git add .
git commit -m "Initial Hugo setup with first blog post and profile picture"
git push origin main
🔑 Step 12: Set Up SSH Authentication
12.1 Generate SSH Key
sh
Copy
Edit
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
Press ENTER to accept defaults.

12.2 Add Key to GitHub
sh
Copy
Edit
cat ~/.ssh/id_rsa.pub
Copy the output → GitHub Settings → SSH Keys → Add New Key

12.3 Update Git Remote
sh
Copy
Edit
git remote set-url origin git@github.com:calabiyau19/my-doc-website.git
🚀 Step 13: Enable GitHub Pages
GitHub Repository → Settings
Click Pages (left menu)
Change Branch to gh-pages → Save
🤖 Step 14: Set Up GitHub Actions (CI/CD)
14.1 Create Workflow File
sh
Copy
Edit
mkdir -p .github/workflows
nano .github/workflows/deploy.yml
Paste:

yaml
Copy
Edit
name: Deploy Hugo Site
on:
  push:
    branches:
      - main
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4
        with:
          submodules: true
          fetch-depth: 0

      - name: Install Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: "latest"
          extended: true

      - name: Build Site
        run: hugo --minify

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: gh-pages
Save & Exit.

14.2 Commit & Push Workflow
sh
Copy
Edit
git add .github/workflows/deploy.yml
git commit -m "Add GitHub Actions workflow"
git push origin main
🌍 Step 15: Verify Deployment
Check GitHub Actions:
👉 GitHub Repository → Actions
Visit Your Live Site:
👉 https://calabiyau19.github.io/my-doc-website/
🎉 Done! Your site is now live with full CI/CD automation! 🚀

pgsql
Copy
Edit

✅ **This keeps all your code exactly as it was while only adjusting Step 1. Now just copy and paste this into your Hugo post!** 😊






