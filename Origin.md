# Origin

[Origin](https://www.origin.com) is an online gaming, digital distribution and digital rights management platform developed by Electronic Arts that allows users to purchase games for PC and mobile platforms.

To install Origin, you can use our Lutris installer: https://lutris.net/games/origin

The following is a list of issues and workarounds found when using it under Wine.

## Issues with Origin:

**Update:** The following might not be necessary anymore. If you still have problems then go ahead and use the script.

***

### Updating Origin:

Origin has a tendency to break when it requires an update. For example, you will probably see this after the client tries to update:

![Screenshot from 2020-05-02 08-22-36](https://user-images.githubusercontent.com/10602045/80855948-3f909880-8c4e-11ea-809b-58a5599fad81.png)

To fix this issue, simply close/stop the game from Running, and launch it again.
Origin will try to update itself again and this time, it will succeed.


### Origin In-Game

Origin's overlay, Origin In-Game, doesn't run well under Wine and because of this we recommend you disable it to avoid any potential issues. If a game requires it for certain features go ahead and enable it but no guarantees!

### Issues with tiling window managers

Origin is composed of multiple smaller windows that tiling window managers usually don't know how to manage, causing issues like Origin being unusably slow, the window looking empty, or crashes.

To fix this, add `origin.exe` to the exceptions of your window manager. For example, add to your i3/Sway configuration file:

```
for_window [instance="origin.exe"] floating enable
```

You can also fix this by enabling `Windowed (virtual desktop)` on Lutris's runner options.

### Game Installs:

Origin tends to have a tough time installing some things. Here's a list of workarounds:

- If your download stops at "Playable":

  - Open the progress view and press the <a href="https://i.imgur.com/8Vv0bva.png">play icon</a> until it resumes downloading.

- VCrun errors out:

  - VCRun tends to fail when installing from Origin if the Lutris runtime is disabled. This can be avoided by making sure "Disable Lutris Runtime" is unticked in the game's system options tab <b>before</b> downloading any games that call for it.

- Directx fails to install when finalizing a download: 

  - Open `/drive_c/Program Files (x86)/Origin Games/Game Name/__Installer/directx/redist` and remove all the `.cab` files.
  - Only these three files should remain: `dsetup32.dll` `DSETUP.dll` and `DXSETUP.exe`
  - Proceed with the installation.

<p align="center">
  <img width="328" height="131" src="https://i.imgur.com/2j6y0u3.png">
</p>

- .NET fails to download (using FIFA 19 as an example):

  - Copy `vc_redist.x64.exe` found in `drive_c/Program Files (x86)/Origin Games/FIFA 19/__Installer/vc/vc2015/redist`
  - Place `vc_redist.x64.exe` into the dotnet redist folder `__Installer/dotnet/dotnet4client/redist`
  - Rename `dotNetFx40_Client_x86_x64.exe` to `dotNetFx40_Client_x86_x64.exe.bak` and rename `vc_redist.x64.exe` to `dotNetFx40_Client_x86_x64.exe`
  - Continue with your install

- If your download has been paused due to permission errors.
  > Your download has been paused.
  > 
  > Origin needs to download files and is waiting for permission. Please choose "Yes" when Windows prompts you for permission.
  - To fix this, simply re-enable IPv6 in your kernel (i.e. remove `ipv6.disable=1` from the kernel command line).
<p align="center">
  <img width="582" height="309" src="https://user-images.githubusercontent.com/65068529/81470778-eba52700-91ec-11ea-83cb-ed25d394800e.png">
</p>
