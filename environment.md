# Software Environments

This page details the various software environments available for use in CDC,
where the primary aim is to support development using GNU Radio. It describes
how to access these environments outside of EDS12.

Please don't hesitate to contact me if you encounter any environment related
issues.

## Content

1. [FEIT GPU Desktop](#feit-gpu-desktop)
    - [Ubuntu VM](#ubuntu-vm)
    - [MATLAB/Simulink](#matlab-simulink)
2. [Personal Computer Installation](#personal-computer-installation)

## FEIT GPU Desktop

The FEIT Desktop used on the lab computers in EDS12 is available to you outside
of workshop through myUniApps. To access the environment:

1. Open a browser and navigate to
[https://unimelb.cloud.com](https://unimelb.cloud.com)
2. Login with your university credentials
3. If you wish, install Citrix Workspace on your personal computer by
clicking *Detect Workspace*, otherwise click *Use web browser*
4. Navigate to *Desktops > All Desktops*
5. Open a session by selecting *FEIT GPU Desktop*
6. Login to Windows using your university credentials

Obviously, you will not be able to interface with the SDR hardware when
accessing the remote desktop, but you can still perform much of your software
development and debugging.

> **WARNING:** The FEIT GPU Desktop is **non-persistent** – locally saved data
> may be lost when you log out. Make sure to save any files you wish to keep to
> another location, e.g., your OneDrive account.

## Ubuntu VM

The main environment we will be using is an Ubuntu Linux virtual machine (VM) in
which we can run GNU Radio. This option will allow stable usage of the Nuand
bladeRF SDR hardware that will be the focus of the design project. Additionally,
extending GNU Radio functionality through the creation and compilation of C++
signal processing blocks is straightforward under Linux.

On the FEIT GPU Desktop, the Ubuntu Linux VM can be accessed as follows.

1. Start VirtualBox: *Start Menu > Oracle VM VitualBox > Oracle VM VirtualBox*
2. Select the *ELEN90089_2023* virtual machine
3. Click the start button to launch the virtual machine
4. Login to Ubuntu using the following credentials\
username: cdc\
password: sdr

To open Python or GRC, first open a bash shell by clicking on the Terminal icon
in the dock: ![terminal icon](images/terminal.png). The Python interpreter can
then be launched at the command line.
```
$ python3
```
Similarly, GRC can be launched from the command line.
```
$ gnuradio-companion
```

## MATLAB / Simulink

A support package for accessing the Nuand bladeRF has been installed should you
want to access a device in MATLAB and/or Simulink. Make sure to launch
**MATLAB R2022b**. See the following pages for documentation on how to use
the bladeRF SDR in MATLAB/Simulink.

- [Communications Toolbox Support Package for BladeRF 2.0](https://www.mathworks.com/matlabcentral/fileexchange/74591-communications-toolbox-support-package-for-bladerf-2-0)

## Personal Computer Installation

Coming soon...
