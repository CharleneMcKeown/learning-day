# Microsoft UK Learning Day DevOps WorkShop (September 24th 2020)

By the end of this workshop, you will have a blog running in Azure, deployed by GitHub Actions.  You will use core DevOps practices like continuous integration and continuous deployment to deploy new blog posts in a safe, repeatable and timely manner! 

This workshops requires no prior knowledge of git, GitHub or Azure. 

<img src="./images/flow.PNG" />

## Pre-reqs

1. Azure Visual Studio Subscription enabled
    - Go to [http://my.visualstudio.com/benefits](http://my.visualstudio.com/benefits)

1. GitHub Account
    - Go to [https://github.com/join](https://github.com/join)

## Step 1 - Set up your workspace

[Codespaces](https://visualstudio.microsoft.com/services/visual-studio-codespaces/) is a development environment that you can use with only a web browser. It is cloud based, which means you can connect to it from anywhere, and you can create one in just a minute or two.

It's a really quick and easy way to start developing software or working on projects, without having to install software on your own computer. Codespaces provides you with Visual Studio Code and is configured to run git. You can even configure it with other tools and dependencies you need for your specific project.


1. Visit [https://aka.ms/vso-login](https://aka.ms/vso-login) to log in and get started. You will need to use the identity you used when creating your Visual Studio Subscription.

1. If you have never used Codespaces before, you'll need to create a plan. Click on **Create Codespace** to create a billing plan. 

    <img src="./images/create-cs0.PNG" alt="Create Codespace" width=800px />

1. Choose your Visual Studio Subscription and leave the location on West Europe. You can leave Advanced Options on their defaults. Click **Create**.
    <br>
    <img src="./images/create-cs1.PNG" alt="Create Billing Plan" width=400px />

    >Note: If you get a **TimedoutWaitingForRegisterResourceProvider** error, click **Cancel** and try again. Sometimes there is a delay in the background whilst Codespaces is enabled on your Azure subscription.

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

On the left hand side, you will see a list of files - these files automatically got added to your codespace based on the Hugo GitHub repo you specified earlier. 


## Step 2 - Setup Hugo

[Hugo](https://gohugo.io/) is a static site generator. A static site contains web pages with fixed content, and displays the same content to every user who visits the web page. Generally, static sites are made up of HTML pages that are stored as files in a file system somewhere. They can utilise CSS for styling and Javascript for more complex features like page transitions, menus and buttons.

Dynamic sites work differently. They generate their content based on making a database request. Think about a site like Netflix.com. You can log in, and you will see your library of favourite shows and movies to watch. Those are generated dynamically, and will be different for every user.

###### A History Lesson

Back in the early days of the web, static sites were common. [Geocities, anyone?!](https://www.geocitiesarchive.org/index.html)

As time passed and e-commerce become more prevalent, dynamic sites backed by databases became the norm, allowing users to log into websites, place orders and write reviews. 

Static sites have had a resurgence over the last few years, especially with the entrance of static site generators. They make it really very easy to build your static site. They basically run a script that takes your content (in today's example, a blog post), combines that data with templates and outputs a folder with all of the HTML and assets you need to publish your site.

There are major advantages to using static sites.

- They are seriously fast to load (it's just HTML!)
- They are cheap to host (no database or backend server necessary)
- They are easy to backup and deploy (it's just HTML!)

Back to Hugo. It's open source, extremely popular, and it has a bunch of templates that you can use to really customise and make your website your own. Let's get started with it now.

1. Open a new terminal in VS Code by clicking on the hamburger menu icon and selecting Terminal > New Terminal.

    <br>
    <img src="./images/new-terminal.PNG" alt="New Terminal" width=600px />

1. Run the following command in the terminal that just opened at the bottom of your screen.

    ```
    go install --tags extended
    ```
    
    <img src="./images/install-hugo.PNG" alt="Install Hugo" width=600px />

    You are simply installing Hugo to your Codespace environment with this command. You will see a lot of scrolling text for a minute or two. Wait for this to complete, and then add Hugo to your path by typing the below command.

    ```
    export PATH=/go/bin:$PATH
    ```

    Verify the installation has been successful by typing the below:

    ```
    hugo version
    ```

    If successful, you will see the below image:

    <img src="./images/hugo.PNG" alt="Install Hugo" width=600px />


## Step 3 - Create a Hugo website

1. Create a new website by typing the following command into your terminal.
    ```
    hugo new site static-blog
    ```
    You should get a "Congratulations!" message: 
    <br>
    <img src="./images/hugo-new.PNG" alt="Create new Hugo site" width=600px />
    <br>
1. Next, let's add a theme to the website by running the following commands:
    
    ```
    cd static-blog
    git init
    git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
    ```

    The first command changes directory into the static site folder. The second command initializes this folder as a git repository. The third command adds a reference to a specific theme for Hugo, which can be found in another Github repository. 
    <br>
    <img src="./images/git-init.PNG" alt="Git Init" width=600px />
    <br>

    You need to add your theme to a configuration file, which lets Hugo know what you want the site to look like. To do this, run this command:

    ```
    echo 'theme = "ananke"' >> config.toml
    ```
1. You have enough at this point to actually check out what your website looks like. Type one more command:

    ```
    hugo server -D
    ```
    <img src="./images/hugo-server.PNG" alt="Hugo server" width=600px />

What is really cool about Codespaces is that you can actually visit your site through the magic of port forwarding! Your website is now running inside your Codespace. Click on the link in your terminal to visit it.

<img src="./images/hugo-site.PNG" alt="Hugo site" width=600px />


## Step 4 - Setup GitHub

1. In your Codespace terminal, type:

    ```
    git status
    ```
    <img src="./images/git-status.PNG" alt="Git Status"/>

    This is a useful command, and one to use often. It tells you a few things about your git repository. 

    - You are on the master (main) branch
    - You haven't made any commits yet
    - You have changes that need to be committed
    - You have untracked files


    >Note: If you need a quick primer on git, please check out [FreeCodeCamp](https://www.freecodecamp.org/news/learn-the-basics-of-git-in-under-10-minutes-da548267cc91/) which is about a ten minute read. 

1. In your Codespace terminal, type each command below. Be sure to replace your email and your name.

    ```
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"
    git add .
    git commit -m 'adding my static site files'
    ```
    What you have done here is asked git to track the files and folders that are necessary to build your static site. You have also configured git to use your name and email, so any change you make can be traced back to you. This is really useful when working with other people on the same code base.

    <img src="./images/git-commit.PNG" alt="Git commit"/>

    Now that you have git configured locally, you need to create a repository to host your code. You shouldn't rely on keeping your code locally or in a Codespace. If you were working on a team blog, or building a bigger website, you need to be able to collaborate with others - this is where GitHub repositories come in.

1. Open up a new browser and type **repo.new** - this is actually a domain owned by GitHub that gives you a nice shortcut to create a new repo! You may be prompted to log in or create an account if you haven't done so already.

1. Create a new repo called learningday - but don't initialize it yet (you are going to push your existing repository instead). Click **Create repository**.

    >Note: In the image below, you will see marketplace apps. Don't worry, you're not expected to have these GitHub apps for this workshop.

    <img src="./images/new-repo.PNG" alt="New repo"/>

    Once you hit the screen below, go back to your Codespace.

    <img src="./images/new-repo2.PNG" alt="New repo"/>

1. Copy the below commands into your Codespace terminal, replacing **youraccount** with your GitHub account name.

    ```
    git remote add origin https://github.com/youraccount/learningday.git
    git push -u origin master
    ```
    You will be prompted to authorize Codespaces with your GitHub account - go ahead and do this.

    <img src="./images/authorise-vs.PNG" alt="Authorise VS"/>

    Afterwards, you should see all of your files in the remote repo:

    <img src="./images/repo.PNG" alt="repo"/>


## Step 5 - Publish your static site

Now that you have the barebones of your website, and a repo hosting your code, you need somewhere to publish that code to.

[Azure Static Web Apps](https://azure.microsoft.com/en-us/services/app-service/static/) is a service that automatically builds and deploys web apps to Azure from a GitHub repository.

1. Navigate to [http://portal.azure.com](http://portal.azure.com) and log in.
1. On the homepage, search for **Static Web Apps** and click on the marketplace icon.
    <img src="./images/create-static-site.PNG" alt="Create static web app"/>
1. Fill in the following details:

    - Subscription: Choose your **Visual Studio Subscription**
    - Resource Group:Create a new one called **learningday-rg**
    - Static Web App Name: **learningday**
    - Region: **West Europe**
        <img src="./images/create-static-site2.PNG" alt="Create static web app"/>
1. Click on **Sign in with GitHub** and authorise connection.
1. Fill in the following details:

    - Organisation: **Your GitHub Account name**
    - Repository: **learningday**
    - Branch: **master**
    - Build Presets: **Hugo**
    - App Location: **/**
    - Api Location: **Leave this blank**
    - App artifact location: **public**

    <img src="./images/create-static-site3.PNG" alt="Create static web app"/>

1. Click **Review + create**

1. Head back to your GitHub repo and refresh the page. You will see a new folder in your repo called **.github/workflows**
    <img src="./images/workflowfolder.PNG" alt="workflow"/>

    When you created the static web app just now, Azure pushed a new commit to your repo which contained a file called **azure-static-web-apps-yourappname.yml**. 

    This is a [workflow](https://docs.github.com/en/actions/configuring-and-managing-workflows) file, and it contains all the instructions needed to build and deploy your static web app to Azure. 
    
    [GitHub Actions](https://docs.github.com/en/actions) uses these files to build end-to-end continuous integration (CI) and continuous deployment (CD) capabilities directly in your repository.

1. Click on the **Actions** tab in your repo. You might see that that the workflow is still running. Click on it to view the live logs.

    <img src="./images/action.PNG" alt="action"/>

    In this example, the workflow is on the **Build and Deploy** job. 

    <img src="./images/action2.PNG" alt="action"/>

    Wait for the workflow to successfully complete.

1. Go back to Azure and find your recently deployed static web app. You can search **Static Web App** in the search bar of the Azure Portal if you can't find it. Once found, click on it and find the URL of your web app (it's in the far right of the screenshot below).

1. Click on it, and you should see your empty blog. Time to update it!

    <img src="./images/staticwebapp.PNG" alt="Static Web App"/>

## Step 6 - Use CI & CD to update the blog

**Continuous integration** is the process of automating the build and testing of code every time a change is committed to version control.

**Continuous deployment** is the process of deploying software frequently, and in an automated way.

You are going to make some changes to your blog now, and commit those changes to your GitHub repo. Then, automatically, GitHub Actions will build your blog and deploy it to Azure.

In a more real world scenario, you could run tests to make sure the blog was still in a deployable state, and not broken by any erroneous changes.

1. Go back to your Codespace terminal.

    >Note: If your Codespace has timed out, make sure you change directory back into static-blog by typing **cd static-blog**.

1. Create a new post by typing the following:
    ```
    hugo new posts/my-first-post.md
    ```

1. Find the file you just created in the file explorer to the left. It will be in **static-blog/content/posts**.
    <img src="./images/first-post.PNG" alt="First post"/>

1. Set **draft: false** and write some text below the second **---**. This will be your first post!

    If you are stuck for inspiration, you could blog about a new announcement from Ignite 2020 that really impressed you!

    Once you are finished, save the post by typing Ctrl + S.

1. Find the config.toml (it will be in the root of your static-blog folder) and change the title name to whatever you want it to be, then save it with Ctrl + S.
    <img src="./images/title.PNG" alt="title"/>

1. In your terminal, type:

    ```
    git pull
    ```
    This command pulls down any changes from your remote repo into your local repo. You will see that the .github folder now exists locally, along with your workflow file. 

    Always do a git pull before a git push!

1. In your terminal, type: 
    ```
    git add .
    ```
    Remember, this commands adds any new or untracked files we created to git. 

1. Now you can practice continuous integration! You have made changes locally, so you can now commit and push those to your GitHub repo. Type:

    ```
    git commit -m "added my first blog post"
    git push
    ```
1. Go back to your GitHub repo and observe the updated files. You should now see a content/posts directory which Hugo created for you locally when you created your first post.

    <img src="./images/content-posts.PNG" alt="content/posts"/>

1. Click on **Actions** to observe your workflow running for a second time. You can see that the workflow tells you that it is linked to the commit you just made (added my first blog post). Optionally, click on it to view the logs again.

    <img src="./images/workflow2.PNG" alt="content/posts"/>

1. Finally, once the workflow completes successfully, refresh your static web app. You should see an updated title and your first post!

    <img src="./images/blog.PNG" alt="blog"/>

### Wrap Up

Well done, you made it to the end!

At this point you should have your own blog running in Azure, with version control and a CI/CD pipeline set up for automated deployment.

You learned:

1. How to work with version control using git and GitHub
1. How to develop from anywhere using Codespaces
1. How to navigate the Azure portal and create resources
1. About the fundamentals of Continuous Integration and Continuous Deployment

### Next Steps

- **Share** your blog on LinkedIn! 

- **Create** more content - a good place to start would be sharing your thoughts on the recent Ignite news.

- **Customise** it even more by installing a new [theme](https://themes.gohugo.io/) or assign a custom domain to your blog. You need to have purchased your own domain and then follow this [guide](https://docs.microsoft.com/en-us/azure/static-web-apps/custom-domain).

- **Explore** the use of [trunk based development](https://trunkbaseddevelopment.com/#one-line-summary) to protect your main branch

- **Improve** this workshop! [Fork it](https://guides.github.com/activities/forking/) and contribute back to the community.

- **Keep learning** about DevOps - http://aka.ms/DevOps

- **Keep learning** about GitHub - https://lab.github.com/