ssh.ws
======

Inspired by my success with [socks5](http://github.com/kousu/socks5.ws), I now intend to pour SSH over WebSockets.

**TIP** someone has already written ssh in javascript: [paramikojs](https://github.com/mimecuvalo/paramikojs); and it looks so godawfully overengineered and full of indirection that it might actually be really short to insert swap in WebSockets; see [this write() callback](https://github.com/mimecuvalo/firessh/blob/b31e19b7b058f7507e5c2c3251c16f50ad322d85/src/content/js/connection/ssh2.js#L127) which if you trace the paramiko code is the *only place the socket is actually used*

In combination with [termlib](http://www.masswerk.at/termlib/), this should provide end-to-end ssh sessions from the browser.

Usage
=====

You should probably load this from a webserver to avoid javascript permission problems. The quickest one you probably have available is python's stdlib:

```
$ python3 -m http.server
```
or
```
$ python2 -m SimpleHTTPServer
```

You will also need to have sshd with password login working (which is the default).

Finally, since this is ssh.**ws** you need [websockify](https://github.com/kanaka/websockify/) or equivalent in front of it:
```
$ websockify 8022 localhost:22
```

Once you have those three(!) servers running, start your browser:
```
$ firefox http://localhost:8000
```

Competition
===========

Most of the competition uses a custom protocol over AJAX/Comet/WebSockets over SSL to a backend proxy which does the actual ssh'ing.
Of these, many protocols are simply that of a terminal emulator.
ssh.ws fills the niche of actually providing in-the-browser end-to-end ssh encryption.


* [consoleFISH](http://serfish.com/console/) - _which tunnels ssh, and has the cleartext at the server_
* [gotossh](http://www.gotossh.com/) - _for-profit ssh tunneling company_
* [shellinabox](https://code.google.com/p/shellinabox/) - _the only security is SSL_
* this [chrome extension](https://chrome.google.com/webstore/detail/secure-shell/pnhechapfaindjhompbnflcldabbghjo)
* this [firefox extension](http://firessh.mozdev.org/developers.html)
* a list on wikipedia: https://en.wikipedia.org/wiki/Web-based_SSH


ssh.ws still depends on a backend proxy, though to bridge WebSockets to the SSH tcp port;~
ssh.ws has been unapologetically designed and tested against using [websockify](https://github.com/kanaka/websockify/) for this backend proxy.

You could either install websockify in "single-server" mode
```
$ websockify 8022 localhost:22
```
which, in combination with the HTML files provided here, gives a great way to put an ssh login screen to your server on the web.

or use it in combination with [socks5.ws](http://github.com/kousu/socks5.ws) and [dante](http://www.inet.no/dante/) in "multi-server" mode
bridge you could be able to set this up only once and ssh to anywhere--but be careful not to accidentally make yourself an open proxy!!


Security
========

Most of the competition uses a proxy which sees your screen content and keystrokes in the clear. For example,
GotoSSH [says](http://www.gotossh.com/security)
_"We act as a middle-man between your web browser and the SSH session to your server machine. "_
and ConsoleFISH [says](serfish.com/console/web-ssh-security.jsp)
_"all of your communication is available in unencrypted form at the SSH tunnel"_
Further, client->proxy is usually run over SSL which we should all know by now is basically toast, crypto-wise.

ConsoleFISH claims this setup is true of "any other web SSH client" and it is true that ssh.ws
requires a proxy to translate WebSocket to TCP, but neither that proxy nor anyone sniffing client->proxy
ever sees the content because ssh is running in javascript, giving end-to-end authentication (via hostkeys) and encryption.

The most dangerous attack to ssh.ws is DNS/arp poisoning to compromise the copy of [paramikojs](https://github.com/mimecuvalo/paramikojs)
which you download.  There is no good all around solution for that, and in this respect FireSSH has a strong security advantage because,
like openssh, you download it--and if your distro is good, verify package signatures--once and for all.

