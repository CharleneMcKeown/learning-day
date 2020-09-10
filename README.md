# Learning Day 

Work in progress! By the end of this workshop, you will have a blog running in Azure, deployed by GitHub Actions.  You will use core DevOps practices like continuous integration and continuous deployment to deploy new blog posts in a safe, repeatable and timely manner! 

This workshops requires no prior knowledge of git, GitHub or Azure. 

## pre-reqs

1. Azure Visual Studio subscription enabled
1. GitHub Account

## Set up your workspace

Codespaces are...

1. Visit https://aka.ms/vso-login to log in and get started. You will need to use the identity you used when creating your Visual Studio Subscription.
<br>
1. If you have never used Codespaces before, you'll need to create a plan. Click on **Create Codespace** to create a billing plan. 

    ![create-cs0.PNG](./images/create-cs0.PNG)
<br>
1. Choose your Visual Studio Subscription and leave the location on West Europe. You can leave Advanced Options on their defaults. Click **Create**.
<br>

    ![create-cs1.PNG](./images/create-cs1.PNG)

1. Now you can create your Codespace. Give it a name, and then paste in the following link in the **Git Repository** field. 
```
https://github.com/gohugoio/hugo.git
```

Leave everything else on their default settings. Click **Create**.
    ![create-cs.PNG](./images/create-cs.PNG)

After a few moments, you should see your new Codespace ready to go! 

    ![vscode.PNG](./images/vscode.PNG)

Let's spend a moment exploring the menu. If you have spent time using VS Code before and are comfortable, feel free to skip to the next step.

todo.. vscode intro


1. Setup Hugo
```
go install --tags extended
```

```
export PATH=/go/bin:$PATH
```

Verify the installation:

```
hugo version
```


these steps if not using Azure Cloud Shell rather than codespaces:
```
mkdir src
cd src
git clone https://github.com/gohugoio/hugo.git
cd hugo
go install --tags extended
```
```
cd ..
cd ..
cd go/bin
```
#Verify you see Hugo
#add it to path:
```
PATH=$PATH:~/go/bin
```
```
cd ..
cd..
hugo version
```
1. explore with vs code in browser

## Step 2

1. Create a new website
```
hugo new site static-blog
```

1. Add a theme
```
cd static-blog
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```
```
echo 'theme = "ananke"' >> config.toml
```

1. open new browser - type repo.new
1. create a new repo - but don't initialize it yet. copy the commands to 'push existing repo'

```
git remote add origin https://github.com/youraccount/yourrepo.git
git push -u origin master
```
1. create a personal access token
1. come back to cloud shell
1. configure git
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

##### need a step to setup credential manager?

1. explain git status, add and commit process
```
git status
git add .
git commit -m "added a theme"
```

1. git push

```
git remote add origin https://github.com/youraccount/your-repo.git
git push -u origin master
```
If it's your first time using GitHub from Cloud Shell, you will be prompted to login. Use your account name and the personal access token you generated earlier.
TADA!

## Step 3

1. Create static site in Azure
1. point it to your new repo
1. navigate to new repo
1. explore .github folder 
1. explore running Action

## Step 4 

1. checkout your empty static site!
1. in cloud shell write a blog post
```
hugo new posts/my-first-post.md
```
1. ensure draft:false
1. configure config.toml to change site name
1. git pull first
1. git add .
1. git commit and push - CI in action
1. observe the workflow and deployment - CD

##### Encourage people to share their first blog post on LinkedIn & Twitter with a #LearningDay? 

##### Could have a Logic App triggering on when it detects a new post 