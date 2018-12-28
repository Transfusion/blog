title: 'Understanding an OSS project, the no B$ way'
tags: []
categories: []
date: 2017-12-20 19:47:00
---
You may be here because you have been thinking about getting more than just foot-deep into FOSS. Maybe you're here to build your portfolio like I am because you just fukin graduated from school and you have no shit to show besides a  Perhaps you think the curve is steep. Well no s\*\*\* it is steep, and code doesn't write itself. Let's write some fucking real code.

Pick an issue that you feel confident working on and dive the f\*\*\* in.

https://github.com/qutebrowser/qutebrowser/issues/3256 Here is one issue I picked, simply because I think I know Python pretty well, such as decorators, inheritance and threading.

Now unless you are already a Vim pro with a fancy ctags setup, in which case you wouldn't be here, its time to get your f\*\*\* ing IDE set up and a text editor with powerful search capabilities so you don't waste your precious time `hjkl`ing around like you're trying to play Minecraft southpaw. 

I'm reading the documentation so I don't waste time asking and waiting for a reply. I'm going to do this fast and quick. https://github.com/qutebrowser/qutebrowser/blob/master/doc/contributing.asciidoc

I do `tox -e mkvenv-pypi` from within the cloned qutebrowser directory, it creates the `.venv` dir automatically, I open it up as a project in PyCharm, and I configure the project interpreter to the created venv. I right click the file containing the `if __name__ == '__main__':` line and run through the tutorials twice. I'm ready to code now.

I'll work on the first part; extending the `:version` command with a `--paste` argument. I figure if I can get this working there should probably be some internal hook for the JS to interact with Python itself for the button bit. Now I'm wondering, I need a fuckin pastebin client, and what's all this bull about "Qt slots and signals." I open up Sublime Text, drag the qutebrowser inside. I hit Cmd-Shift-F and do a global search for pastebin. I Google pyqtSlot(). http://pyqt.sourceforge.net/Docs/PyQt5/signals_slots.html#PyQt5.QtCore.pyqtSlot Big fuckin deal, it seems like some glamorized callback.


