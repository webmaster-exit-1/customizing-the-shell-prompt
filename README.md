<!-- Markdownlint-disable -->
    
<h1>Examples for Customizing the Shell Prompt</h1>

-----------------------------------------------------------------------------------------------------

  Description: Just some examples of what you can add to your shell prompt to make it your own. <br>
  I hope this helps anyone to create your own unique terminal prompt styles and themes.

## Getting started

  First we need to install `myip` from either the AUR or the clone the repository from Github [MyIP](https://github.com/make-github-pseudonymous-again/myip).

Install from the AUR

```bash
yay -S myip
```

Or clone from Github

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
    
  Next we need to make the script `myweather` for our shell prompt. <br>
Edit **"YOUR_CITY_HERE"** to your city.
    
```bash
echo -e "$(clear)\n"
curl -w -s 'v2.wttr.in/%20%20%20%20%20%20%20%20YOUR_CITY_HERE?u&format=%l\n%20%20%20%20Current%20Weather%20Forecast\n*%20Currently%20the%20temp. %20is:%20%c%t\n*%20But%20feels%20like:%20%f\n*%20With%20a%20U.V.%20index%20of:%20%u\n*%20Todays%20Sunrise%20is%20at:%20%S\n*%20Tonights%20Sunset%20is%20at:%20%s' 2>/dev/null
echo -e "\n"
```
    
  Add it to the `~/.bin` directory and make it executable.
    
```bash
mv myweather ~/.bin
chmod +x ~/.bin/myweather
```

  Put these color environment variables to your `.bashrc`

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
### Advanced Colorization and Animated Text

  Let's put all of that together into a function for your `.bashrc` file.

```bash
if [ "$TERM" = "xterm-256color" ]; then
  function myweather() {
    ~/.bin/myweather
  }

  if [ -x ~/.bin/myweather ]; then
    {
      echo -e "${Blue}$(~/.bin/myweather)${NC}"
      sleep 1
      echo -e "${Green}.................${NC}${BRed}${BLINK}WARNING${NC}${Green}.................${NC}
${BPurple} --- ${NC}${BBlue}力${NC}${BPurple}--- ${NC}${BRed}Anonymize your network${BPurple} ---${NC}${BBlue} 撚${NC}${BPurple}-- ${NC}
${Green}.........................................${NC}
${White} 數${NC}${BRed}Public IP Address: ${NC}${Black}${On_White}$(myip public)${NC}
${White} ﲬ${NC}${BRed} Private IP Address: ${NC}${Black}${On_White}$(myip private)${NC}
${Green}.........................................${NC}
${BPurple} --- ${NC}${BGreen}${NC}${BPurple} --- ${NC}${BGreen}Use a${NC}${BRed} VPN${NC}${BPurple} --- ${NC}${BGreen}or a${NC}${BPurple} --- ${NC}${BRed}Socks5 PROXY${NC}${BPurple} --- ${NC}${BYellow}${NC}${BPurple} --- ${NC}"
    } | {
      pv -qL $((18+(-3 + RANDOM%5)))
      pv -qL $((28+(-3 + RANDOM%5)))
    }
  fi
fi
```

  This function is going to display the **weather** for your **city** and your ***public*** and ***private*** **IP** addresses as a **warning**. <br>
So you know to change it if need be. <br>

### Example for On-Screen Early Alert System

  Here's a working example to detect when fail2ban has detected a failed login attempt and then display a warning on the screen:

```bash
#!/bin/bash

# Define color codes and formatting options
BRed='\033[1;31m'
On_White='\033[47m'
BLINK='\033[5m'
END='\033[0m' # Reset color and formatting

# Define the warning message with animation
DANGER="${BRed}${On_White}${BLINK}SSH Failed Login Attempt Detected!${END}"

# Check if fail2ban has detected a failed login attempt
if grep -q "Ban " /var/log/fail2ban.log; then
    # Display the warning message on screen
    echo -e "$DANGER"
fi
```

(Though that isn't really practical, just more of a "working" exercise. Here's a more reasonable way to achieve this)

```bash
#!/bin/bash

# Check if fail2ban has detected a failed login attempt
if grep -q "Ban " /var/log/fail2ban.log; then
    # Send a desktop notification using zenity
    zenity --warning --text="A failed login attempt has been detected." --urgency=critical --timeout=3600
fi
```

  In this modified script, we use `zenity` with the `--warning` option to display a 
warning dialog with a message indicating that a failed login attempt has been detected. 

  The `--urgency=critical` option sets the urgency level to high, and the `--timeout=3600` 
option sets the timeout to 1 hour.

  To run this script, you would save it to a file, for example `ssh_warning_zenity.sh`, 
give it execute permissions using `chmod +x ssh_warning_zenity.sh`, and then execute it in a terminal.

  Please note that `zenity` is a command-line utility that is typically available on most Linux distributions. 

  If you're using a different operating system or if `zenity` is not installed, you would
need to find an equivalent command or library for sending desktop notifications on that platform.

  Using `zenity` provides a more interactive and user-friendly experience compared to a simple 
text-based warning on the screen. It allows the user to quickly acknowledge the notification 
and take appropriate action if needed.

  Remember to adjust the timing and path to the script in the `cron` job or `systemd` service configuration 
file according to your specific requirements.

  Here's an example of how you could set up a `cron` job to run the script every minute:

```bash
# Edit the crontab file
crontab -e

# Add the following line to run the script every minute
* * * * * /path/to/ssh_warning_notify_bell.sh
```

  In this example, the `ssh_warning_notify_bell.sh` script is set to run every minute. 

  You would need to replace `/path/to/` with the actual path to the script on your system.

  Alternatively, you could set up a `systemd` service to run the script on boot or at a specific interval. 

  Here's an example of a `systemd` service configuration file:

```ini
[Unit]
Description=SSH Failed Login Attempt Notification

[Service]
ExecStart=/path/to/ssh_warning_notify_bell.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

Save this file as `ssh_warning.service` in the `/etc/systemd/system/` directory and then 
run the following commands to enable and start the service:

```bash
sudo systemctl enable ssh_warning.service
sudo systemctl start ssh_warning.service
```

  By setting up a `cron` job or a `systemd` service, you ensure that the script runs automatically
in the background without any user interaction. 

  The script will check for failed login
attempts and send desktop notifications with an audible bell if necessary.

## Visual Examples :) 

  One clip with the script running as is and the other split up with `clear &&` added after `sleep 1` in the function.<br>

https://user-images.githubusercontent.com/98633966/195940771-111df364-9c2b-4975-8c6e-ebcfe5bfd559.mp4

- In this next example the function clears the screen after the weather and before the network warning.
- Notice the artistic difference from the previous video where the text ends on the same column and the centered text. Small changes, (visualy) big differences.

https://user-images.githubusercontent.com/98633966/195940811-bba59d32-4db6-4bd9-8723-1b35909f36b8.mp4

# Happy Hacking
