## Building and installing [DWM](http://dwm.suckless.org/) from source
<!-- TODO: write the intro -->

## Table of Contents
- [Prerequisites](#prerequisites)
- [Cloning dwm source code](#cloning-dwm-source-code)

## Prerequisites
We need to install the following tools to build and install dwm:

```bash
sudo xbps-install -S git vim make gcc libX11-devel libXft-devel libXinerama-devel
```

> [!NOTE]
> `libX11-devel` or `libX` or `Xlib` is header files for `X11`, you can found them in `/usr/include/X11/*`.
> Try issuing the following command to list the `X11` programming `header files`
```bash
ls /usr/include/X11/
```


## Cloning dwm source code
> [!TIP]
> creating `src` dir in your `home/userName` to save or download source code of the programs that you build from source,
> is a good practice


- We going to clone [dwm](http://dwm.suckless.org/) source code using `git`,to do so run the following command to clone the [dwm](http://dwm.suckless.org/) source code:

```bash
mkdir -p ~/src                           # create src dir under your home
cd ~/src                                 # change dir to ~/src
git clone https://git.suckless.org/dwm   # clone dwm in ~/src dir
```
- Exploring `dwm` files:<br>
In the `src` dir, where we've cloned `dwm` in, let `tree` it

```bash
tree dwm  # list contents of dwm dir
```
_The output:_
```
dwm/
├── config.def.h
├── config.mk
├── drw.c
├── drw.h
├── dwm.1
├── dwm.c
├── dwm.png
├── LICENSE
├── Makefile
├── README
├── transient.c
├── util.c
└── util.h
```
## Building and Install `DWM`
1. In order to build and insatall `dwm`, first change the directory to `dwm` dir by issuing the command:
```bash
cd ~/src/dwm
```
2. Then, fire the following command, to build and install `dwm` and remove (clean) unwanted files:
```bash
sudo make install clean
```
`dwm` should be successfully installed in your machine and ready to go.<br>
But, if we don't have [Xorg-Server](), `dwm` can't be start !!, so let's setup our `X-Server` `(>^.^<)`

## Installing `Xorg-Server` step by step
The following steps will be in deep detail a bit.

```bash
xbps-install -S xorg-server   # it'll be there -> /usr/libexec/Xorg
```
`X-server` is simply a server, that listen to `GUI` programs like `dwm`.
In this level we can't execute/run `X-server`, because it needs some system informations to be passed to it as arguments.<br>
Thus, we need to install `StartX` to do the job, which is a script, that comes with a package called `Xinitrc`,
to pass the required arguments to `X-server` for us, and automate it for the next time as well.

- first of all let's install `xinit`
```bash
sudo xbps-install -S xinit   # xinit is actually a set of scripts wrapper to X-server
```
Try typing the following command to Start `X-server`!!
```bash
startx   # it's a script, that comes with xinit package
```
It fails, doesn't it ?!, we still need to install another package called `xauth`.
But, before going ahead, let's have a quick look at `startx` script, you can found it here `/usr/bin/startx`,
open it with a text-editor of your choice, I'm using `vim`:
```bash
vim /usr/bin/startx   # it's a BASH script !!
```
However, let's install `xauth` package to go ahead, as you guess:
```bash
xbps-install -S xauth
```
Now, if you try the command `startx` it'll fail again, but in this time we can pass to it our `dwm` via `~/.xinitrc`,
you maybe see something like this in the list of error massages `xinitrc: 'number': /etc/X11/xinint/xinitrc`.
However, `xinitrc` is a configuration file, and the `/etc/X11/xinint/xinitrc` is the default configuration file, that comes with
`xinit` package.<br>
But, we're going to create our own `xinitrc` configuration file, and making `xinit` to start our `dwm`!!
```bash
cd ~           # change directory to your home dir
vim .xinitrc   # pick your favorite editor <i3 and create the file
```
type in the `~/.xinitrc` the following:
```
dwm
```
save and quit, and try again the command `startx`, you'll notce that, things this time look different,
and maybe you see that error at the very bottom, that says something like:
`cannot load font from name: 'monospace:size=10'`.<br>
So far so good, the last error that I've mention above about loading font, it comes actually from our `dwm` `(>^.^<)`,
actually `Void Linux` doesn't have `monospace` font installed, but first of all, please open the following file:
```bash
vim ~/src/dwm/config.h     # or set the right path, where you save DWM source code.
```
and look closely at `line:8`, that contains:
```c
static const char *fonts[]          = { "monospace:size=10" };
```
is this make sense to you?! And where you see something like this??.<br>

So I guess you know that what the next, let's do it:
- Installing fonts:
you can query about fonts like this way:
```bash
xbps-query -Rs monospase            # you'll see a list of fonts name in the  result
# (OR)
xbps-query -Rs xorg | grep "font"   # this command will grep the Xorg fonts
```
after your select fonts of your choice, then let's install them:
```bash
xbps-install -S xorg-fonts          # I choose xorg-fonts and you?
```
Remember that we need monospace font for now to run our `dwm`, letter we'll see how to change the fonts `(>-.^<)`.<br>

For last time type the following command:
```bash
startx             # it should work Now!!!
```
if it works then please let me know `(>^.^<)`.<br>
Unfortunately you may stuck with `dwm`, every thing will be frozen!? Why that?
> [!TIP]
> If you face this problem, then please try hit `CTRL+ALT+F3 or F4` to open new `tty`, or reboot your machine/VM
Well, `Xorg` can't handle input form your devices like the keyboard for example, thus we need to install additional package called
`xorg-input-drivers`:
```bash
xbps-install -S xorg-input-drivers      # it allows handle inputs
```
Now, your keyboard and mouse should work fine, and if you press `ALT+SHIFT+ENTER` will open a `Terminal`,
but, it won't open any terminal?!, well we need to install a `Terminal`, do you have any favorite terminal?! `(>^.^<)`.
By The Way, hitting `ALT+SHIFT+q` by default will exit `dwm` and bring you back to `TTY` terminal!,
we going to modify key-binds letter as well.

## [Installing `ST` Terminal](st.md)
Please hit this link [ST Terminal](st.md) to continue, it is just couple of lines of instructions.

