# The Best Terminal Command: xkill

_Tristan Goodell on Opinion | 07 Sep 2018_

Today, I will be presenting hands-down one of the best Linux terminal commands: `xkill`. [Xkill](https://www.x.org/archive/current/doc/man/man1/xkill.1.xhtml) is a terminal command that usually comes with most Linux distrobutions. It is really handy because if an application ceases to work, you can simply 'xkill it': causing all processes to cease.

This command is incredibly handy if, say, your web browser freezes and you cannot close the application under normal circumstances. Just `ctrl + alt + t` to open up a new terminal window and type in `xkill`.  Your cursor will turn into an `x`. Next, click the window of the application that is not functioning normaly. The window will close and you can move on with life! It is incredibily handy.

According to the official documentation:

> Xkill is a utility for forcing the X server to close connections to clients. This program is very dangerous, but is useful for aborting programs that have displayed undesired windows on a user’s screen. If no resource identifier is given with -id, xkill will display a special cursor as a prompt for the user to select a window to be killed. If a pointer button is pressed over a non-root window, the server will close its connection to the client that created the window.

When used correctly, xkill can be an invaluable tool to your everyday workflow. It is wise to use with caution however. You may accidentally xkill a process that you didn't mean to.

---

## How to Get Xkill

If your linux distrobution does not already come with the easy to use xkill, you can easily install it using the terminal commands below.

### Ubuntu

`sudo apt-get install xorg-xkill`

### Fedora

`sudo yum install xorg-xkill`

### Arch

`sudo pacman -S xorg-xkill`

Sadly, there is no mainstream equivalant of xkill on Windows or OSX, however there were talks of a Windows [port](https://www.ghacks.net/2008/10/18/windows-xkill/) here. The post has not been updated since 2013, so I am unsure if it would even work.

There have been several threads talking about a potential xkill port to OSX, however I have not found any concrete releases at the time of writing this.
