# Obsidian New Session Button

## Summary

Create a button in an Obsidian note that creates a new note from a template and autolinks to it from a "table-of-contents" (MOC) note.

## Requirements

* Obsidian note-taking software
* The Meta-bind Community Plugin
* The Templater Community Plugin

## About The New Session Button

I am a *referee* (Game Master) for a bi-weekly Traveller TTRPG campaign.  In my Traveller Obsidian vault, I have a **Sessions** note that contains various
links to other notes that I reference during game sessions. At the bottom of this note is a section called Sesssions which is a simple list of links to each game
session's note. At the top of my Sessions note, I have a button called "New Session Note".

### Button Actions

When the New Session Note button is clicked, the following occurs:

* Obsidian prompts for the name of the new note.
* Obsidian creates a new note in my Sessions folder using my Sessions Template, and renames it to the name entered.
* Obsidian creates a link to the new note at the bottom of my main Sessions note, which is also the same note that the button is on.

The code below can be copy-pasted into the main body of a note to create the button. Be sure to configure the label, templateFile, and folderPath.

````
```meta-bind-button
label: New Session Note
icon: ""
style: default
class: ""
cssStyle: ""
backgroundImage: ""
tooltip: ""
id: ""
hidden: false
actions:
  - type: templaterCreateNote
    templateFile: Templates/Session Template.md
    folderPath: Traveller/Sessions
    fileName: ""
    openNote: true
    openIfAlreadyExists: false
```
````

### Sessions Template

Upon clicking the button and entering a name for the new note, Obsidian opens the **templateFile** and executes it. At the top of the template, above the *front matter*,
there is Javascript code which is executed.  This is the code that tells Obsidian to rename the new note and creates a link to the new note on my Sessions page. This code
also defines some variables that are automatically added to the front matter of the new note.

The code below is a complete Obsidian template which can be copy-pasted into a new template note.  Be sure that the template note is the same name and file path that you
defined as the *templateFile* within your button code.  Also, in the code below, be sure to set the name of the note where you want a link to the new note to be created
(for example, *Sessions.md*).

````
<%_* let title = await tp.system.prompt('Enter session name');_%>
<%_* let date = await tp.date.now("YYYY-MM-DD");_%>
<%_* let file = date + " - " + title;_%>
<%_* await tp.file.rename(date + " - " + title)_%>
<%_* let moc = tp.file.find_tfile("Sessions.md"); _%>
<%_* let newlink = "[[" + file + "]]"; _%>
<%_* await app.vault.adapter.append(moc.path, newlink); _%>
<%_* await new Promise(resolve => setTimeout(resolve, 250)); _%>
<%_* app.workspace.getLeaf(true).openFile(moc); _%>
---
type: note
description: Traveller Campaign - <% title %>
subject: Traveller - <% title %>
created: <% date %>
revised: <% date %>
revision: 1
author: kspen
tags:
  - traveller
  - game-campaign
  - game-session
---
# <% title %>

## Session Begins

session notes go here
````
