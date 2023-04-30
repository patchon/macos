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
  $ > cat <<EOF > ${HOME}/Library/KeyBindings/DefaultKeyBinding.dict
  {
    "@\UF703"  = "moveWordBackward:";        /* Cmd  + LeftArrow  */
    "@\UF703"  = "moveWordForward:";         /* Cmd  + RightArrow */
    "@\U007F"  = "deleteWordBackward:";      /* Cmd  + Backspace  */
    "~ " = ("insertText:", " ");             /* Stop invisible &nbsp characters when pressing pipe */
  } 
  EOF
  ```  
  
  > **Note**<br>
  Still got a small issue with this, it doesn't work perfect. Jumps a
  whole line in input boxes in for example a browser. When editing this readme in gitHub, pressing
  **CTRL**+->, jumps to the end of the line instead of next word.
  Current workaround is to use the **ALT** key instead as an acceptable workaround.

* To get **CTRL+SHIFT**+c/v, and split pane **CTRL+SHIFT**+e/o
  * **Preferences** -> **Keys** -> **Keybindings** -> **Import**
  ```bash
  $ > cat <<EOF > ${HOME}/iterm-keybindings.json
  {
    "Key Mappings": {
      "0x43-0x60000-0x8": {
        "Version": 0,
        "Action": 25,
        "Text": "Copy\nCopy",
        "Label": ""
      },
      "0x56-0x60000-0x9": {
        "Version": 0,
        "Action": 25,
        "Text": "Paste\nPaste",
        "Label": ""
      },
      "0x4f-0x60000-0x1f": {
        "Version": 0,
        "Action": 29,
        "Text": "67CA84F8-F106-4FE3-8CF8-6540DFBBC878",
        "Label": ""
      },
      "0x45-0x60000-0xe": {
        "Version": 0,
        "Action": 28,
        "Text": "67CA84F8-F106-4FE3-8CF8-6540DFBBC878",
        "Label": ""
      }
    },
    "Touch Bar Items": {}
  }
  EOF
  ```

* Add "typical Swedish" keyboard layout, 
  * Download the two files and put into ~/Library/Keyboard Layouts and reboot.
  * Select keyboard layout from **System Preferences** -> **Keyboard** -> **Input Sources** (under Others).

  ```bash
  $ > curl https://raw.githubusercontent.com/patchon/macos/raw/master/Swedish-SFZ.keylayout -o ~/Library/Keyboard\ Layouts/Swedish-SFZ.keylayout
  $ > curl https://github.com/patchon/macos/raw/master/Swedish-SFZ.icns -o ~/Library/Keyboard\ Layouts/Swedish-SFZ.keylayout
  ```
  > **Note**<br>
  Also, disable the default "Shortcut 2" from the AltTab application, since it is binded on the "pipe" (<) button.

* Install Homebrew,
  ```bash
  $ > /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
  ```
  
* Install / configure random things,
  ```
  $ > brew install bash jq wget podman
  $ > echo "/opt/homebrew/bin/bash" >> /etc/shells
  $ > chsh -s /opt/homebrew/bin/bash
  $ > curl https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/stable/openshift-client-mac-arm64.tar.gz -o /tmp/oc.tar.gz
  $ > sudo mkdir /usr/local/bin && sudo chown $USER /usr/local/bin
  $ > tar zxvfp /tmp/oc.tar.gz -C /usr/local/bin/ && rm -f /usr/local/bin/README.md
  $ > 
  
  
  
Profit.

¯\_(ツ)_/¯
