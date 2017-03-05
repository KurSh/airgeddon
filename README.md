<!-- Change version for shield on each commit -->
<!-- Visit https://shields.io/ for more info -->
<!-- Shields' color scheme based on banner: colorA=273133 colorB=0093ee -->

# :satellite: airgeddon [![Version-shield]](CHANGELOG.md) [![Bash4.2-shield]](http://tldp.org/LDP/abs/html/bashver4.html#AEN21220) [![License-shield]](LICENSE.md) [![Paypal-shield]](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=7ELM486P7XKKG) [![Bitcoin-shield]](https://blockchain.info/address/1AKnTXbomtwUzrm81FRzi5acSSXxGteGTH)

> This is a multi-use bash script for Linux systems to audit wireless networks.

![Banner]

<details>
	<summary id="TOC"><strong>Table Of Contents</strong></summary>
- [Features]
- [Requirements]
 - [Essential Tools]
 - [Optional Tools]
 - [Update Tools]
 - [Internal Tools]
 - [BeEF Tips]
- [Usage]
- [Supported Languages]
- [Known Incompatibilities]
- [Contributing]
- [Changelog]
- [Disclaimer & License]
- [Acknowledgments]
 - [Hat Tip To]
 - [Inspiration]
</details>

---

### Features

- Interface mode switcher (Monitor-Managed) keeping selection even on interface name changing
- DoS over wireless networks using different methods
- Assisted Handshake file capturing
- Cleaning and optimizing Handshake captured files
- Offline password decrypting on WPA/WPA2 captured files (dictionary, bruteforce and rule based)
- Evil Twin attacks (Rogue AP)
 - Only Rogue/Fake AP version to sniff using external sniffer (Hostapd + DHCP + DoS)
 - Simple integrated sniffing (Hostapd + DHCP + DoS + Ettercap)
 - Integrated sniffing, sslstrip (Hostapd + DHCP + DoS + Ettercap + Sslstrip)
 - Integrated sniffing, sslstrip2 and BeEF browser exploitation framework (Hostapd + DHCP + DoS + Bettercap + BeEF)
 - Captive portal with "DNS blackhole" to capture wifi passwords (Hostapd + DHCP + DoS + Dnsspoff + Lighttpd)
- WPS features
 - WPS scanning (wash). Self parameterization to avoid *"bad fcs"* problem
 - Custom PIN association (bully and reaver)
 - Pixie Dust attacks (bully and reaver)
 - Bruteforce PIN attacks (bully and reaver)
 - Parameterizable timeouts
 - Known WPS PINs attack (bully and reaver), based on online PIN database with auto-update
 - Integration of the most common PIN generation algorithms
- WEP All-in-One attack (combining different techniques: Chop-Chop, Caffe Latte, Hirte, Fragmentation, Fake association, etc.)
- Compatibility with many Linux distributions (see [Requirements] section)
- Easy targeting and selection in every section
- Drag and drop files on console window for entering file paths
- Dynamic screen resolution detection and windows auto-sizing for optimal viewing
- Controlled Exit. Cleaning tasks and temp files. Option to keep monitor mode if desired
- Multilanguage support and autodetect OS language feature (see [Supported Languages] section)
- Help hints in every zone/menu for easy use
- Auto-update. Script checks for newer version if possible

---

### Requirements

Bash **4.2** or later.

Compatible with any Linux distribution that has installed the tools needed. The script checks for them at the beginning.

> `airgeddon` is already included in some Linux distributions and repositories:
> - [Wifislax] 4.12, 64-1.0 or higher
> - [BlackArch] 2017.01.28 or later
> - [ArchStrike] repository

<!-- Distribution compatibility should be written here -->
<details open>
	<summary id="distros"><strong>Tested on these compatible Linux distributions</strong></summary>
