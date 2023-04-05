

# Pluma Trics

----

## How to comment-out multiple lines in Pluma


Pluma --> Tools --> " Manage Snippets... " --> Global

Create a new insert, copy and paste this code (written in Python 2.x)


```
$<
selected_txt = $PLUMA_SELECTED_TEXT
output = "" 
for line in selected_txt.split("\n"):
    line = "#" + line
    output = output + line + "\n"
    
# remove last /n character
output = output[:-1]

return output
>

```

Set shortcut key:    Ctrl+3


----

## How to remove comments multiple lines in Pluma

I build script which will remove first character from selectect lines.

```
$<
selected_txt = $PLUMA_SELECTED_TEXT
output = "" 
for line in selected_txt.split("\n"):
		# remove first character
    line = line[1:]
    output = output + line + "\n" 
    
# remove last /n character
output = output[:-1]

return output
>
```

Set shortcut key:    Ctrl+R

----

This trics working with Pluma 1.26.0