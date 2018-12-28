title: BitMessage on the CLI
url: 110.html
id: 110
categories:
  - Messaging
date: 2013-12-31 23:29:05
tags:
---
[https://github.com/Dokument/PyBitmessage-Daemon](https://github.com/Dokument/PyBitmessage-Daemon) [https://bitmessage.org/wiki/Compiling_instructions#Download_and_run_PyBitmessage](https://bitmessage.org/wiki/Compiling_instructions#Download_and_run_PyBitmessage)

> sudo apt-get install python openssl git python-qt4 ... Download the source code from github: git clone https://github.com/Bitmessage/PyBitmessage $HOME/PyBitmessage Run PyBitmessage: ~/PyBitmessage/src/bitmessagemain.py If you receive a warning that you need to use python 2.7.5 or greater, and have followed the above instructions to upgrade it, your system may be attemping to run PyBitmessage with python 3. Run: python2 ~/PyBitmessage/src/bitmessagemain.py

You can leave python-qt4 out. After your first run of bitmessagemain.py, it will return this:

```
2013-12-31 23:14:08,057 - DEBUG - reloading keys from keys.dat file
2013-12-31 23:14:08,167 - DEBUG - reloading subscriptions...
```

PyBitmessage requires PyQt unless you want to run it as a daemon and interact with it using the API. You can download PyQt from http://www.riverbankcomputing.com/software/pyqt/download or by searching Google for 'PyQt Download'. If you want to run in daemon mode, see https://bitmessage.org/wiki/Daemon

`Error message: No module named PyQt4`

Then follow these instructions: [https://bitmessage.org/wiki/Daemon](https://bitmessage.org/wiki/Daemon) Result: [![screenshot_142](/wp-content/uploads/2013/12/screenshot_142-300x281.png)](/wp-content/uploads/2013/12/screenshot_142.png) An interesting POC Vanity address generator (singlethreaded, written in Python, don't expect much): [https://bitmessage.org/forum/index.php?topic=1727.0](https://bitmessage.org/forum/index.php?topic=1727.0)