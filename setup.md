---
layout: page
title: Setup
root: .
---

## Lets get started!
You should have the following...
* Have an account on Mana
* Have UH Duo/MFA enabled
* Be able to connect to the workshop in Zoom and Mana Open OnDemand via a web browser
* Have a GitHub account


## Connect to Mana through Open OnDemand
Connect to Mana by pointing your browser (ChromeOS, Firefox or Safari) at 

[mana.its.hawaii.edu][mana-ood]

You should get the UH gold screen and then login with your user name and password. 
 
![su_fig1](fig/gold_screen_crop.png)

Authenticate with MFA/DUO via your preferred method.

You should see the Mana Open OnDemand start page

![su_fig2](fig/mana_ood.png)

## Launch an interactive session on a compute node
Start an interactive session

![su_fig3](fig/select_desktop.png)
![su_fig4](fig/check_ignition.png)
![su_fig5](fig/waiting_for_a_session.png)
![su_fig6](fig/my_interactive_session.png)

## Your compute node is assigned.
Start a shell...

![su_fig7](fig/are_you_sure.png)

Answer
	yes

Warning: Permanently added 'gpu-0016.hpc.ci.its.hawaii.edu,10.100.11.214' (ECDSA) to the list of known hosts.
Authentication failed.
Your connection to the remote server has been terminated.

Go back to my interactive sessions in the browser and start another shell..

![su_fig8](fig/compute_node_login_prompt.png)

Change the terminal theme if you like.  You can do that anytime.


![su_fig9](fig/terminal_themes_dropdown.png)



![su_fig10](fig/light_compute_node_login_prompt.png)

Download [data-shell.zip] to your home directory.

wget https://ci-tracs.github.io/Scientific_Software_Basics/data/data-shell.zip

unzip data-shell.zip

[mana-ood]: https://mana.its.hawaii.edu
[zip-file]: {{ page.root }}/data/data-shell.zip

