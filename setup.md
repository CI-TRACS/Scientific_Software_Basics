---
layout: page
title: Setup
root: .
---

## Lets get start!
You should have the following...
* Have an account on Mana
* Have UH Duo/MFA enabled
* Be able to connect to the workshop in Zoom and Mana Open OnDemand via a web browser
* Have a GitHub account

1. Connect to Mana by pointing your browser (ChromeOS, Firefox or Safari) at [mana.its.hawaii.edu][mana-ood]
2. You should get the UH gold screen and then login with your user name and password. 
 
![su_fig1](fig/gold_screen_crop.png)

3. Authenticate with MFA/DUO via your preferred method.

4. You should see the Mana Open OnDemand start page

![su_fig2](fig/mana_ood.png)

5. Start an interactive session

![su_fig3](fig/select_desktop.png)
![su_fig4](fig/check_ignition.png)
![su_fig5](fig/waiting_for_a_session.png)
![su_fig6](fig/my_interactive_session.png)

6. Start a shell...
![su_fig7](fig/are_you_sure.png)

The authenticity of host 'gpu-0016.hpc.ci.its.hawaii.edu (10.100.11.214)' can't be established.
ECDSA key fingerprint is SHA256:YKU34+3iBdCzB/tzvkzAnlF+X0da4fVJqWgGG8CVT8M.
ECDSA key fingerprint is MD5:6a:2b:b3:ab:12:8f:c0:5e:36:10:2c:25:5d:16:37:7a.
Are you sure you want to continue connecting (yes/no)?                                           

Answer
	yes

Warning: Permanently added 'gpu-0016.hpc.ci.its.hawaii.edu,10.100.11.214' (ECDSA) to the list of known hosts.
Authentication failed.
Your connection to the remote server has been terminated.

Go back to my interactive sessions in the browser and start another shell..
![su_fig8](fig/compute_node_login_prompt.png)
![su_fig9](fig/terminal_themes_dropdown.png)

Change the terminal theme if you like.  You can do that anytime.

![su_fig10](fig/light_compute_node_login_prompt.png)

1. Download [data-shell.zip] to your home directory.

wget https://ci-tracs.github.io/Scientific_Software_Basics/data/shell-lesson-data.zip

unzip shell-lesson-data.zip



[zip-file]: {{ page.root }}/data/shell-lesson-data.zip
[mana-ood]: https://mana.its.hawaii.edu
[wsl]: https://docs.microsoft.com/en-us/windows/wsl/install-win10
[mac-terminal]: http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/
[gnome-terminal]: https://help.gnome.org/users/gnome-terminal/stable/
[kde-konsole]: https://konsole.kde.org/
[xterm]: https://en.wikipedia.org/wiki/Xterm
[install_shell]: https://carpentries.github.io/workshop-template/#shell
