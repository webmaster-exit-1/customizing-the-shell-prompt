<!-- Markdownlint-disable -->
    
<h1>Shell Prompt Flair</h1>

-----------------------------------------------------------------------------------------------------

Author: Mr.GFY <br>
Description: A simple script to add flair to your shell prompt. <br>
It's really more of an exercise in adding color to text output, And should be viewed as such. <br> 
Use what is done here to create your own unique terminal prompt styles and themes.

## Getting started

First we need to install `myip` from either the AUR or the clone the repository from Github [MyIP](https://github.com/make-github-pseudonymous-again/myip).

<h4><u>AUR</u></h4>

```bash
yay -S myip
```

<h4><u>Github</u></h4>

```bash
git clone https://github.com/make-github-pseudonymous-again/myip
cd myip
sudo make DESTDIR=/ PREFIX=/usr install
```
    
Now we make our personal bin direcotry and add it to our path. <br>
This is where we will keep our custom scripts.
    
```bash
mkdir -p ~/.bin
cp /usr/bin/myip ~/.bin/myip
sudo chown $USER:$USER --reducersive ~/.bin
echo 'export PATH="$HOME/.bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```
    
Now we need to make the script `myweather` for our shell prompt. <br>
Edit **"YOUR_CITY_HERE"** to your city.
    
```bash
#!/usr/bin/env bash

echo -e "$(clear)\n"
curl -w -s 'v2.wttr.in/%20%20%20%20%20%20%20%20YOUR_CITY_HERE?u&format=%l\n%20%20%20%20Current%20Weather%20Forecast\n*%20Currently%20the%20temp. %20is:%20%c%t\n*%20But%20feels%20like:%20%f\n*%20With%20a%20U.V.%20index%20of:%20%u\n*%20Todays%20Sunrise%20is%20at:%20%S\n*%20Tonights%20Sunset%20is%20at:%20%s' 2>/dev/null
echo -e "\n"
```
    
Add it to the `~/.bin` directory and make it executable.
    
```bash
mv myweather ~/.bin
chmod +x ~/.bin/myweather
```

Add these color environment variables to your `.bashrc`

```bash
##----------------------------------------------------------
## Color definitions (taken from Color Bash Prompt HowTo)
##----------------------------------------------------------

## Normal Colors
export Black='\e[0;30m'   # Black
export Red='\e[0;31m'     # Red
export Green='\e[0;32m'   # Green
export Yellow='\e[0;33m'  # Yellow
export Blue='\e[0;34m'    # Blue
export Purple='\e[0;35m'  # Purple
export Cyan='\e[0;36m'    # Cyan
export White='\e[0;37m'   # White

## Bold Colors
export BBlack='\e[1;30m'  # Bold Black
export BRed='\e[1;31m'    # Bold Red
export BGreen='\e[1;32m'  # Bold Green
export BYellow='\e[1;33m' # Bold Yellow
export BBlue='\e[1;34m'   # Bold Blue
export BPurple='\e[1;35m' # Bold Purple
export BCyan='\e[1;36m'   # Bold Cyan
export BWhite='\e[1;37m'  # Bold White

## Background Colors
export On_Black='\e[40m'  # On Black
export On_Red='\e[41m'    # On Red
export On_Green='\e[42m'  # On Green
export On_Yellow='\e[43m' # On Yellow
export On_Blue='\e[44m'   # On Blue
export On_Purple='\e[45m' # On Purple
export On_Cyan='\e[46m'   # On Cyan
export On_White='\e[47m'  # On White

## Reset Color Pallet
export NC='\e[m'          # Color Reset

## Blinking Text On/Off
export BLINK='\e[5m'      # Blinking Text

## Alarming Text Effects
export ALERT="${BRed}${BLINK}"             # Bold Red On Black Background
export DANGER="${BRed}${On_White}${BLINK}" # Blinking Bold Red On White Background
```

Now add this function to your `.bashrc`

```bash
[ "$TERM" = "xterm-256color" ] &&
    function myweather() {
      ~/.bin/myweather
    }
    if [ -x ~/.bin/myweather ]; then
    echo -e "${Blue}$(~/.bin/myweather)${NC}" | pv -qL $((18+(-3 + RANDOM%5))) && sleep 1 &&
    echo -e "${Green}.................${NC}${BRed}${BLINK}WARNING${NC}${Green}.................${NC}\n${BPurple} --- ${NC}${BBlue}力${NC}${BPurple}--- ${NC}${BRed}Anonymize your network${BPurple} ---${NC}${BBlue} 撚${NC}${BPurple}-- ${NC}\n${Green}.........................................${NC}\n${White} 數${NC}${BRed}Public IP Address: ${NC}${Black}${On_White}$(myip public)${NC}\n${White} ﲬ${NC}${BRed} Private IP Address: ${NC}${Black}${On_White}$(myip private)${NC}\n${Green}.........................................${NC}\n${BPurple} --- ${NC}${BGreen}${NC}${BPurple} --- ${NC}${BGreen}Use a${NC}${BRed} VPN${NC}${BPurple} --- ${NC}${BGreen}or a${NC}${BPurple} --- ${NC}${BRed}Socks5 PROXY${NC}${BPurple} --- ${NC}${BYellow}${NC}${BPurple} --- ${NC}" | pv -qL $((28+(-3 + RANDOM%5)))

fi
```

This function is going to display the **weather** for your **city** and your ***public*** and ***private*** **IP** addresses as a **warning**. <br>
So you know to change it if need be. <br>

And this is what it should look like when all is said and done. <br>
One clip with the script running as is and the other split up with `clear &&` added after `sleep 1` in the function.<br>


https://user-images.githubusercontent.com/98633966/195940771-111df364-9c2b-4975-8c6e-ebcfe5bfd559.mp4


https://user-images.githubusercontent.com/98633966/195940811-bba59d32-4db6-4bd9-8723-1b35909f36b8.mp4
