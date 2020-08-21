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

1. open new browser - type repo.new
1. create a new repo
1. come back to cloud shell
1. git push mirror to new repo

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

