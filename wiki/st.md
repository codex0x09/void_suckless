## Building and Installing ST Terminal

[ST](https://st.suckless.org/), or Simple Terminal, that's written in C programming language, if you like C-lang then it for you.<br>
I use Alacrity Terminal for a while, but now, I'm going to switch to `ST` terminal from now on, because of programming purposes.

## Cloning `ST` Source Code:

```bash
xbps-install -S pkg-config              # dependency to build 'ST'
mkdir -p ~/src                          # make source 'src' directory if not exist
cd ~/src                                # change directory to 'src'
git clone https://git.suckless.org/st   # cloning 'ST' source code
```
Now, after cloning the `ST` source code, let's build it and install it
```bash
cd ~/src/st               # cd to st first
sudo make install clean   # build, install, and clean the tree
```

> [!NOTE]
> If `pkg-config` is not installed in the system, then  when building `ST` you'll encounter an errors such as:<br>
> * `/bin/sh: 1: pkg-config:not found` (this error will appear fore times),<br>
> because `pkg-config` used in the `config.mk` file, which `pkg-config` is used to be passed as a flag to the `CC` or `gcc` compiler.<br>
> By the way(btw), `config.mk` file is a configuration file for `Makefile`.
> * `fatal error: ft2build.h: No such file or directory | #include <ft2build>`<br>
> `ft2build.h` can be found in `/usr/include/X11/Xft/Xft.h` at line:40.

Done !!, now st is ready to go, just start your x-server by typing `startx` and enjoy `(>^.^<)`.
We didn't finish yet, we need to do some configurations, customizations, and more.

## [Next topic title](nex-topic-file-name)
Please hit this link [Next topic title](nex-topic-file-name) to continue.
