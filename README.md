# Scansnap firmware

The following is a quick and dirty way to get my Scansnap S1300 working on [Ubuntu][u], [Xubuntu][x], or [Elementary OS][e]. (This could possibly work on other Debian based linux too.)

1. Download firmware:

        git clone https://github.com/ckunte/scansnap-firmware.git

2. Run the following commands in a Terminal

        sudo mkdir -p /usr/share/sane/epjitsu
        sudo cp ~/Downloads/scansnap-firmware/* /usr/share/sane/epjitsu/.
        sudo cpan upgrade sane
        sudo apt-get install libsane-dev
        
3. Logout, and then re-login. Try [Simple Scan][ss], and the scanner should work.

[u]: http://www.ubuntu.com/
[x]: http://xubuntu.org/
[e]: http://elementary.io/ "elementary OS"
[ss]: https://launchpad.net/simple-scan "Simple Scanning Utility."