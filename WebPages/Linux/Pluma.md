

# Pluma Trics

----

## 1. Snippets

Allows you to quickly and conveniently insert frequently used text fragments

----

### 1.1 How to comment-out multiple lines in Pluma?

**- How to Add?**



Pluma --> Tools --> " Manage Snippets... " --> Global



**- If you don't see Manage Snippets** 

You may need to enable a plugin snippets.

Pluma --> Edit --> Preferences --> Plugins



**- Create a new insert inside Manage Snippets**

Copy and paste this code (written in Python 2.x)


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


**- How it works?**

Just try. Select several lines in the file.

Press two keys **Ctrl+3**

Your lines should already be commented out with **#**

----

### 1.2 How to remove comments from multiple lines in Pluma?

I build script which will remove first character from selectect lines.

Add to " Manage Snippets " like above in 1.1

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


### 1.3 How to add a tab to each selected line?

Mark lines of code. Then click **Tab** key.

Your lines should be shifted to the right.

The distance can be changed, however 4 spaces = 1 tab is standard.

Pluma --> Edit --> Preferences --> Editor --> Tab with


----

## 2. Side Pane


The side panel with files allows you to quickly create and open new files.

**- How to Add**

Pluma --> View --> Side Pane

Turn on the plug:

Pluma --> Edit --> Preferences --> (Something like) File browser panel

In the side panel at the bottom, click the folder icon.
This will allow you to see all the files in your project folder.

----


## 3. Color Scheme


Pluma --> Edit --> Preferences --> Font & Colors

I've read that a darker background is better for working at night.

Everyone has their own taste. 

I usually liked the white background but **Cobalt** color scheme looks great.

----



## 4 Line numbering

Having it is important.

Error messages usually include the line number where the error is found in the file.

If you don't have it enabled:

Pluma --> Edit --> Preferences --> View --> Display line numbers

----



## 5. Automatic indentations

Makes it easy faster code formatting.

At least in theory. It irritates me sometimes.

Pluma --> Edit --> Preferences --> Enable automatic indentation

----

This trics working with Pluma 1.26.0