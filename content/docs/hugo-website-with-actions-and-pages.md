---
title: "How to Build Hugo Website"
date: 2025-02-18T12:00:00Z
draft: false
---


#### A step-by-step guide to deploying a static Hugo site with full CI/CD using GitHub Actions and Pages

### **Prerequisites**

* A GitHub account  
* A Linux machine (tested on Xubuntu Minimal)  
* Basic knowledge of the command line

### **Step 1: Remove Any Previous Setup**

sh  
CopyEdit  
`rm -rf ~/my-doc-website`  

Then, delete any existing GitHub repository for the project.

### **Step 2: Create a New GitHub Repository**

Go to GitHub, create a new repository named **my-doc-website**.

### **Step 3: Clone the Repository to Your Local Machine**

sh  
CopyEdit  
`cd ~`    
`git clone git@github.com:calabiyau19/my-doc-website.git`    
`cd my-doc-website`  

### **Step 4: Install Necessary Software**

sh  
CopyEdit  
`sudo apt update && sudo apt upgrade -y`    
`sudo apt install git -y`    
`git --version`  

### **Step 5: Install Hugo**

sh  
CopyEdit  
`sudo dpkg -i hugo_extended_0.143.1_linux-amd64.deb`    
`hugo version`  

### **Step 6: Add the Anatole Theme**

sh  
CopyEdit  
`git submodule add https://github.com/lxndrblz/anatole.git themes/anatole`    
`ls themes`  

### **Step 7: Configure Hugo (`hugo.toml`)**

sh  
CopyEdit  
`nano hugo.toml`  

Replace contents with:

toml  
CopyEdit  
`baseURL = "https://calabiyau19.github.io/my-doc-website/"`    
`languageCode = "en-us"`    
`title = "My Doc Website"`    
`theme = "anatole"`  

### **Step 8: Start Hugo Locally**

sh  
CopyEdit  
`hugo server -D`  

### **Step 9: Add a Profile Picture**

sh  
CopyEdit  
`mkdir -p static/images`    
`cp ~/Downloads/profile.jpg static/images/profile.jpg`  

### **Step 10: Add a First Blog Post**

sh  
CopyEdit  
`hugo new blog/my-first-post.md`    
`nano content/blog/my-first-post.md`  

### **Step 11: Commit and Push the Site to GitHub**

sh  
CopyEdit  
`git add .`    
`git commit -m "Initial Hugo setup"`    
`git push origin main`  

### **Step 12: Set Up GitHub Pages**

Go to **GitHub repository → Settings → Pages** → Set branch to **main** → Save.

### **Step 13: Set Up GitHub Actions for Deployment**

sh  
CopyEdit  
`mkdir -p .github/workflows`    
`nano .github/workflows/deploy.yml`  

### **Step 14: Commit and Push GitHub Actions Workflow**

sh  
CopyEdit  
`git add .github/workflows/deploy.yml`    
`git commit -m "Add GitHub Actions workflow"`    
`git push origin main`  

### **Step 15: Enable GitHub Actions Write Permissions**

Go to **GitHub repository → Settings → Actions → Set permissions**.

### **Step 16: Manually Create the `gh-pages` Branch**

sh  
CopyEdit  
`git checkout --orphan gh-pages`    
`git rm -rf .`    
`git commit --allow-empty -m "Initialize gh-pages branch"`    
`git push origin gh-pages`    
`git checkout main`  

### **Step 17: Trigger Deployment Again**

sh  
CopyEdit  
`nano hugo.toml`    
`# Add a small change`  

`git add hugo.toml`    
`git commit -m "Trigger new deployment"`    
`git push origin main`  

### **Step 18: Verify Deployment**

Go to **GitHub Actions tab** → Ensure deployment is successful.  
Visit: [https://calabiyau19.github.io/my-doc-website/](https://calabiyau19.github.io/my-doc-website/)

🎉 **Done\!** Your Hugo site is fully deployed with CI/CD