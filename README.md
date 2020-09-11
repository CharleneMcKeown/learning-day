# Learning Day 

Work in progress! By the end of this workshop, you will have a blog running in Azure, deployed by GitHub Actions.  You will use core DevOps practices like continuous integration and continuous deployment to deploy new blog posts in a safe, repeatable and timely manner! 

This workshops requires no prior knowledge of git, GitHub or Azure. 

## pre-reqs

1. Azure Visual Studio subscription enabled
1. GitHub Account

## Set up your workspace

Codespaces are...

1. Visit https://aka.ms/vso-login to log in and get started. You will need to use the identity you used when creating your Visual Studio Subscription.

1. If you have never used Codespaces before, you'll need to create a plan. Click on **Create Codespace** to create a billing plan. 

    <img src="./images/create-cs0.PNG" alt="Create Codespace" width=800px />

1. Choose your Visual Studio Subscription and leave the location on West Europe. You can leave Advanced Options on their defaults. Click **Create**.
    <br>
    <img src="./images/create-cs1.PNG" alt="Create Billing Plan" width=400px />

1. Now you can create your Codespace. Give it a name, and then paste in the following link in the **Git Repository** field. 
    <br>
    ```
    https://github.com/gohugoio/hugo.git
    ```

    Leave everything else on their default settings. Click **Create**.
    <br>
     <img src="./images/create-cs.PNG" alt="Create Codespace" width=400px />   
    After a few moments, you should see your new Codespace ready to go! 

    <img src="./images/vscode.PNG" alt="Create Codespace" width=800px />

Let's spend a moment exploring the menu. If you have spent time using VS Code before and are comfortable, feel free to skip to the next step - [Setup Hugo](#Setup-Hugo).

todo.. vscode intro


## Setup Hugo

Hugo is a static site generator. A static site contains web pages with fixed content, and displays the same content to every user who visits the web page. Generally, static sites are made up of HTML pages that are stored as files in a file system somewhere. They can utilise CSS for styling and Javascript for more complex features like page transitions, menus and buttons.

Dynamic sites work differently. They generate their content based on making a database request. Think about a site like Netflix.com. You can log in, and you will see your library of favourite shows and movies to watch. Those are generated dynamically, and will be different for every user.

###### A History Lesson

Back in the early days of the web, static sites were prevalent. [Geocities, anyone?!](https://www.geocitiesarchive.org/index.html)

As time passed and e-commerce become more prevalent, dynamic sites backed by databases became the norm, allowing users to log into websites, place orders and write reviews. 

Static sites have had a resurgence over the last few years, especially with the entrance of static site generators. They make it really very easy to build your static site. They basically run a script that takes your content (in today's example, a blog post), combines that data with templates and outputs a folder with all of the HTML and assets you need to publish your site.

There are major advantages to using static sites.

- They are seriously fast to load (it's just HTML!)
- They are cheap to host (no database or backend server necessary)
- They are easy to backup and deploy (it's just HTML!)

Back to [Hugo!](https://gohugo.io/) It's open source, extremely popular, and it has a bunch of templates that you can use to really customise and make your website your own. Let's get started with it now.

1. Open a new terminal in VS Code by clicking on the hamburger menu icon and selecting Terminal > New Terminal.

    <br>
    <img src="./images/new-terminal.PNG" alt="New Terminal" width=600px />

1. Run the following command in the terminal that just opened at the bottom of your screen.

    ```
    go install --tags extended
    ```
    
    <img src="./images/install-hugo.PNG" alt="Install Hugo" width=600px />

    We are simply installing Hugo to our Codespace environment with this command. You will see a lot of scrolling text for a minute or two. Wait for this to complete, and then add Hugo to your path by typing the below command.

    ```
    export PATH=/go/bin:$PATH
    ```

    Verify the installation has been successful by typing the below:

    ```
    hugo version
    ```

    If successful, you will see the below image:

    <img src="./images/hugo.PNG" alt="Install Hugo" width=600px />


these steps if not using Azure Cloud Shell rather than codespaces:
```
mkdir src
cd src
git clone https://github.com/gohugoio/hugo.git
cd hugo
go install --tags extended
```

Verify you see Hugo
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

1. Create a new website by typing the following command into your terminal.
    ```
    hugo new site static-blog
    ```
    You should get a "Congratulations!" message: 
    <br>
    <img src="./images/hugo-new.PNG" alt="Create new Hugo site" width=600px />
    <br>
1. Next, let's add a theme to the website.
    
    ```
    cd static-blog
    git init
    git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
    ```

    The first command changes directory into the static site folder. The second command initiliazes this folder as a Git repository. The third command adds a reference to a specific theme for Hugo, which can be found in another Github repository. 
    <br>
    <img src="./images/git-init.PNG" alt="Git Init" width=600px />
    <br>

    We need to add our theme to a configuration file, which lets Hugo know what we want the site to look like:

    ```
    echo 'theme = "ananke"' >> config.toml
    ```
1. So far we have typed a bunch of commands. You have enough at this point to actually check out what your website looks like. Type one more command:

    ```
    hugo server -D
    ```
    ![hugo-server.PNG](./images/hugo-server.PNG) 

What is really cool about Codespaces is that we can actually visit your site through the magic of port forwarding! Your website is now running inside your Codespace. Click on the link in your terminal to visit it.

![hugo-site.PNG](./images/hugo-site.PNG) 


## Setup GitHub

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
