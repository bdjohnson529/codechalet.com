---
title: "Windows Context Menu"
layout: blog
parent: Windows
parent_path: windows/
---
The Windows context menu is the menu which appears when you right click in the Windows file explorer. The menu can be customized to launch new applications. Adding applications to the context menu saves time!

## Registry Editor
The registry editor can be customized to add and remove programs from the context menu. Press Windows + R and enter `regedit.exe` and enter to launch the Registry Editor.

The context menu settings are saved at the following path.
```
HKEY_CLASSES_ROOT\Directory\Background\shell
```

In this folder, you will notice the programs which appear when you right click within a folder. My directory looks like this:
```
.
├── Directory
|	├── Background
|	├── shell
|		├── Launch Sublime
|			├── command
|		├── Launch Anaconda Prompt
|			├── command
```

These are the same programs which appear when I right-click in a directory. You will be able to see the options added above when you right click within a directory.

To associate the action with a command, modify the two command keys with the values

```
C:\Program Files\Sublime Text 3\sublime_text.exe "%V"
cmd.exe /K C:\ProgramData\Anaconda3\Scripts\activate.bat
```

Voila! Now you should be able to launch your program from the context menu!

# References
* [Add Anaconda to Right Click Menu](https://gist.github.com/jiewpeng/8ba446acf329b1801bf91db767d179ea)