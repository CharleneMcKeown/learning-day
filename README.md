# Learning Day 

Work in progress.

## pre-reqs

1. Azure Visual Studio subscription enabled
1. GitHub Account

## Step 1

1. log into Azure
1. Open cloud shell
1. Setup Hugo
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
git submodule add https://github.com/your-identity/hugo-theme-dimension.git themes/dimension
```
```
echo 'theme = "dimension"' >> config.toml
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
1. we could include some tips for styling to make it more snazzy
1. git commit and push - CI in action
1. observe the workflow and deployment - CD

