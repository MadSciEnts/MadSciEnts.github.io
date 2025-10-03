---
title: Maya Dockable Windows
author: <SW>
categories: [Maya]
tags: [MayaScripts]
media_subpath: /media/
---

# Dockable Windows in Maya


![Dockable Windows in Maya](Bare_Dockable.PNG)

Creating workflow tools and scripts in Maya is always a good way to meet impossible deadlines.

Using PyQT is often the preferred way of delivering useful user interfaces.

However this is often overkill when prototyping workflows and tools under a time crunch.

Python in Maya is still pointing to Mel commands, at the end of the day.  All of Maya is a collection of ui mel commands linked together or otherwise wrapped.

Fortunately Maya comes with it's own set of methods for interacting with scripts and the work scene.

These are great for rapid prototyping of basic interactions for tools of limited scope or one off dialog interaction.

Because of this their use cases are very specific.  

The simplest and most limited form of this is the Confirmation Dialog.



## Confirmation Dialog

![confirm dialog](https://help.autodesk.com/cloudhelp/ENU/MayaCRE-Tech-Docs/gfx/confirmExample.gif)


```
cmds.confirmDialog( title='Confirm',
                    message='Are you sure?',
                    button=['Yes','No'],
                    defaultButton='Yes',
                    cancelButton='No',
                    dismissString='No' )
```

There are limitations with Maya's dialog windows.  You cannot interact with the work scene while these windows wait for your input.

They are great for forcing confirmation of a next process (as their name would suggest).

For instance before launching a lengthly export process or caching event, it is good practice to confirm with the artist that the elements to be processed are correct.




## Maya Native Windows

Another way is to simply create a floating window using Maya's native commands.

This allows for more control over how the information is presented.  Text, Input fields, Drop down menus, buttons, etc.

Using the 'callback' parameter in each UI Widget, you can connect user interaction to script commands.


```
import maya.cmds as cmds

# Make a new window
#
window = cmds.window( title="Long Name", iconName='Short Name', widthHeight=(200, 55) )
cmds.columnLayout( adjustableColumn=True )
cmds.button( label='Do Nothing' )
cmds.button( label='Close', command=('cmds.deleteUI(\"' + window + '\", window=True)') )
cmds.setParent( '..' )
cmds.showWindow( window )
```

[Window command documentation](https://help.autodesk.com/cloudhelp/ENU/MayaCRE-Tech-Docs/CommandsPython/window.html)

This presents an interesting problem.  As artists launch more tools during their workflow, they must manage an increasing number of custom tool windows.

While it is good practice to ensure that workflows are contained within a limited scope of tool windows, it isn't always possible.
This is especially true during rapid prototyping of tools and emerging workflows.


## Dockable Workspaces

This is where "Dockable Workspaces" come in.

![Dockable Tool Windows](Bare_Dockable.PNG)

The basic implementation of the dockable workspaces (as shown from the Maya Documentation) gives you an idea of the general structure.
The workspace control command will point to a previously defined function of the UI to be drawn. This function will contain all of the buttons, labels, layout and ui.
The workspace control command simply gives it a space to draw these elements into.

```
import maya.cmds as cmds

def createCustomWorkspaceControlUI(*args):
  cmds.columnLayout()
  cmds.button()
  cmds.button()
  cmds.button()

cmds.workspaceControl("myCustomWorkspaceControl",
                       retain=False,
                       floating=True,
                       uiScript="createCustomWorkspaceControlUI()");
```

[Workspace Control Documentation](https://help.autodesk.com/cloudhelp/ENU/MayaCRE-Tech-Docs/CommandsPython/workspaceControl.html)


We can extend this further by utilizing some parameters to allow this dockable area to behave similar to the attribute editor tab.

Below is the general starting point I like to begin with when rapidly prototyping a toolset or workflow.


We begin by declaring a global variable for the name of the window/dockable control.

Then we define the Main UI. What buttons or controls are drawn in this space.

A RefreshWindow function is good practice. When updating fields or elements, this can be handy.

It is important to check if the dockable control already exists.

If it does, delete it and draw the new one.

And finally, there is the CreateDockWindow function that kicks off the whole process.


```
import maya.cmds as cmds

#############GLOBALS#########################
global winName

### MAIN UI ##############################
def createCustomWorkspaceControlUI():
  scrollLayout = cmds.scrollLayout(
    horizontalScrollBarThickness=16,
	  verticalScrollBarThickness=16, width=250)
	
    cmds.columnLayout(adj=True, width=350)
    cmds.text("Dockable Window")
    cmds.button("Button", width=100)
    cmds.separator( height=40, style='in' )
##########################################
    

### UI FUNCTIONS ############################
def RefreshWindow():
    global winName
    if cmds.workspaceControl(winName, exists=True):
        cmds.deleteUI(winName)
    createDockWindow()

def createDockWindow():
    global winName
    if cmds.workspaceControl(winName, exists=True):
        cmds.deleteUI(winName)
    cmds.workspaceControl(winName,
    tabToControl=["AttributeEditor", -1],
    retain=False,
    floating=True,
    uiScript='createCustomWorkspaceControlUI()',
    widthProperty="fixed",
    resizeWidth=350,
    minimumWidth=350)
#############################################

    
winName = "MyDockable"
createDockWindow()
```

I highly recommend using dockable custom tools whenever possible.
