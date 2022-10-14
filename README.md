<!-- Markdownlint-disable -->
# Shell Prompt Flair

Author: Mr.GFY
Description: A simple script to add flair to your shell prompt.

## Getting started

First we need to install `myip` from either the AUR or the clone the repository from Github [MyIP](https://github.com/make-github-pseudonymous-again/myip).

<u>AUR</u>

```bash
yay -S myip
```
<u>Github</u>

```bash
git clone https://github.com/make-github-pseudonymous-again/myip
cd myip
sudo make DESTDIR=/ PREFIX=/usr install
```

Now we make our personal bin direcotry and add it to our path.
this is where we will keep our custom scripts.

```bash
mkdir -p ~/.bin
cp /usr/bin/myip ~/.bin/myip
sudo chown $USER:$USER --reducersive ~/.bin
echo 'export PATH="$HOME/.bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Now we need to make the script myweather for our shell prompt.
Edit the "YOUR_CITY_HERE" to your city.

```bash
#!/usr/bin/env bash

echo -e "\n"
curl -w -s 'v2.wttr.in/%20%20%20%20%20%20%20%20YOUR_CITY_HERE?u&format=%l\n%20%20%20%20Current%20Weather%20Forecast\n*%20Currently%20the%20temp.%20is:%20%c%t\n*%20But%20feels%20like:%20%f\n*%20With%20a%20U.V.%20index%20of:%20%u\n*%20Todays%20Sunrise%20is%20at:%20%S\n*%20Tonights%20Sunset%20is%20at:%20%s' 2>/dev/null
echo -e "\n"
```

Name this file `myweather` and put it in your ~/.bin directory.

```bash
mv myweather ~/.bin
chmod +x ~/.bin/myweather
```

Now edit your .bashrc file and add this funtion to it.

```bash
[ "$TERM" = "xterm-256color" ] &&
    function myweather() {
      ~/.bin/myweather
    }
    if [ -x ~/.bin/myweather ]; then
    echo -e "${BWhite}$(~/.bin/myweather)${NC}" | pv -qL $((18+(-3 + RANDOM%5))) && sleep 2 && clear &&
    echo -e "${Green}.................${NC}${BRed}${BLINK}WARNING${NC}${Green}.................${NC}\n${BPurple} --- ${NC}${BBlue}力${NC}${BPurple}--- ${NC}${BRed}Anonymize your network${BPurple} ---${NC}${BBlue} 撚${NC}${BPurple}-- ${NC}\n${Green}.........................................${NC}\n${White} 數${NC}${BRed}Public IP Address: ${NC}${Black}${On_White}$(myip public)${NC}\n${White} ﲬ${NC}${BRed} Private IP Address: ${NC}${Black}${On_White}$(myip private)${NC}\n${Green}.........................................${NC}\n${BPurple} --- ${NC}${BGreen}${NC}${BPurple} --- ${NC}${BGreen}Use a${NC}${BRed} VPN${NC}${BPurple} --- ${NC}${BGreen}or a${NC}${BPurple} --- ${NC}${BRed}Socks5 PROXY${NC}${BPurple} --- ${NC}${BYellow}${NC}${BPurple} --- ${NC}" | pv -qL $((28+(-3 + RANDOM%5)))

fi
```

This fuction is going to display the **weather** for your **city** and your ***public*** and ***private*** **IP** addresses as a **warning**, so you know to change it if need be. A vpn or a proxy will work just fine.

And this is what it should look like when all is said and done.

[!prompt-flair](https://gitlab.com/mrgofuckyourself/shell-prompt-flair/-/blob/main/prompt-flair.mp4)
