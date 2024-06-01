## Archived as no longer used inside installer ISO itself 

# EndeavourOS Community Editions  
Implementation for Community Edition installs with calamares packagechooser module 

**This repo only carry example files, please  Pull Request on the default EndeavourOS calamares repository here:**
* https://github.com/endeavouros-team/EndeavourOS-calamares
 
![Community Editions Banner](https://github.com/RyzenDew/Community-Edition-installer-files/blob/main/community.jpg)

## How to get my Community Edition added into EndeavourOS installer?

In the install-process you can select a single Community Edition.  
For the selection window an image and a short description of your edition is required.  
In order to install the necessary packages.  

You need a package list and ultimately the necessary configuration files (DotFiles)  
and scripts that are needed to start and set up the interface.  

This repo contains examples for the files you need to create and maintain:

1. [packagechooser_ce.conf](https://github.com/endeavouros-team/calamares/blob/calamares/data/eos/modules/packagechooser_ce.conf)
2. [screenshot](https://github.com/endeavouros-team/calamares/tree/calamares/data/eos/images-ce)
3. [setup_once.sh](https://github.com/endeavouros-team/endeavouros-xfce4-theming/blob/master/set_once.sh) or similar script implementation that needs to run on first login.
4. [skel configuration files (DotFiles)](https://github.com/EndeavourOS-Community-Editions/bspwm)
5. A [PKGBUILD](https://github.com/endeavouros-team/PKGBUILDS/blob/master/eos-skel-ce-bspwm/PKGBUILD)  for the used skel packages
!! remember to always do a version update on the PKGBUILD when changing the configs, so it triggers package rebuild for the repository !! 

For the Desktop Manager (Login Manager) you can choose between this 4:

1. Lightdm (with slick-greeter)
2. SDDM
3. LXDM
4. GDM

As these will get handled automatic inside installer.

