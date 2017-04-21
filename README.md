# About
[![Gitter](https://badges.gitter.im/Join\ Chat.svg)](https://gitter.im/sidorares/node-x11?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
 X11 protocol client for node.js

 Implements core X11 protocol, as well as Xrender, Damage, Composite, Big-Requests, Dpms, Screensaver, XFixes, Shape, XTest, XC-Misc, GLX and Apple-WM extensions.
# install

`npm install x11`

Windows users:
1) install [XMing](http://www.straightrunning.com/XmingNotes/) or [Cygwin/X](http://x.cygwin.com/)
2) get node-x11 copy (using [git](http://code.google.com/p/msysgit/downloads/list?can=3) or from [Github](https://github.com/sidorares/node-x11/archives/master ))

#CI build status:

[![Build Status](https://secure.travis-ci.org/sidorares/node-x11.png)](http://travis-ci.org/sidorares/node-x11)

# example

Core requests usage:

```js
    var x11 = require('x11');

    var Exposure = x11.eventMask.Exposure;
    var PointerMotion = x11.eventMask.PointerMotion;

    x11.createClient(function(err, display) {
        if (!err) {
            var X = display.client;
            var root = display.screen[0].root;
            var wid = X.AllocID();
            X.CreateWindow(
                wid, root,        // new window id, parent
                0, 0, 100, 100,   // x, y, w, h
                0, 0, 0, 0,       // border, depth, class, visual
                { eventMask: Exposure|PointerMotion } // other parameters
            );
            X.MapWindow(wid);
            var gc = X.AllocID();
            X.CreateGC(gc, wid);
            X.on('event', function(ev) {
                if (ev.type == 12)
                {
                    X.PolyText8(wid, gc, 50, 50, ['Hello, Node.JS!']);
                }
            });
            X.on('error', function(e) {
                console.log(e);
            });
	    } else {
		    console.log(err);
        }
    });
```

# Screenshots

  ![tetris game](https://lh6.googleusercontent.com/-RCRY9A7WwnA/Tlww0FHP7NI/AAAAAAAAAwo/nxfSxsw6xow/s400/tetris.png)
  ![XRENDER gradients](https://lh4.googleusercontent.com/-VS0BMYYmq6M/Tlww0Y1ij0I/AAAAAAAAAws/pVWsPZ63Yeo/s400/render-gradients.png)
  ![OpenGL glxgears](http://img-fotki.yandex.ru/get/4123/37511094.30/0_81712_6c2ebb11_L)
  ![OpenGL teapot](http://img-fotki.yandex.ru/get/4132/37511094.30/0_81713_82a5ac48_L)

# In use
  - [ntk](https://github.com/sidorares/ntk) - higher level toolkit on top of X11
  - [node-remote](https://github.com/AndrewSwerlick/node-remote) - media center controller
  - [tiles](https://github.com/dominictarr/tiles) - tiling window manager
  - [vnc](https://github.com/sidorares/node-vnc) - vnc client.
  - [node-ewmh](https://github.com/santigimeno/node-ewmh) - set of EWMH helpers.
  - [OdieWM](https://github.com/bu/OdieWM) - window manager
  - [Dbusmenu](https://github.com/sidorares/node-dbusmenu) - unity global menu client.
  - [AirWM](https://github.com/AirWM/AirWM) - tiling window manager
  - [npdf](https://github.com/sidorares/npdf) - pdf viewer
  - [tinywm](https://github.com/Airblader/node-tinywm) The famous [TinyWM](https://github.com/mackstann/tinywm) written in node.js
  - [basedwm](https://github.com/anko/basedwm) Infinite-desktop panning X window manager in LiveScript

# X11 resources/documentation:

  - [Xplain](https://github.com/magcius/xplain) - A series of articles to help explain the X Window System http://magcius.github.io/xplain/article/
  - [Official X11 docs](http://www.x.org/releases/X11R7.6/doc/) 
  - [protocol specification](http://www.x.org/releases/X11R7.6/doc/xproto/x11protocol.pdf)
  - C Xlib to X11 request mapping table http://tronche.com/gui/x/xlib/appendix/a.html
  - [How to write composite manager](http://www.talisman.org/~erlkonig/misc/x11-composite-tutorial/)
  - [Extended Window Manager Hints specification](http://standards.freedesktop.org/wm-spec/wm-spec-1.3.html)

# Other implementations

  - C: XLib - http://www.sbin.org/doc/Xlib/ http://www.tronche.com/gui/x/xlib/ http://www.x.org/docs/X11/xlib.pdf
  - C: XCB - http://xcb.freedesktop.org/
  - Python:  http://sourceforge.net/projects/python-xlib/ ( github fork: https://github.com/Ademan/python-xlib-branch pypi: http://pypi.python.org/pypi/Python%20Xlib )
  - https://github.com/alexer/python-xlib-render
  - Python/twisted:  https://launchpad.net/twisted-x11
  - Perl: http://search.cpan.org/~smccam/X11-Protocol-0.56/Protocol.pm
  - Go: https://github.com/BurntSushi/xgb
  - Java: https://github.com/xderoche/J11
  - Ruby: https://github.com/dj2/x-ruby-bindings
  - Clojure: https://github.com/noodlewiz/xcljb
  - Guile: https://github.com/mwitmer/guile-xcb

# Server side (protocol + functionality) implementations for js + DOM

would be really great to make completely web based playground page, connecting node-x11 api to DOM based implementation 

  - https://github.com/GothAck/javascript-x-server
  - https://github.com/ttaubert/x-server-js
