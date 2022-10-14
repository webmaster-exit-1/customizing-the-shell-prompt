# Shell Prompt Flair

Author: [Mrgofuckyourself]

## Getting started

First we need to install `myip` from github or the AUR.

```bash
yay -S myip
```

Make a personal hidden bin directory in your home directory.
This is where we will keep our personal executable files/scripts.

```bash
mkdir -p ~/.bin
```

Then add it to your path in your `.bashrc` or `.zshrc` file.

```bash
echo 'export PATH="$HOME/.bin:$PATH"' >> ~/.bashrc
```

```bash
git clone https://github.com/make-github-pseudonymous-again/myip
cd myip
sudo make DESTDIR=/home/"$USER" PREFIX=.bin install
sudo chown $USER:$USER --reducersive ~/.bin
chmod +x ~/.bin/myip
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
    echo -e "${Green}.................${NC}${BRed}${BLINK}WARNING${NC}${Green}.................${NC}\n${BPurple
} --- ${NC}${BBlue}力${NC}${BPurple}--- ${NC}${BRed}You may want to use a${BPurple} ---${NC}${BBlue} 撚${NC}${B
Purple}-- ${NC}\n${Green}.........................................${NC}\n${White} 數${NC}${BRed}Public IP Addre
ss: ${NC}${Black}${On_White}$(myip public)${NC}\n${White} ﲬ${NC}${BRed} Private IP Address: ${NC}${Black}${On_W
hite}$(myip private)${NC}\n${Green}.........................................${NC}\n${BPurple} --- ${NC}${BGreen
}${NC}${BPurple} --- ${NC}${BRed}VPN${NC}${BPurple} --- ${NC}${BGreen}or${NC}${BPurple} --- ${NC}${BRed}PROXY$
{NC}${BPurple} --- ${NC}${BYellow}${NC}${BPurple} --- ${NC}" | pv -qL $((28+(-3 + RANDOM%5)))

fi
```

This fuction is going to display the weather for your city and your public and private IP addresses.



```bash
cd existing_repo
git remote add origin https://gitlab.com/mrgofuckyourself/shell-prompt-flair.git
git branch -M main
git push -uf origin main
```

## Integrate with your tools

- [ ] [Set up project integrations](https://gitlab.com/mrgofuckyourself/shell-prompt-flair/-/settings/integrations)

## Collaborate with your team

- [ ] [Invite team members and collaborators](https://docs.gitlab.com/ee/user/project/members/)
- [ ] [Create a new merge request](https://docs.gitlab.com/ee/user/project/merge_requests/creating_merge_requests.html)
- [ ] [Automatically close issues from merge requests](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#closing-issues-automatically)
- [ ] [Enable merge request approvals](https://docs.gitlab.com/ee/user/project/merge_requests/approvals/)
- [ ] [Automatically merge when pipeline succeeds](https://docs.gitlab.com/ee/user/project/merge_requests/merge_when_pipeline_succeeds.html)

## Test and Deploy

Use the built-in continuous integration in GitLab.

- [ ] [Get started with GitLab CI/CD](https://docs.gitlab.com/ee/ci/quick_start/index.html)
- [ ] [Analyze your code for known vulnerabilities with Static Application Security Testing(SAST)](https://docs.gitlab.com/ee/user/application_security/sast/)
- [ ] [Deploy to Kubernetes, Amazon EC2, or Amazon ECS using Auto Deploy](https://docs.gitlab.com/ee/topics/autodevops/requirements.html)
- [ ] [Use pull-based deployments for improved Kubernetes management](https://docs.gitlab.com/ee/user/clusters/agent/)
- [ ] [Set up protected environments](https://docs.gitlab.com/ee/ci/environments/protected_environments.html)

***

### Editing this README

When you're ready to make this README your own, just edit this file and use the handy template below (or feel free to structure it however you want - this is just a starting point!). Thank you to [makeareadme.com](https://www.makeareadme.com/) for this template.

## Suggestions for a good README

Every project is different, so consider which of these sections apply to yours. The sections used in the template are suggestions for most open source projects. Also keep in mind that while a README can be too long and detailed, too long is better than too short. If you think your README is too long, consider utilizing another form of documentation rather than cutting out information.

## Name

Choose a self-explaining name for your project.

## Description

Let people know what your project can do specifically. Provide context and add a link to any reference visitors might be unfamiliar with. A list of Features or a Background subsection can also be added here. If there are alternatives to your project, this is a good place to list differentiating factors.

## Badges

On some READMEs, you may see small images that convey metadata, such as whether or not all the tests are passing for the project. You can use Shields to add some to your README. Many services also have instructions for adding a badge.

## Visuals

Depending on what you are making, it can be a good idea to include screenshots or even a video (you'll frequently see GIFs rather than actual videos). Tools like ttygif can help, but check out Asciinema for a more sophisticated method.

## Installation

Within a particular ecosystem, there may be a common way of installing things, such as using Yarn, NuGet, or Homebrew. However, consider the possibility that whoever is reading your README is a novice and would like more guidance. Listing specific steps helps remove ambiguity and gets people to using your project as quickly as possible. If it only runs in a specific context like a particular programming language version or operating system or has dependencies that have to be installed manually, also add a Requirements subsection.

## Usage

Use examples liberally, and show the expected output if you can. It's helpful to have inline the smallest example of usage that you can demonstrate, while providing links to more sophisticated examples if they are too long to reasonably include in the README.

## Support

Tell people where they can go to for help. It can be any combination of an issue tracker, a chat room, an email address, etc.

## Roadmap

If you have ideas for releases in the future, it is a good idea to list them in the README.

## Contributing

State if you are open to contributions and what your requirements are for accepting them.

For people who want to make changes to your project, it's helpful to have some documentation on how to get started. Perhaps there is a script that they should run or some environment variables that they need to set. Make these steps explicit. These instructions could also be useful to your future self.

You can also document commands to lint the code or run tests. These steps help to ensure high code quality and reduce the likelihood that the changes inadvertently break something. Having instructions for running tests is especially helpful if it requires external setup, such as starting a Selenium server for testing in a browser.

## Authors and acknowledgment

Show your appreciation to those who have contributed to the project.

## License

For open source projects, say how it is licensed.

## Project status

If you have run out of energy or time for your project, put a note at the top of the README saying that development has slowed down or stopped completely. Someone may choose to fork your project or volunteer to step in as a maintainer or owner, allowing your project to keep going. You can also make an explicit request for maintainers.
