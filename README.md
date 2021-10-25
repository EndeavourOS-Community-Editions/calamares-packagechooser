# calamares-packagechooser
Implementation for Community Edition installs with calamares packagechooser module

## How to get my Community Edition added into EndeavourOS installer?

1. To use the packagechooser module in calamares we need you to add your Community Edition into the needed configuration files for calamares:
* https://github.com/endeavouros-team/EndeavourOS-calamares/blob/main/calamares/modules/packagechooser.conf

2. the install command entry:
* https://github.com/endeavouros-team/EndeavourOS-calamares/blob/main/calamares/modules/contextualprocess.conf

3. add the packages list that is needed in addition to the **base system** you find in this file: 
https://raw.githubusercontent.com/endeavouros-team/EndeavourOS-calamares/main/calamares/files/netinstall-ce-base.yaml 
here:
* https://github.com/endeavouros-team/EndeavourOS-calamares/tree/main/calamares/ce
File name is your **id** used in **packagechooser.conf** that will be used to select and install the packages list inside the **contextualprocess.conf**

4. add a screenshot for your Community Edition here:
* https://github.com/endeavouros-team/EndeavourOS-calamares/tree/master/calamares/images

# packagechooser.conf

Translations are not required  but should be good to make it clear for everyone what your setup is about.

```
    - id: sway
      name: "Sway Edition"
      description: "text text text"
      screenshot: "/etc/calamares/images/sway.jpg"
 ```

This 4 ones are requiered to add your Edition. Please validate your edit with a yaml validator! The 2 calamares config files must be valid yaml to be used.

Screenshot should have 1067x800 pixels and must be .jpg
<img src="https://raw.githubusercontent.com/endeavouros-team/EndeavourOS-calamares/main/calamares/images/community.jpg" alt="example" width="1067"/>

# contextualprocess.conf:

```
dontChroot: false
timeout: 600

packagechooser_packagechooser:

    sway:   "pacman -Sy --needed --noconfirm - < /tmp/ce/sway.txt"
    
    bspwm:  "pacman -Sy --needed --noconfirm - < /tmp/ce/bspwm.txt"
```
   
 
 Where sway is the **id:** and **sway.txt** is the packages list.
 
5. create a PKGBUILD that installs your configs to /etc/skel and may runs a config script on first boot to setup user specific stuff

# PKGBUILD:
```
# Maintainer: xx>
# Contributor: xx>
# Contributor: xx>

_pkgname=sway
pkgname=eos-skel-ce-sway
pkgver=1.0
pkgrel=1
pkgdesc="pre user creation skel setup for SWAY EOS-CE"
arch=('any')
groups=('eos-ce')
url="https://github.com/EndeavourOS-Community-Editions/${pkgname}"
license=('GPL')
conflicts=('eos-ce-sway')
depends=('git')
source=("${_pkgname}::git+https://github.com/EndeavourOS-Community-Editions/${_pkgname}.git")
sha256sums=('SKIP')

package() {
    PREFIX=/etc/skel
    cd "$_pkgname"
    mkdir -p "${pkgdir}${PREFIX}/.config/"
    cp -R ".config/" "${pkgdir}${PREFIX}/"
    install -Dm644 ".gtkrc-2.0" "${pkgdir}${PREFIX}/.gtkrc-2.0"
    install -Dm644 ".profile" "${pkgdir}${PREFIX}/.profile"
    install -Dm644 ".nanorc" "${pkgdir}${PREFIX}/.nanorc"
    install -Dm755 "set_once.sh" "${pkgdir}${PREFIX}/set_once.sh"
    install -Dm644 "xed.dconf" "${pkgdir}${PREFIX}/xed.dconf"
}
```
And create a pull request to add it to the EndeavourOS Calamares repository. this package must be added to your packages list too.

https://github.com/endeavouros-team/PKGBUILDS

6. The needed Dot-Files for your setup:

The Structure of your dotfiles should be sorted like this:

* https://github.com/EndeavourOS-Community-Editions/sway

So it can be used by the PKGBUILD in the above example.

You do not need to use GitHub, any other place can be used also to develop your repo, but to be added to installer we need a copy here at this repository.
