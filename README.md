ssh.js
======

Inspired by my success with [socks5](http://github.com/kousu/socks5.js), I now intend to pour SSH over WebSockets.

**TIP** someone has already written ssh in javascript: [paramikojs](https://github.com/mimecuvalo/paramikojs); and it looks so godawfully overengineered and full of indirection that it might actually be really short to insert swap in WebSockets; see [this write() callback](https://github.com/mimecuvalo/firessh/blob/b31e19b7b058f7507e5c2c3251c16f50ad322d85/src/content/js/connection/ssh2.js#L127) which if you trace the paramiko code is the *only place the socket is actually used*

In combination with [termlib](http://www.masswerk.at/termlib/), this should provide end-to-end ssh sessions from the browser.


Competition
===========

* [consoleFISH](http://serfish.com/console/) - _which tunnels ssh, and has the cleartext at the server_
* [gotossh](http://www.gotossh.com/) - _for-profit ssh tunneling company_
* [shellinabox](https://code.google.com/p/shellinabox/) - _the only security is SSL_
* this [chrome extension](https://chrome.google.com/webstore/detail/secure-shell/pnhechapfaindjhompbnflcldabbghjo)
* this [firefox extension](http://firessh.mozdev.org/developers.html)
* a list on wikipedia: https://en.wikipedia.org/wiki/Web-based_SSH