- *Kali 2.0, 2016.1, 2016.2 and arm versions (Raspberry Pi)*
- *Wifislax 4.11.1, 4.12 and 64-1.0*
- *Backbox 4.5.1 and 4.6*
- *Parrot 2.2.1 to 3.4.1 and arm versions (Raspberry Pi)*
- *BlackArch 2016.01.10 to 2017.01.28*
- *Cyborg Hawk 1.1*
- *Debian 7 (Wheezy) and 8 (Jessie)*
- *Ubuntu/Xubuntu 15.10, 16.04 and 16.04.1*
- *OpenSUSE Leap 42.1 and 42.2*
- *CentOS 6 and 7*
- *Gentoo 20160514 and 20160704*
- *Fedora 24*
- *Red Hat 7 (Maipo)*
- *Arch 4.6.2-1 to 4.9.11-1*
- *Raspbian 7 (Wheezy) and 8 (Jessie) (Raspberry Pi)*
- *OpenMandriva LX3*
</details>

<!-- HTML entities here: http://www.amp-what.com/unicode/search/%2F%26%5Cw%2F -->
#### Essential tools &#8592; The script does not work if you don't have installed all of them

 Command     | Possible package name | &#149;  | Command     | Possible package name 
:------------|:----------------------|:-------:|:------------|:----------------------
 ifconfig    | net-tools             | &#9474; | iwconfig    | wireless-tools        
 iw          | iw                    | &#9474; | awk         | awk \| gawk           
 airmon-ng   | aircrack-ng           | &#9474; | airodump-ng | aircrack-ng           
 aircrack-ng | aircrack-ng           | &#9474; | xterm       | xterm                 

#### Optional tools &#8592; Not necessary to work, only needed for some features

 Command     | Possible package name    | &#149;  | Command  | Possible package name                                
:------------|:-------------------------|:-------:|:---------|:-----------------------------------------------------
 wpaclean    | aircrack-ng              | &#9474; | ettercap | ettercap \| ettercap-text-only \| ettercap-graphical 
 crunch      | crunch                   | &#9474; | etterlog | ettercap \| ettercap-text-only \| ettercap-graphical 
 aireplay-ng | aircrack-ng              | &#9474; | sslstrip | sslstrip                                             
 mdk3        | mdk3                     | &#9474; | dhcpd    | isc-dhcp-server \| dhcp-server \| dhcp               
 hashcat     | hashcat                  | &#9474; | dnsspoof | dsniff                                               
 hostapd     | hostapd                  | &#9474; | wash     | reaver                                               
 lighttpd    | lighttpd                 | &#9474; | reaver   | reaver                                               
 iptables    | iptables                 | &#9474; | bully    | bully                                                
 bettercap   | bettercap                | &#9474; | pixiewps | pixiewps                                             
 beef        | beef-xss \| beef-project | &#9474; | unbuffer | expect \| expect-dev                                 

