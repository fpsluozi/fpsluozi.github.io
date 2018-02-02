---
layout: post
title: [Teaching] General.asu LINUX Setup 
---

Below are the tool bundles for coding on ASU's remote Linux server.

Your OS | Command Line | File Transfer | Text Editor
--- | --- | --- | ---
**Windows** | [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/) | [WinSCP](https://winscp.net/eng/index.php)| [Notepad++](https://notepad-plus-plus.org/)
**MacOS** | Terminal / [iTerm](https://www.iterm2.com) | [Cyberduck](https://cyberduck.io) | [Sublime Text](https://www.sublimetext.com) / [VS Code](https://code.visualstudio.com) (Also available for Windows)
**Linux (Hardcore)** | Terminal | scp | vi / emacs

Additional notes
---
1. Hostname is general.asu.edu . Username/passowrd is the same with your ASU username/password.
`ssh yourasuusername@general.asu.edu`

2. Choose SFTP as the connection protocol on WinSCP/Cyberduck.

3. In the preferences of WinSCP/Cyberduck, you may select your favorite text editor as default to open \*.\* files. By doing so, you now can edit and synchronize your code files while working on them locally.

4. Never forget to refer to [Makefile Tutorial](http://mrbook.org/blog/tutorials/make/) when struggling with compiling.

5. Or email [me](mailto:yluo97@asu.edu) if you have any more concerns.
