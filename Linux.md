## Running SMT on Linux using Bottles

For the rare few out there wanting to run SMT under Linux, it's relatively straightforward to get it working using [Bottles](https://usebottles.com/).

Here are the basic steps involved:

1. Install Bottles however you like. Note that if you run Bottles via Flatpak you'll need to give it permission to wherever your EVE logs live (see below).
2. Download SMT from https://github.com/Slazanger/SMT/releases - the zip file ending with `_Setup.zip` has an installer file that simplifies setup. Unzip this file so you have access to `SMT_Setup.msi`.
3. In Bottles, create a new bottle using the "Application" environment. Click on the bottle, then click "Dependencies". Install the `dotnetcoredesktop6` and `allfonts` dependencies.
4. In the bottle details screen, look for the button in the upper right that has three vertical dots (the "seconday menu") and then click "Browse Files". This should open your file browser pointing to the directory containing the files for the bottle. Copy in the `SMT_Setup.msi` file from wherever you unzipped it earlier (doesn't really matter where you put it).
5. Back in the bottle details screen, click "Legacy Wine Tools" and then "Explorer". This should open a file explorer inside the bottle. Find the `SMT_Setup.msi` file and double-click to install, using whatever choices you prefer (the defaults should be fine).
6. Back in the bottle details again, click the three vertical dots and then click "Search for new programs". There should now be an "SMT" entry under "Programs". Clicking on it should bring up SMT, but you may need some other setting changes if it doesn't work (see below).

Once SMT is installed, you'll need to configure Bottles to add a Windows drive to get access to your EVE log files. This is under "Settings", "Compatibility", "Manage Drives". For example, if you're running under Steam create an `E:` drive pointing to `~/.steam/debian-installation/steamapps/compatdata/8500/pfx/drive_c/users/steamuser/Documents/EVE`. Adjust to wherever your `Documents/EVE` directory lives. Try `find ~/.steam -name EVE` if you're running via Steam. **Note**: if you're running Bottles via Flatpak you'll need to run this to grant access to your `~/.steam` directory: `flatpak override --user com.usebottles.bottles --filesystem=~/.steam`

Now inside SMT go to "File", "Preferences", "General" and click "Set custom log folder". Change it to `E:\logs` (or wherever you chose earlier) and then restart SMT. If all went well, you should start seeing intel reports in the "Intel" pane in the lower left.

If SMT doesn't run:

- try enabling "Discrete Graphics" in the bottle display settings. It may not work without this if your Nvidia settings are set to use the GPU all the time.
- try changing the "Runner" value - if the default runner (e.g. `soda-8.0-2`) doesn't work, try Wine (e.g. `sys-wine-9.0` if you have Wine installed separately), or try different runners by installing them under Preferences from the main Bottles screen.
- if the `dotnetcoredesktop6` dependency mentioned earlier isn't exactly what SMT needs, try downloading and installing the .NET Desktop Runtime from [here](https://download.visualstudio.microsoft.com/download/pr/d0849e66-227d-40f7-8f7b-c3f7dfe51f43/37f8a04ab7ff94db7f20d3c598dc4d74/windowsdesktop-runtime-6.0.29-win-x64.exe).

Good luck!
