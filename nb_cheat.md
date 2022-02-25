# NB CHEAT
# add
nb add --title "Title" ""content" --tags tag1,tag2
nb a title.md
nb notebook:a
nb notebooks add example 
# search
nb home:q "search"

# Repo
gh repo create 
nb remote set https://github.com/einfachgewaltig/cheat
nb notebook:sync
nb git fetch origin
nb notebook:git status
## initialize new "home" notebook with the branch "sample-branch" on the remote
nb init https://github.com/xwmx/example sample-branch
## initialize new "home" notebook with the branch "sample-branch" on the remote
nb init https://github.com/xwmx/example sample-branch
nb remote branches

# Import
nb import ~/Pictures/example.png
nb open example.png
## import all files and directories in the current directory
nb import ./*
## import all markdown files in the current directory
nb import ./*.md
## import example.md and sample.md in the current directory
nb import example.md sample.md

# export 
nb export pandoc 42 --from markdown_strict --to epub -o path/to/example.epub
