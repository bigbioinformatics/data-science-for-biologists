# Getting started with jupyter lab

## Setting up your personal conda environment

The server you are accessing has a package management system called `conda`. Learn more about `conda` (here)[https://docs.conda.io/en/latest/]. Conda works by creating 'environments' which contain software that is only accessible from within the environment. This means that making a change in an environment doesn't affect the rest of the server. This is also useful because you can completely control the software within your environment -- no admin privileges are required to install new programs. In this tutorial, you will initialize conda, create a personal conda environment, install a software program into it, and set up your jupyter notebook to recongnize that enrivonment automatically. 

These steps must be completed in a 'terminal' session:
1. Initialize conda for your user account:
`conda init`
2 

To do this simply run the following (substituting your username for `<username>`):

```
conda init
conda create -n <username> ipykernel
```

When prompted, type `y` and hit enter.

Once the packages finish downloading run the following:

```
.conda/envs/<username>/bin/python -m ipykernel install --user --name '<username>' --display-name "<username>'s environment"
```

If you return to the Launcher (`+` symbol) or press ctrl + shift + L (windows) you should see an option to launch a jupyter notebook using `<username>'s environment`





## Setting up git

The first task is to set up a github account, create a new repository, and push your first commit

1. Visit github.com and create an account if you don't already have one
2. Go to your repositories page and create a new one
3. Open jupyter lab and create a new 'terminal' page
4. Use the terminal to create a directory for your workshop project (rename this with the actual name of your project):
`mkdir myproject`
5. Navigate to the project directory: 
`cd myproject`
6. Configure that directory as a git repository: 
`git init`
7. Add a new file:
`echo "# myproject" > README.md`
8. Add the file (and any others in this folder) to your git repository:
`git add .`
9. Configure your repository author information:
```
git config user.email "yourName@livemail.uthscsa.edu"
git config user.name "Your Name"
```
10. Add your first commit (don't forget the message `-m "my message"`):
`git commit -m "My first commit!"`
11. Link your local repository to your github.com repository:
`git remote add origin https://github.com/yourName/github_repo_name.git`
12. Push your local repository to github.com:
`git push -u origin master`
13. Check your github.com repository -- it should that you successfully added a new file "README.md" which says "myproject".
