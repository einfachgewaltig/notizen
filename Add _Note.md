# 

## create a new note in your text editor
 nb add

> ## create a new note with the filename "example.md"
nb add example.md

## create a new note containing "This is a note."
nb add "This is a note."

> ## create a new note with piped content
echo "Note content." | nb add

## create a new password-protected, encrypted note titled "Secret Document"
nb add --title "Secret Document" --encrypt

## create a new note in the notebook named "example"
nb example:add "This is a note."

> ## create a new note in the folder named "sample"
nb add sample/
