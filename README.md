# commit-day.sh walkthrough

## Installation

First off, this application only works with bash or shells that can run bash script (e.g., zsh). If you're on Linux or Mac, no extra configuration should be necessary. If you are windows, you'll need to install (Windows Subsystem for Linux (WSL))[https://docs.microsoft.com/en-us/windows/wsl/install]

Clone this repo and name it according to the month for which you'd like fill in git squares. Navigate to the directory from your terminal. Then delete the git history by removing the `.git` directory:

```cli
cd <path to directory containing commit-day.sh>
rm -rf .git
```

With the repo's git history is removed, initialize another git repository. Next create a new repository on Github to store your commits, then link your local and remote repositories:

```cli
git init
git add .
git commit -m "Initial commit"
git remote add origin <github repo url>
git remote -v
```
If the console returns the correct url for your github repo, continue. If not, try again.

```cli
git push -u origin main
```

Allow `commit-day.sh` to be run in the terminal by adding permissions:

```cli
chmod +x ./commit-day.sh
```

Craft your arguments that you will enter in the command line. The command takes 4 arguments: a 4 digit year, 1 or 2 digit month, 1 or 2 digit day to start committing, 1 or 2 digit day to end committing.

For example, if I wanted to add commits from October 9th 2021 to October 17th 2021, my arguments would look like this:
```cli
commit-day.sh 2021 10 9 17
```

Go to github and double check that your squares are being displayed properly. When your commits for a month look the way you want them to, STOP committing before moving onto another month. This will make it so that if you somehow pass arguments you didn't mean to, you won't have delete the whole repository and lose the commits you were happy with. Remove the git history for your completed month:
```cli
rm -rf .git
```

Now you can start the process all over again with `git init` starting with a different month.

## Variables inside the script

You can change the number of commits in each day. On line 11 of `commit-day.sh`, the variable `n` exists. This will randomly generate a number between 0-6 (i.e., `RANDOM%7`) and then add 10 to it by default. You can change this to numbers to suit your preferred commit range:

between 5 and 10 commits a day:
```bash
n=$((RANDOM%6+5))
```

flat 7 commits a day:
```bash
n=7
```

## Possible Errors
Line 25 and 28 reference `main` as your main branch. If you get an error that says `main branch does not exist`, your main branch is liely set to `master`. Just change `main` to `master` inside commit-day.sh