##### Important tips about BeEF

 - The right software you must install is **BeEF** (Browser Exploitation Framework). Be careful, do not mistake it with **beef** (Flexible Brainfuck Interpreter). This package has the same name and executable file name on some distributions and can lead into confusion. Anyway, `airgeddon` is able to detect the issue and displays a warning if needed. Here is a link to the right [BeEF installation's page].
 - If you are using a distribution which already has BeEF installed like Kali, BlackArch or Wifislax, there will be no problems. If you have manually installed BeEF, `airgeddon` is able to manage the integration asking for the path where it's installed, even modifying its own code in order to make updates-proof persistent changes.

#### Update tools &#8592; Not necessary to work, only used for auto-update

 Command | Possible package name 
:--------|:----------------------
 curl    | curl                  

#### Internal tools &#8592; These are internally checked. Not necessary to work, good to have

 Command  | Possible package name                  
:---------|:---------------------------------------
 xdpyinfo | x11-utils \| xdpyinfo \| xorg-xdpyinfo 
 ethtool  | ethtool                                
 lspci    | pciutils                               
 rfkill   | rfkill                                 

It is highly recommended to have the internal tools installed. They improve functionality and performance. For example, `xdpyinfo` allows the script to detect the display resolution in order to print on windows in a better way (size and position).

Of course, the script also uses many standard basic tools that are supposed to be included in any Linux distribution, so they are not checked (cp, rm, grep, pgrep, egrep, md5sum, uname, echo, hash, cat, sed, etc.).

A command could be included in different packages, depending on the distribution.

---

### Usage

It is essential to run this script as **root**, otherwise `airgeddon` won't work properly.

<details open>
	<summary id="gettingStarted"><strong>Getting Started</strong></summary>
- Clone the repository
 - `git clone https://github.com/v1s1t0r1sh3r3/airgeddon.git`
- Go to the newly created directory
 - `cd airgeddon`
- Run it (remove **sudo** if you already have root permissions)
 - `sudo bash airgeddon.sh`
</details>

`airgeddon` should be launched with **bash** `bash /path/to/airgeddon.sh` and not with `sh` or any other kind of shell. <br/>

If you launch the script using another shell, there will be *Syntax errors* and faulty results.
Even with no initial errors, they will appear later. Always launch with **bash**!

---

### Supported Languages

![English][English] English <br/>
![Spanish][Spanish] Spanish <br/>
![French][French] French <br/>
![Catalan][Catalan] Catalan <br/>
![Portuguese][Portuguese] Portuguese <br/>
![Russian][Russian] Russian <br/>
![Greek][Greek] Greek <br/>

---

### Known Incompatibilities

- Incompatible with Mac OSX at the moment
 - *Bash version* &#8592; it can be avoided by upgrading it using `brew` or whatever, this is not the real problem :smile:
 - *Aircrack suite* &#8592; this suite does not support `airodump` and `aireplay` for OSX
 - *Wireless tools* &#8592; `iwconfig` does not exist in OSX, so `airport` command cannot be used. It generates different outputs
- Incompatible with OpenBSD and FreeBSD. They are Unix systems but they have some differences with Linux
 - *Bash* &#8592; They have no bash. It can be installed, this is not the real problem again :sweat_smile:
 - *Wireless tools* &#8592; `iwconfig` does not exist in these systems, they use `ifconfig` instead and it generates different outputs

---

### Contributing

- Translations into other languages
- More distribution support compatibility
- New features
- More WPS pins for the database
- Testing and feedback

Read the [Contributing File] for more details on the process of project collaborating and on our code of conduct.

---

### Changelog

Read the [Changelog File] to review changes.

---

### Disclaimer & License

<a href="LICENSE.md"><img src="http://gplv3.fsf.org/gplv3-127x51.png" align="left" hspace="10" vspace="6"></a>

This script must be used for educational purposes and penetration testing only. <br/>
Use it on your own networks or with the permission of the network's owner only.<br/>
`airgeddon` staff is not responsible of its use in any case.

---

### Acknowledgments
<!-- Links are missing, should be replaced -->

[Kcdtv] for French translations, beta testing, suggestions about new features and support received since the beginning, <br/>
**USUARIONUEVO** for helping me to improve the script, suggestions about new features and for the support received, <br/>
**El padrino** and [cLn] for Catalan translations, <br/>
[Luan] for Portuguese translations, <br/>
[MiAl] for Russian translations, <br/>
[xtonousou] for Greek translations, beta testing, suggestions, the help received fixing code warnings and other stuff, <br/>
[OscarAkaElvis] for allowing me to own his body when I visit the earth.

#### Hat tip to

- The "Spanish pentesting crew"
- The [Wifislax] staff
- The [BlackArch] community
- The forum people of [Seguridadwireless.net], [Wifi-libre.com] and [Lampiweb.com]
- The [Hackware.ru] admins
- All the people who helped building the online PIN database for WPS
- Dominique Bongard for bringing to us the Pixie Dust attacks
- Zhao Chunsheng and Stefan Viehböck for their wonderful algorithms
- All the developers who made and designed the third-party tools that `airgeddon` uses

#### Inspiration
<!-- Links are missing, should be replaced -->

- [vk496] &#8594; Linset
- MI1 &#8594; Airstorm
- [MatToufoutu] &#8594; Ap-fucker
- Coeman76 &#8594; Handshaker
- Goyfilms &#8594; Goyscript
- [Kcdtv] &#8594; WPSPin

<!-- Anchors -->
[Features]: #features
[Essential Tools]: #essential-tools--the-script-does-not-work-if-you-dont-have-installed-all-of-them
[Optional Tools]: #optional-tools--not-necessary-to-work-only-needed-for-some-features
[BeEF Tips]: #important-tips-about-beef
[Update Tools]: #update-tools--not-necessary-to-work-only-used-for-auto-update
[Internal Tools]: #internal-tools--these-are-internally-checked-not-necessary-to-work-good-to-have
[Requirements]: #requirements
[Usage]: #usage
[Supported Languages]: #supported-languages
[Known Incompatibilities]: #known-incompatibilities
[Contributing]: #contributing
[Changelog]: #changelog
[Disclaimer & License]: #disclaimer--license
[Acknowledgments]: #acknowledgments
[Hat Tip To]: #hat-tip-to
[Inspiration]: #inspiration
<!-- Links To Images -->
[Banner]: /imgs/banners/airgeddon_banner.png "We will conquer the earth!!"
[English]: /imgs/flags/us.png "English"
[Spanish]: /imgs/flags/es.png "Spanish"
[French]: /imgs/flags/fr.png "French"
[Catalan]: /imgs/flags/cat.png "Catalan"
[Portuguese]: /imgs/flags/pt.png "Portuguese"
[Russian]: /imgs/flags/ru.png "Russian"
[Greek]: /imgs/flags/gr.png "Greek"
<!-- Links To MDs -->
[Changelog File]: CHANGELOG.md
[Contributing File]: CONTRIBUTING.md
[License File]: LICENSE.md
<!-- URLs -->
[Wifislax]: http://www.wifislax.com
[BlackArch]: https://blackarch.org
[ArchStrike]: https://archstrike.org/wiki
[BeEF installation's page]: https://github.com/beefproject/beef/wiki/Installation
[Seguridadwireless.net]: http://foro.seguridadwireless.net
[Wifi-libre.com]: https://www.wifi-libre.com
[Lampiweb.com]: http://lampiweb.com/foro
[Hackware.ru]: https://hackware.ru
<!-- Github URLs -->
[vk496]: https://github.com/vk496
[MatToufoutu]: https://github.com/mattoufoutu
[Kcdtv]: https://github.com/kcdtv
[cLn]: https://github.com/cLn73
[Luan]: https://github.com/Luan7805
[MiAl]: https://github.com/Mi-Al
[xtonousou]: https://github.com/xtonousou
[OscarAkaElvis]: https://github.com/OscarAkaElvis
<!-- Badges URLs -->
[Version-shield]: https://img.shields.io/badge/version-6.1-blue.svg?style=flat-square&colorA=273133&colorB=0093ee "Latest version"
[Bash4.2-shield]: https://img.shields.io/badge/bash-4.2%2B-blue.svg?style=flat-square&colorA=273133&colorB=00db00 "Bash 4.2 or later"
[License-shield]: https://img.shields.io/badge/license-GPL%20v3%2B-blue.svg?style=flat-square&colorA=273133&colorB=bd0000 "GPL v3+"
[Paypal-shield]: https://img.shields.io/badge/donate-paypal-blue.svg?style=flat-square&colorA=002f86&colorB=009cde "Show me the money!"
[Bitcoin-shield]: https://img.shields.io/badge/donate-bitcoin-blue.svg?style=flat-square&colorA=273133&colorB=f7931a "Show me the money!"
