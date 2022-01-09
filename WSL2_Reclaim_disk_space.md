    # WSL2 a Good Alternative to Use UNIX Systems
### Autor Luiz Carlos
Date: 30/12/2021


# What is the Windows Subsystem for Linux?

The Windows Subsystem for Linux lets developers run a GNU/Linux environment -- including most 
command-line tools, utilities, and applications -- directly on Windows, unmodified, without the
overhead of a traditional virtual machine or dualboot setup.

WSL 2 is a new version of the Windows Subsystem for Linux architecture that powers the Windows 
Subsystem for Linux to run ELF64 Linux binaries on Windows. Its primary goals are to increase file
system performance, as well as adding full system call compatibility.


## Install

[link to full tutorial on how to install WSL2](https://docs.microsoft.com/en-us/windows/wsl/install)




## Reclain space alocated into wsl back to Windowns


''' Ubuntu app with miniconda install and some envs setuped, must use about 20Gb to work.
    Anything besides that, could be some space retained by the WSL, which can be return to 
    windowns with the following steps. '''




### For Windows 10 Home Optimize-VHD cmdlet

The follow command must be run in PowerShell as Administrator user.
```cmd
wsl --shutdown
diskpart
select vdisk file="C:\Users\"change_for_your_user_name"\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu20.04onWindows_79rhkp1fndgsc\LocalState\ext4.vhdx"
attach vdisk readonly
compact vdisk
detach vdisk

exit
```


### Windowns PRO Optimize (shrink) WSL 2 .vhdx

The following commands must be run in PowerShell as Administrator user.

Find a DistroFolder found at: $env:LOCALAPPDATA\Packages\

Examples:
* CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc
* CanonicalGroupLimited.Ubuntu20.04onWindows_79rhkp1fndgsc

```cmd
cd LOCALAPPDATA\Packages\REPLACE_IT_WITH_TARGET_DISTRO_FOLDERNAME\LocalState\

cd LOCALAPPDATA\Packages\CanonicalGroupLimited.Ubuntu20.04onWindows_79rhkp1fndgsc\LocalState\

wsl --shutdown

optimize-vhd -Path .\ext4.vhdx -Mode full
```


## Run wsl or your favorite terminal


## References and usefull links:
https://docs.microsoft.com/en-us/windows/wsl/about
https://docs.microsoft.com/en-us/windows/wsl/install

Instalation WSL2:
https://www.youtube.com/watch?v=_fntjriRe48&list=PLzEzeFOP0XCMKBXmNC55hYZOOKZll7vFa&index=4&t=222s&ab_channel=DavidBombal

Reclain disk space:
https://www.youtube.com/watch?v=wSHMFX-4i3g&list=PLzEzeFOP0XCMKBXmNC55hYZOOKZll7vFa&index=3&t=3s&ab_channel=NickJanetakis