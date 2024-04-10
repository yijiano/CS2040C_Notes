#cs2040c 
# Nice Links
[Learn C++](https://www.learncpp.com/)
[Intro to Algo Textbook](https://www.inf.ufpr.br/andre/textos-CI1165/Introduction%20to%20Algorithms%20-%203rd%20Edition.pdf)
[VISUALGO](https://visualgo.net/en)
[Competitive Programming Stuff](https://cpbooks.net)
[Steven Halim GitHub](https://github.com/stevenhalim)

# Content
[[01_intro|Introduction & OOP]]
[[02_vla_adt|Variable Length Array & Abstract Data Types]]
[[03_searching|Searching]]
[[04_sorting|Sorting]]
[[05_trees_bst_avl_augtrees|Trees (BST, AVL, Augmentation)]]
[[06_hashing|Hashing]]
[[07_heap|Heap]]
[[08_ufds|Union-Find Disjoint Sets]]
[[09_graphs_dfs_bfs_dag|Graphs (DFS, BFS, DAG)]]
[[10_sssp_bf|Single-Source Shortest Path]]
[[11_dijkstras|Dijkstra's Algorithm]]
[[12_topological_sort_connected_components|Topological Sort & Connected Components]]
[[13_graphs_drawing_mst_bsp|Graphs (Drawing, MST, BSP)]]

# Git tl;dr #git
[Source](https://rogerdudler.github.io/git-guide/)
## Create new repository 
```
git init
```
## Checkout a repository
```sh
# Create a working copy of a local repository
git clone /path/to/repository

# When using a remote server:
git clone username@host:/path/to/repository
```
## Add & Commit
```sh
# Propose changes (add it to the INDEX)
git add <filename>
git add *
git add -A

# Commit changes, commit to HEAD
git commit -a -m "Commit message"
```
## Pushing Changes
```sh
# Send changes in HEAD to your remote repository
git push origin <branch>

# If you have not cloned an existing repository and want to connect your repository to a remote server, you need to add it with

git remote add origin <server>
```
## Branching
```sh
# Create new branch named "feature_x" and switch using
git checkout -b feature_x

# Switch back to master
git checkout master

# And delete the branch again
git branch -d feature_x
```

>[!NOTE]
>A branch is *not available to others* unless you push the branch to your remote repository
## Update & Merge
```sh
# Before merging, you can preview using
git diff <source_branch> <target_branch>

# Fetch and merge remote changes
git pull

# Merge another branch into your active branch
git merge <branch>
```
## Tagging
```sh
git tag <tag_name> <first_10_characters_of_commit>
```
## Log
```sh
# Study repository history
git log

# See only commits of a certain author
git log --author=bob

# See compressed log where each commit is one line
git log --pretty=online

# ASCII art tree of all branches
git log --graph --online --decorate --all

# See only which files have changed:
git log --name-status

# Help
git log --help
```
## Replace Local Changes
```sh
# Replace local changes with HEAD
git checkout -- <filename>

# Drop all local changes and fetch latest history from server and point local master branch at it
git fetch origin
git reset --hard origin/master
```
## Useful Hints
```sh
# Built-in git GUI
gitk

# Use colourful git output
git config color.ui true

# Show log on just one line per commit
git config format.pretty online

# Use interactive adding
git add -i
```