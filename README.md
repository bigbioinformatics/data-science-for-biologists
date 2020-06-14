# Getting started with jupyter lab

## Setting up your personal conda environment

The server you are accessing has a package management system called `conda`. Learn more about `conda` [here](https://docs.conda.io/en/latest/). Conda works by creating 'environments' which contain software that is only accessible from within that environment. This means that making a change in an environment doesn't affect the rest of the server. This is also useful because you can completely control the software within your environment -- no admin privileges are required to install new programs. In this tutorial, you will initialize conda, create a personal conda environment, install a software program into it, and set up your jupyter notebook to recognize that environment automatically. 

These steps must be completed in a 'terminal' session:
1. Initialize conda for your user account:
```
conda init
```
2. Close and reopen your terminal session. You should now see `(base)` infront of the command line.
2. Create your personal environment (replace `<username>` with your username). When prompted, select `y` and hit 'enter':
```
conda create -n <username> ipykernel
```
3. Activate your environment:
```
conda activate <username>
```
4. Install a software program:
```
conda install -c bioconda salmon
```
5. Verify that `salmon` was correctly installed (will show "Salmon" in ascii art if it worked):
```
salmon swim
```
6. Link your environment with your jupyter profile:
```
.conda/envs/<username>/bin/python -m ipykernel install --user --name '<username>' --display-name "<username>'s environment"
```
7. Return to the Launcher (`+` symbol) or press ctrl + shift + L (windows) you should see an option to launch a jupyter notebook with `<username>'s environment`


**NOTE**: Every time your open a new terminal, you will be in the `(base)` environment -- however, you do not have permissions for downloading software into the `(base)` environment (it will produce an error if you try). Before you can download a program, you will need to run `conda activate <username>`. Doing this should change the `(base)` environment to one which displays `(<username>)`. 


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
