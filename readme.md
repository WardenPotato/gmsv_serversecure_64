# gmsv_serversecure

A module for Garry's Mod that mitigates exploits on the Source engine.

Based on these plugins from AzuiSleet:

[serverplugin_serversecure][1]

[serverplugin_serversecure2][2]

[serversecure3][3]

## Compiling

Warning: this fork will only focus on supporting and building x64 linux builds, goto the original repo if your purpose is anything but this.

On Linux, everything should work fine as is, on **release** mode.

These restrictions are not random; they exist because of ABI compatibility reasons.

If stuff starts erroring or fails to work, be sure to check the correct line endings (`\n` and such) are present in the files for each OS.

### Compiling for linux(instructions partly borrowed from https://github.com/Earu/gm_win_toast)
1) Get [premake](https://github.com/premake/premake-core/releases/download/v5.0.0-alpha14/premake-5.0.0-alpha14-linux.tar.gz) add it to your `PATH`
2) Get [garrysmod_common](https://github.com/danielga/garrysmod_common) (with `git clone https://github.com/danielga/garrysmod_common --recursive --branch=x86-64-support-sourcesdk`) and set an env var called `GARRYSMOD_COMMON` to the path of the local repo
3) Run `premake5 gmake --gmcommon=$GARRYSMOD_COMMON` in your local copy of **this** repo
4) Navigate to the makefile directory (`cd /projects/linux/gmake`)
5) Run `make config=release_x86_64`

### Important information for pterodactyl users!

In order to switch your servers to 64bit on pterodactly two things need to be done.

1) You will need to modify the gmod egg to support switching branches luckily this is already natively supported but the catch is that its [not upstream yet](https://github.com/pterodactyl/panel/pull/3994#issuecomment-1064009658) so you will have to manually update the egg, you can download it [here](https://github.com/parkervcp/eggs/blob/master/stock_eggs/source-engine/egg-garrys-mod.json) when its downloaded simply goto your panel -> Admin -> Nests -> Source Engine -> Garrys Mod. Then under the tab configuration you will find a Egg File option, upload the file you downloaded earlier and then press the red "Update Egg" button.
2) Goto Panel -> Admins -> Servers -> (whichever server you want to make 64bit) -> Startup. Under the option "Startup Command Modification" change "./srcds_run" to "./srcds_run_x64" and set the option "Beta" to "x86-64" and Tick "Validate Serverfiles" on.

## Requirements

This project requires [garrysmod_common][4], a framework to facilitate the creation of compilations files (Visual Studio, make, XCode, etc). Simply set the environment variable '**GARRYSMOD_COMMON**' or the premake option '**gmcommon**' to the path of your local copy of [garrysmod_common][4].

We also use [SourceSDK2013][5]. The links to [SourceSDK2013][5] point to my own fork of VALVe's repo and for good reason: Garry's Mod has lots of backwards incompatible changes to interfaces and it's much smaller, being perfect for automated build systems like Azure Pipelines (which is used for this project).

  [1]: https://github.com/azuisleet/gmodmodules/tree/master/serverplugin_serversecure
  [2]: https://github.com/azuisleet/gmodmodules/tree/master/serverplugin_serversecure2
  [3]: https://github.com/azuisleet/gmodmodules/tree/master/serversecure3
  [4]: https://github.com/danielga/garrysmod_common
  [5]: https://github.com/danielga/sourcesdk-minimal
