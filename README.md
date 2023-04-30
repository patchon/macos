### Introduction
This repository contains the steps needed to get my macbook up to a working state
according to my needs.

### Applications
* [AltTab](https://github.com/lwouis/alt-tab-macos), simply to use alt+tab instead of cmd+tab
* [Easy Move+Resize](https://github.com/dmarcotte/easy-move-resize), mimic move/resize behaviour as in X11
* [iTerm2](https://www.iterm2.com/downloads.html), really neat terminal

### Configuration 
* To get **CTRL**+c / **CTRL**+v behaviour, 
  * **System preferences** -> **Keyboard** -> **Modifier Keys**
    * Set **^Control** key to **⌘Command**
    * Set **⌘Command** key to **^Control**

* To get **CTRL**+->, **CTRL**+<-, **CTRL**+Backspace, (jump word / delete word)
  * **System preferences** -> **Keyboard** -> **Shortcuts** -> **Mission Control** 
    * Change the default keybindings for **Move left/right a space** as they are binded to **CTRL**+left/right.

  * Configure iTerm2, 
    * **Preferences** -> **Keys** -> **Remap Modifiers**
      * Set **Left ⌘Command** key to **^Control**
  
  * Remap the default macOS keybindings,  
  ```bash
  $ > mkdir ${HOME}/Library/KeyBindings/
  cat <<EOF > ${HOME}/Library/KeyBindings/DefaultKeyBinding.dict
  {
    "@\UF703"  = "moveWordBackward:";        /* Cmd  + LeftArrow  */
    "@\UF703"  = "moveWordForward:";         /* Cmd  + RightArrow */
    "@\U007F"  = "deleteWordBackward:";      /* Cmd  + Backspace  */
    "~ " = ("insertText:", " ");             /* Stop invisible &nbsp characters when pressing pipe */
  } 
  EOF
  ```  
  
**Note**<br><br>
Still got an issue with this in this, does not work perfect. Jumps a
whole line in input boxes, for example when editing this gist, pressing
ctrl+->, jumps to the end of the line instead of next word. Use the *ALT*
key instead as an acceptable workaround.

Specific settings in iTerm2

- Preferences -> Keys -> Keybindings -> Import the following data, 

To get ctrl+shift+c/v, and split pane ctrl+shift+e/o
- Preferences -> Keys -> Keybindings -> Import the following data, 
{
  "Touch Bar Items": {},
  "Key Mappings": {
    "0x56-0x60000-0x9": {
      "Label": "",
      "Text": "Paste\nPaste",
      "Action": 25
    },
    "0x4f-0x60000-0x1f": {
      "Label": "",
      "Text": "575108F1-E84F-4A86-BAB5-5B2114BAA6A0",
      "Action": 29
    },
    "0x45-0x60000-0xe": {
      "Label": "",
      "Text": "575108F1-E84F-4A86-BAB5-5B2114BAA6A0",
      "Action": 28
    },
    "0x43-0x60000-0x8": {
      "Label": "",
      "Text": "Copy\nCopy",
      "Action": 25
    }
  }
}



Add "typical Swedish" keyboard layout, 
- https://github.com/patchon/MacOSX-Improved-Swedish-Keyboard-Layout

Download the two files and put into ~/Library/Keyboard Layouts, reboot
and select keyboard layout from System Preferences -> Keyboard -> Input Sources (under Others).
Also, disable the default "Shortcut 2" from the AltTab application, since
it is binded on the "pipe" (<) button.

Profit.

¯\_(ツ)_/¯
