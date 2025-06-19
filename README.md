# scrips
Convert your text selection to uppercase

This script can marche for LINUX only


#          first step           

install required packages

sudo apt install xclip xdotool xbindkeys

#          second step           

create the script file

nano ~/.scripts/uppercase.sh

If the directory .scripts does not exist, create it first:

mkdir .scripts
nano ~/.scripts/uppercase.sh

#          third step           

Paste the following content into your script file:

```
#!/bin/bash

# Copier la sélection (Ctrl+C)
xdotool key --clearmodifiers ctrl+c
sleep 0.1

# Lire le contenu du presse-papiers
TEXT=$(xclip -o -selection clipboard)

# Vérifier si tout est en majuscules
if [[ "$TEXT" =~ [A-Z] ]] && [[ ! "$TEXT" =~ [a-z] ]]; then
    # Passer en minuscules
    NEW_TEXT=$(echo "$TEXT" | tr '[:upper:]' '[:lower:]')
else
    # Passer en majuscules + remplacer les lettres accentuées
    NEW_TEXT=$(echo "$TEXT" \
        | tr '[:lower:]' '[:upper:]' \
        | sed -e 's/É/E/g' -e 's/È/E/g' -e 's/Ê/E/g' -e 's/Ë/E/g' \
              -e 's/À/A/g' -e 's/Â/A/g' -e 's/Ä/A/g' \
              -e 's/Ù/U/g' -e 's/Û/U/g' -e 's/Ü/U/g' \
              -e 's/Ô/O/g' -e 's/Ö/O/g' \
              -e 's/Î/I/g' -e 's/Ï/I/g' \
              -e 's/Ç/C/g')
fi

# Écrire dans le presse-papiers
echo -n "$NEW_TEXT" | xclip -selection clipboard

# Coller le texte transformé
xdotool key --clearmodifiers ctrl+v
sleep 0.1

```

#          fourth step           

Make the script executable
chmod +x ~/.scripts/uppercase.sh

#          fifth step           

Find your input (mouse button or key) if unknown
Run the following command to detect input events:

xev

Bind the script to your input
Edit your xbindkeys configuration file:

nano ~/.xbindkeysrc

Add this line to assign your script to mouse button 9 (for example):

"~/.scripts/uppercase.sh"
  b:9

#           final step          

Restart xbindkeys to apply changes

killall xbindkeys

xbindkeys


