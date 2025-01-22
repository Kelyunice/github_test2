git init                                               ===> To initialize a repo
git remote add " new alias of repo" "url"              ===> To link the remote repo and the locale
git pull "alias of repo" "branch name"                 ===> To fetch and merge changes from the remote repo
git remote -v                                          ===> To see the alias of the remote repo
git branch -r                                          ===> To ensure your remote branch is available on the local
git log                                                ===> To ensure both have thesame content (are at the same level)
git branch                                             ===> to see available branches
git branch "name"                                      ===> To create new branch
git branch -m "new name"                               ===> To rename a local branch to match the remote name
git switch "branch name"                               ===> To switch to a new branch
git switch -c "new branch name"                        ===> To create new branch and witch directly to it
vi "file name"                                         ===> To create a file and move to adding content
git add .                                              ===> To push changes from working area to stagging area
git commit -m "commit message"                         ===> To commit changes to local
git status                                             ===> To see status of our work
git push "alias of repo" "branch name "                ===> To push changes to remote repo
git checkout -b                                        ===> To create new branch and switch to it
git push -u "alias of repo" "branch name"              ===> To set upstream
git fetch                                              ===> To download a remote repo to our local for viewing
git diff                                               ===> To compare chnages between commits or branches
git commit --amend                                     ===> To edit a commit message
git merge                                              ===> To merge two branches
git branch -D                                          ===> to delete a branch that has not been merged
git branch -d                                          ===> To delete a branch that has already been merged.
cd "repo name", rm -rf .git                            ===> To delete the .git storage
cd out of the repo (rm -rf "repo name")                ===> To delete the repository on CLI
