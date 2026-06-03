---
title: Editing Files With Nano in Linux [With Cheat Sheet]
source: https://itsfoss.com/nano-editor-guide/
author:
  - "[[Abhishek Prakash]]"
published: 2020-05-27
created: 2026-05-26
description: Though Nano is less complicated to use than Vim and Emacs, it doesn't mean Nano cannot be overwhelming. Learn how to use the Nano text editor.
tags:
  - "#nano"
  - "#editor"
---
Nano is the default [terminal-based text editor](https://itsfoss.com/command-line-text-editors-linux/) in Ubuntu and many other Linux distributions. Though it is less complicated to use than the likes of [Vim](https://www.vim.org/?ref=itsfoss.com) and [Emacs](https://www.gnu.org/software/emacs/?ref=itsfoss.com), it doesn’t mean Nano cannot be overwhelming to use.

In this beginner’s guide, I’ll show you how to use the Nano text editor. I will also include a downloadable PDF cheat sheet at the end of the article so that you can refer to it for practicing and mastering Nano editor commands.

Please expand the next section if you are just interested in a quick summary of Nano keyboard shortcuts.

## Essential Nano keyboard shortcuts

| Shortcut | Description |
| --- | --- |
| nano filename | Open file for editing in Nano |
| Arrow keys | Move cursor up, down, left and right |
| Ctrl+A, Ctrl+E | Move cursor to start and end of the line |
| Ctrl+Y/Ctrl+V | Move page up and down |
| Ctrl+\_ | Move cursor to a certain location |
| Alt+A and then use arrow key | Set a marker and select text |
| Alt+6 | Copy the selected text |
| Ctrl+K | Cut the selected text |
| Ctrl+U | Paste the selected text |
| Ctrl+6 | Cancel the selection |
| Ctrl+K | Cut/delete entire line |
| Alt+U | Undo last action |
| Alt+E | Redo last action |
| Ctrl+W, Alt+W | Search for text, move to next match |
| Ctrl+\\ | Search and replace |
| Ctrl+O | Save the modification |
| Ctrl+X | Exit the editor |

## How to use Nano text editor

I presume that you have Nano editor installed on your system already. If not, please your distribution’s package manager to install it.

I have also created a video showing all the essentials in a hands-on video. You may watch it or just read the article here.

![](https://www.youtube.com/watch?v=NCisjUG4OL4)

### Getting familiar with the Nano editor interface

If you’ve ever [used Vim](https://itsfoss.com/pro-vim-tips/) or Emacs, you’ll notice that using Nano is a lot simpler. You can start writing or editing text straightaway.

Nano editor also shows important keyboard shortcuts you need to use for editing at the bottom of the editor. This way you won’t get stuck at [exiting the editor like Vim](https://itsfoss.com/how-to-exit-vim/).

The wider your terminal window, the more shortcuts it shows.

![Nano Editor Interface](https://itsfoss.com/content/images/wordpress/2020/05/nano-editor-interface.png)

Nano Editor Interface

You should get familiar with the symbols in Nano.

- The caret symbol (^) means Ctrl key
- The M character mean the Alt key

When it says “^X Exit”, it means to use Ctrl+X keys to exit the editor. When it says “M-U Undo”, it means use Alt+U key to undo your last action.

### Open or create a file for editing in Nano

You can open a file for editing in Nano like this:

```
nano my_file
```

If the file doesn’t exist, it will still open the editor and when you exit, you’ll have the option for saving the text to my\_file.

You may also open a new file without any name (like new document) with Nano like this:

```
nano
```

### Basic editing

You can start writing or modifying the text straightaway in Nano. There are no special insert mode or anything of that sort. It is almost like using a regular text editor, at least for writing and editing.

As soon as you modify anything in the file, you’ll notice that it reflects this information on the editor.

![Nano Modified Text](https://itsfoss.com/content/images/wordpress/2020/05/nano-modified-text.png)

Nano Modified Text

Nothing is saved immediately to the file automatically unless you explicitly do so. When you exit the editor using Ctrl+X keyboard shortcut, you’ll be asked whether you want to save your modified text to the file or not.

### Moving around in the editor

Mouse click doesn’t work here. Use the arrow keys to move up and down, left and right.

You can use the Home key or Ctrl+A to move to the beginning of a line and End key or Ctrl+E to move to the end of a line. Ctrl+Y/Page Up and Ctrl+V/Page Down keys can be used to scroll by pages.

If you want to go a specific location like last line, first line, to a certain text, use Ctrl+\_ key combination. This will show you some options you can use at the bottom of the editor.

![Nano Editor Jump To Line](https://itsfoss.com/content/images/wordpress/2020/05/nano-editor-jump-to-line.png)

Jump to a specific line in Nano

### Cut, copy and paste in Nano editor

If you don’t want to spend too much time remembering the shortcuts, use mouse.

Select a text with mouse and then use the right click menu to copy the text. You may also use the Ctrl+Shift+C [keyboard shortcut in Ubuntu](https://itsfoss.com/ubuntu-shortcuts/) terminal. Similarly, you can use the right click and select paste from the menu or use the Ctrl+Shift+V key combination.

**Nano specific shortcuts for copy and pasting**

Nano also provides its own shortcuts for cutting and pasting text but that could become confusing for beginners.

Move your cursor to the beginning of the text you want to copy. Press Alt+A to set a marker. Now use the arrow keys to highlight the selection. Once you have selected the desired text, you can Alt+6 key to copy the selected text or use Ctrl+K to cut the selected text. Use Ctrl+6 to cancel the selection.

Once you have copied or cut the selected text, you can use Ctrl+U to paste it.

![Nano Editor Set Mark](https://itsfoss.com/content/images/wordpress/2020/05/nano-editor-set-mark.png)

Nano Editor Set Mark

### Delete text or lines in Nano

There is no dedicated option for deletion in Nano. You may use the Backspace or Delete key to delete one character at a time. Press them repeatedly or hold them to delete multiple characters.

You can also use the Ctrl+K keys that cuts the entire line. If you don’t paste it anywhere, it’s as good as deleting a line.

If you want to delete multiple lines, you may use Ctrl+K on all of them one by one.

Another option is to use the marker (Ctrl+a). Set the marker and move the arrow to select a portion of text. Use Ctrl+K to cut the text. No need to paste it and the selected text will be deleted (in a way).

### Undo or redo your last action

Cut the wrong line? Pasted the wrong text selection? It’s easy to make such silly mistakes and it’s easy to correct those silly mistakes.

You can undo and redo your last actions using:

- Alt+U: Undo
- Alt +E: Redo

You can repeat these key combinations to undo or redo multiple times.

### Search and replace

If you want to search for a certain text, use Ctrl+W, enter the term you want to search, and press enter. The cursor will move to the first match. To go to the next match, use Alt+W keys.

![Nano Editor Basics: Search for Text](https://itsfoss.com/content/images/wordpress/2020/05/nano-search-text.png)

Nano Editor Basics: Search for Text

By default, the search is case-insensitive. You can also use regex for the search terms.

If you want to replace the searched term, use Ctr+\\ keys and then enter the search term and press enter key. Next it will ask for the term you want to replace the searched items with.

![Nano Editor Tips: Search and Replace](https://itsfoss.com/content/images/wordpress/2020/05/nano-editor-search-replace.png)

Nano Editor Tips: Search and Replace

The cursor will move to the first match and Nano will ask for your conformation for replacing the matched text. Use Y or N to confirm or deny respectively. Using either of Y or N will move to the next match. You may also use A to replace all matches.

![Nano Editor Basics: Replace Confirm](https://itsfoss.com/content/images/wordpress/2020/05/nano-editor-search-replace-confirm.png)

Nano Editor Basics: Replace Confirm

### Save your file while editing (without exiting)

In a graphical editor, you are probably used to of saving your changes from time to time. In Nano, you can use Ctrl+O to save the changes you made to the file. It also works with a new, unnamed file.

![Nano Editor Tips: Save While Writing](https://itsfoss.com/content/images/wordpress/2020/05/nano-editor-save-while-writing.png)

Nano Editor Tips: Save While Writing

Nano shows this keyboard shortcut at the bottom but it’s not apparent. It says “^O Write Out” which means to use Ctrl+O (it is the letter O, not the number zero) to save your current work. Not everyone can figure that out.

In a graphical text editor, you probably use Ctrl+S to save your changes. Old habits die hard but they could cause trouble. Out of habit, if you accidentally press Ctrl+S to save your file, you’ll notice that the terminal freezes and you can do nothing.

If you accidentally press Ctrl+S press Ctrl+Q nothing can be scarier than a frozen terminal and losing the work.

### Save and exit Nano editor

To exit the editor, press Ctrl+X keys. When you do that, it will give you the option to save the file, or discard the file or cancel the exit process.

![Save and Exit Nano editor](https://itsfoss.com/content/images/wordpress/2020/05/nano-editor-save-and-exit.png)

Save and Exit Nano editor

You can also do that if you want to save the modified file as a new file (save as function in usual editors). When you press Ctrl+X to exit and then Y to save the changes, it gives the option to which file it should save. You can change the file name at this point.

You’ll need to have ‘write permission’ on the file you are editing if you want to save the modifications to the file.

### Forgot keyboard shortcut? Use help

Like any other terminal based text editor, Nano relies heavily on keyboard shortcuts. Though it displays several useful shortcuts at the bottom of the editor, you cannot see all of them.

It is impossible to remember all the shortcuts, especially in the beginning. What you can do is to use the Ctrl+G keys to bring up the detailed help menu. The help menu lists all the keyboard shortcuts.

![Nano Editor Help Menu](https://itsfoss.com/content/images/wordpress/2020/05/nano-editor-help-menu.png)

Nano Editor Help Menu

### Always look at the bottom of the Nano editor

If you are using Nano, you’ll notice that it displays important information at the bottom. This includes the keyboard shortcuts that will be used in the scenario. It also shows the last action you performed.

![Nano Editor Hints](https://itsfoss.com/content/images/wordpress/2020/05/nano-editor-hints.png)

Nano Editor Hints

If you get too comfortable with Nano, you can get more screen for editing the text by disabling the shortcuts displayed at the bottom. You can use Alt+X keys for that. I don’t recommend doing it, to be honest. Pressing Alt+X brings the shortcut display back.

## Download Nano cheatsheet \[PDF\]

There are a lot more shortcuts and editing options in Nano. I am not going to overwhelm you by mentioning them all.

Here’s a quick summary of the important Nano keyboard shortcuts you should remember. The download link is under the image.

![Nano Editor Cheatsheet](https://itsfoss.com/content/images/wordpress/2020/05/nano-cheatsheet.png)

Nano Editor Cheatsheet

You can download the cheatsheet, print it and keep at your desk. It will help you in remembering and mastering the shortcuts.

I hope you find this beginner’s guide to Nano text editor helpful. If you liked it, please share it on Reddit, [Hacker News](https://news.ycombinator.com/?ref=itsfoss.com) or in various [Linux forums](https://itsfoss.community/?ref=itsfoss.com) you frequently visit.

I welcome your questions and suggestions.