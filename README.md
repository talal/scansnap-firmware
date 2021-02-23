# Scansnap firmware

The following is a quick way to get my ScanSnap S1300i working on [Pop!_OS](https://pop.system76.com/).

## Installation

1. Download firmware

    ```
    sudo mkdir -p /usr/share/sane/epjitsu
    sudo cp scansnap-firmware/1300i_0D12.nal /usr/share/sane/epjitsu/.
    sudo cpan upgrade sane
    sudo apt-get install sane sane-utils libsane libsane-dev
    ```

2. Ensure that scanner is detected by USB stack:

    ```
    $ lsusb | grep Fujitsu
    Bus 003 Device 012: ID 04c5:128d Fujitsu, Ltd ScanSnap S1300i
    ```

    and that its USB ID shows up in the SANE backend it needs:

    ```
    $ grep 128d /etc/sane.d/epjitsu.conf
    usb 0x04c5 0x128d
    ```

3. Adjust permissions to access scanner as a non-root user

    Add the following to `/etc/udev/rules.d/79-scanner.rules`:

    ```
    # Fujitsu ScanSnap S1300i
    ATTRS{idVendor}=="04c5", ATTRS{idProduct}=="128d", MODE="0664", GROUP="scanner", ENV{libsane_matched}="yes"
    ```

    You can get id(s) using `lsusb`.

    Add yourself to the `scanner` group:

    ```
    sudo usermod -a -G scanner <username>
    ```

4. Enable `saned`:

    ```
    sudo systemctl enable saned.socket
    ```

5. Logout, and then re-login. Try [Simple Scan](https://launchpad.net/simple-scan), and the scanner should work. 

    Read `/etc/sane.d/epjitsu.conf`, if needed.
