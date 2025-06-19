# scrips
Convert your text selection to uppercase
This script can marche for LINUX only


# ------------------------          STEP FIRST          ------------------------

INSTALL REQUIRED PACKAGES
sudo apt install xclip xdotool xbindkeys

#------------------------          STEP SECOND          ------------------------

CREATE THE SCRIPT FILE
nano ~/.scripts/uppercase.sh

If the directory .scripts does not exist, create it first:
mkdir .scripts
nano ~/.scripts/uppercase.sh

#------------------------          STEP THIRD          ------------------------

Paste the following content into your script file:

```#!/bin/bash

# 1. copy your selection (Ctrl+C)
xdotool key --clearmodifiers ctrl+c
sleep 0.1  # Petit délai pour s'assurer que le texte est copié

# 2. Read on press paper
TEXT=$(xclip -o -selection clipboard)

# 3. Transform in MAJUSCULES
UPPER=$(echo "$TEXT" | tr '[:lower:]' '[:upper:]')

# 4. Write on press paper
echo -n "$UPPER" | xclip -selection clipboard

# 5. Paste texte (Ctrl+V)
xdotool key --clearmodifiers ctrl+v
```

#------------------------          STEP FOURTH          ------------------------

Make the script executable
chmod +x ~/.scripts/uppercase.sh

#------------------------          STEP FIFTH          ------------------------

Find your input (mouse button or key) if unknown
Run the following command to detect input events:

xev

Bind the script to your input
Edit your xbindkeys configuration file:

nano ~/.xbindkeysrc

Add this line to assign your script to mouse button 9 (for example):

"~/.scripts/uppercase.sh"
  b:9

#------------------------          FINAL STEP          ------------------------

Restart xbindkeys to apply changes
killall xbindkeys
xbindkeys


