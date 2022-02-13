# IP Bot Script

## Installation

1. Open a terminal on your target machine (Jetson, NUC, or Raspberry Pi), or preferably connect to this machine over SSH.
2. Use `wget` to get the latest GitHub release of the installer.
3. Run the following command to execute the installer. Replace `<VERSION_NUMBER>` with the version number contained in the actual filename.

    ```bash
    sudo apt install ./send-ip_<VERSION_NUMBER>_all.deb
    ```

4. Run `send-ip -i` to initialize your script.
5. When prompted, enter the exact Discord webhook URL. You should be able to get this URL from a UMARV Discord admin. This step is why it is recommended that you do this setup process via SSH.
6. It is recommended that you enable auto-login for the machine, so that the script will run without you having to enter your password on the machine. You can do this by opening system settings, going into the user account section, and finding the option to enable automatic login.
7. The script should run automatically when you restart the machine! For more options, run `send-ip --help` in the terminal.

## Uninstallation

1. Run `sudo apt remove send-ip`
2. Run `rm ~/.config/UMARV.conf`
3. Run `rm ~/.config/autostart/send-ip.desktop`

## Development

### Building the .deb installer for the first time

1. Before cloning this repo, create a new build directory by running `mkdir send_ip_build`
2. Run `cd send_ip_build` to enter your build directory.
3. Clone this repo into your build directory by running the following command. (Cloning via the SSH url also works)

    ```bash
    git clone https://github.com/umigv/send_ip.git
    ```

4. Run `cd send_ip` to enter the cloned repository.
5. Run the following command to install the tools required to package the .deb file:

    ```bash
    sudo apt install git devscripts build-essential lintian debhelper
    ```

6. To generate the .deb file, run `./build.sh`
7. You should find a file called `send-ip_<VERSION_NUMBER>_all.deb` in your `send_ip_build` directory. This is the file you will want to deploy on all your other machines.

### Subsequent installer builds

1. Use `cd` to enter the directory where you cloned this repository. (`cd` into `send_ip_build/send_ip`)
2. Increment the version number in the `send-ip` script.
3. Add a new entry in `debian/changelog` with your updated version number. Add this new entry at the top of the file.
4. Run `./build.sh` to generate the .deb file.
5. You should find the updated .deb file in your `send_ip_build` directory.
6. Make sure to commit and push your updated `send-ip` and `debian/changelog` files before uploading the new .deb file to GitHub. This ensures that the release tag on GitHub aligns with the version number in your files.
