<mark>Happy Path</mark>
1- git checkout main
2- git pull
3- git checkout -b feature
# work + commit many times
4- git fetch origin
5- git rebase main
6- git push origin feature
# open PR and merge feature into main

<mark>Unhappy Path</mark>
git checkout main
git pull
git checkout -b feature
# make changes and commit multiple times
git add .
git commit -m "your commit message"
# repeat add + commit as needed
git fetch origin
git rebase main//better with (git rebase i main) for interactive squash commits
# if conflicts occur, edit files to resolve
git add <resolved-files>
git rebase --continue
# repeat add + rebase --continue until done
# to cancel rebase if needed:
# git rebase --abort
git push origin feature
# open PR and merge feature into main
