# folders.md

## note in Ordner
# add a new note in the folder named "example"
nb add example/

# add a new note in the folder named "demo" in "example"
nb add example/demo/

----------------------------------
## Ordner
# add ordner
# create a new folder named "sample"
nb add sample --type folder

# create a folder named "example" containing a folder named "demo"
nb add example/demo --type folder

tems in folders can be idenitified with the folder's relative path using either folder ids or names, followed by the id, title, or filename of the item:

# list item 1 ("Title One", one.md) in the example/demo/ folder
nb list example/demo/1

# edit item 1 ("Title One", one.md) in the example/demo/ folder
nb edit example/2/one.md

# show item 1 ("Title One", one.md) in the example/demo/ folder
nb show 1/2/Title\ One

# delete item 1 ("Title One", one.md) in the example/demo/ folder
nb delete 1/demo/1
For folders and items in other notebooks, combine the relative path with the notebook name, separated by a colon:

# list the contents of the "sample" folder in the "example" notebook
nb example:sample/

# add an item to the "sample/demo" folder in the "example" notebook
nb add example:sample/demo/

# edit item 3 in the "sample/demo" folder in the "example" notebook
nb edit example:sample/demo/3
Browse starting at any folder with nb browse:

❯ nb browse example:sample/demo/
❯nb · example : sample / demo /

search: [                    ]

[example:sample/demo/5] Title Five
[example:sample/demo/4] Title Four
[example:sample/demo/3] Title Three
[example:sample/demo/2] Title Two
[example:sample/demo/1] Title One 


