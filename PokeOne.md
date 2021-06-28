# How to install PokeOne on Linux (Ubuntu, Pop!_OS, Arch, Manjaro)

*Last updated 20/06/2021*

*© caevee (CC-BY 4.0)*

## Step 1: Update your system

#### Ubuntu/Pop!_OS

```bash
sudo apt update && sudo apt upgrade
```

#### Arch/Manjaro

```bash
sudo pacman -Syu
```

## Step 2: Install all needed packages

#### Pop!_OS

Simply install the Lutris package from the Pop!_Shop

#### Ubuntu

**!!! If this guide is out of date check the official [Lutris](https://lutris.net/downloads/) download page for the latest recommended install process !!!**

Add the Lutris PPA

```bash
sudo add-apt-repository ppa:lutris-team/lutris
```

Update your local package information so you can use the PPA

```bash
sudo apt update
```

Install the Lutris and Winetricks package

```bash
sudo apt install lutris winetricks wine
```

#### Arch

Since Arch strictly splits 64- and 32-bit packages you need to first enable the multilib repository to download winetricks relevant packages

To do so open the file `/etc/pacman.conf` inside your favorite text editor with root priviliges

```bash
sudo vim /etc/pacman.conf
```

Then uncomment search for `multilib` and uncomment the following two lines

Now update your local package information so you can install the 32-bit packages

```bash
sudo pacman -Syyu
```

Now you can install all necessary packages

```bash
sudo pacman -S lutris winetricks wine
```

#### Manjaro

Install all necessary packages via the Pamac GUI or with:

```bash
sudo pacman -S lutris winetricks wine
```

## Step 3: Download the P1 setup file for Windows

Open the [PokeOne Community](https://pokeonecommunity.com/) website and download p1setup.exe 

## Step 4: Setup the installer on Lutris

Open Lutris and click on the manage version button of Wine in your Lutris client.

Tick `lutris-6.10-2`. This is gonna download and extract the 6.10-2 runner.

*The reason we're specifying an exact version is because this is the latest version we know for sure works*

Now click the `+` sign on the top left corner of your Lutris client and set up following settings:

###### Game info:

* `Name` = `PokeOne`

* `Runner` = `Wine`

###### Game options

* `Executable` = `/home/{yourUsername}/Downloads/p1setup.exe` click on browse and select the downloaded p1setup.exe. 

* `Working directory` = `~/Games/PokeOne` or `/home/{yourUsername}/Games/PokeOne` both are valid. Just create a folder where you want your game to be saved and put its path in here.

* `Wine prefix` = exact same folder as `Working directory`

* `Prefix architecture` = `32-bit`

###### Runner options

Just unselect `Enable DXVK/VKD3D`

Now you can click `save`.

## Step 5: Run the installer

Run the game and go through the installation process. Don't change the install path and untick `Run PokeOne` at the end. When Wine requests for `Gecko` and `Mono` installs click install.

## Step 6: Change executable

Since the installation is done you can now change the executable to the launcher.exe.

Right-click the game in Lutris and press `configure`. Now inside of `Game options` you want to put a new path into `Executable`. The path will be

 `{yourWorkingDirectory}/drive_c/users/{yourUsername}/AppData/Roaming/PokeOne/Launcher.exe` 

or

 `{yourWorkingDirectory}/drive_c/users/{yourUsername}/Application Data/PokeOne/Launcher.exe`.

Just dig a little and you'll find it.

## Step 7: Assign ENV Variables for Winetricks

PokeOne needs .NET 4.6 to run properly and we use Winetricks to install that. First though we need to tell Winetricks what Wine architecture we're using and where to install .NET. to do so open your terminal and export these variables:

*Use autocomplete to make sure you're not misstyping anything. And make your life easier.*

The wine executable of the runner we're using

```bash
export WINE="/home/{yourUsername}/.local/share/lutris/runner/wine/{theRunnerWeAreUsing}/bin/wine"
```

Your working directory

```bash
export WINEPREFIX="/home/{yourUsername}/Games/PokeOne"
```

Our Wine architecture

```bash
export WINEARCH="win32"
```

## Step 8: Install .NET 4.6

```bash
sudo winetricks --self-update
```

```bash
winetricks dotnet46
```

The last command is gonna start the installation the process which takes **a while**.

Bring some coffee and watch your terminal freak out. Besides your terminal going crazy there will be three setups popping up where you just want to follow the instructions **except for rebooting**. When it asks for reboot just click `reboot later`.

**Don't continue until the setup is fully done and your terminal is ready again**

## Step 9: Enjoy

Open the game and let it patch. You should be able to play now.

*In some cases the client crashes when you don't click `Go!` immediately when you have the option to.*
