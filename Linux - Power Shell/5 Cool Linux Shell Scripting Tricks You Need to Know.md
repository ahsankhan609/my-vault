---
title: 5 Cool Linux Shell Scripting Tricks You Need to Know
source: https://python.plainenglish.io/5-cool-linux-shell-scripting-tricks-you-need-to-know-6197e9d23076
author:
  - "[[Frost]]"
published: 2026-01-14
created: 2026-06-13
description: 5 Cool Linux Shell Scripting Tricks You Need to Know In this article, you’ll learn practical shell scripting tricks you can actually use in everyday situations, like setting reminders, finding …
tags:
  - bash
  - best-practices
---
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*jqeE0Wi1sq2WgeQkd5SPhA.jpeg)

In this article, you’ll learn practical shell scripting tricks you can actually use in everyday situations, like setting reminders, finding large files, renaming many files at once, cleaning up your Downloads folder, and checking your internet connection.

Each example is simple, useful, and designed to demonstrate the power of shell scripting. So, let’s get started.

### Simple Reminder Script

Most people think reminders need a phone app or calendar, but Linux already has everything you need to make a tiny reminder assistant right in the terminal.

A reminder script is just a program that asks when you want to be reminded and shows your message.

Imagine telling your computer, “Hey, in 10 minutes, remind me to check the oven.” The script listens to your request, counts time silently, and pops up a message to you.

```c
read -p "Remind me in seconds: " time
read -p "Message: " message

sleep "$time"

echo "⏰ Reminder: $message"
```

Save it as remind.sh, make it executable and run the script:

```c
chmod +x remind.sh
./remind.sh &
```

Ten minutes later:

```c
⏰ Reminder: Check the oven
```

You don’t need complex tools to solve real problems. With a few lines of shell scripting, your terminal becomes your assistant.

### Find the Biggest File in a Folder

Finding the biggest file in a folder is a practical thing to know, especially when your disk is getting full, and you’re not sure what’s taking up all the space.

A very simple command looks like this:

```c
ls -S | head -1
```

This lists the files in the current folder, sorts them from biggest to smallest, and then shows only the first one. That first result is the largest file in that directory. For many everyday cases, this is enough and works instantly.

If you want to create a more friendly script that prints a friendly message, use:

```c
largest=$(ls -Sh | head -1)
echo "📦 Biggest file in this folder:"
echo "$largest"
```

This script makes the output easier to read and more pleasant. Remember, this method looks only at the current folder, not inside subfolders.

### Rename Hundreds of Files in One Shot

Renaming hundreds of files one by one is the kind of task that makes people hate computers. It’s slow, boring, and easy to mess up.

This is where Linux shell scripting comes in, because you can rename a whole group of files in one shot with just a few lines of code.

Imagine you have a folder full of images named like this:

```c
IMG_001.jpg
IMG_002.jpg
IMG_003.jpg
```

And you want them to be called something cleaner, like:

```c
holiday_1.jpg
holiday_2.jpg
holiday_3.jpg
```

Doing this by hand would be boring. So instead, you can use a simple shell loop:

```c
count=1

for file in *.jpg; do
  mv "$file" "holiday_$count.jpg"
  ((count++))
done
```

When you run this, the shell goes through every.jpg file in the folder. The count variable starts at 1 and increases after each file.

The mv command renames the file using that number. In a few seconds, all your files have new names.

### Auto-Clean Your Downloads Folder

Your Downloads folder is one of those places that quietly turns into a mess.

You download a PDF to read later, an installer you only need once, a random image someone sent you, and before you know it, the folder is full of old files you no longer need.

So, cleaning your Downloads folder is about letting your computer take care of that mess for you. A common example is deleting files that are more than a week old. This command does exactly that:

```c
find ~/Downloads -type f -mtime +7 -exec rm {} \;
```

You can also make the cleanup more friendly by turning it into a small script with a message:

```c
#!/bin/bash

echo "Cleaning old files from Downloads…"

find ~/Downloads -type f -mtime +7 -exec rm {} \;

echo "Downloads folder cleaned!"
```

Now it feels like a real tool instead of a random command. You can run it whenever you want and clean your folder.

### Detect Internet Connection

Detecting whether you have an internet connection is one of those small things that turns a simple script into a smart one.

Many tasks only make sense when the internet is available, like downloading updates, syncing files, or accessing the web. Instead of guessing, your script can quickly check the Internet connection.

A very common and friendly way to do this is with:

```c
if ping -c 1 google.com >/dev/null 2>&1; then
  echo "🌐 Internet is connected"
else
  echo "❌ No internet connection"
fi
```

When this runs, your system sends a tiny message to Google’s servers and waits briefly for a reply.

The -c 1 option means it only tries once. If it gets a response, the script prints a friendly message saying the “Internet is connected”. If it doesn’t, it prints “No internet connection”.

### Conclusion

[linux-commands](Linux%20Commands.md)
[Editing Files With Nano in Linux With Cheat Sheet](Editing%20Files%20With%20Nano%20in%20Linux%20With%20Cheat%20Sheet.md)
[Deprecated Linux Commands You Should Not Use Anymore](Deprecated%20Linux%20Commands%20You%20Should%20Not%20Use%20Anymore.md)
[10 Bash History Shortcuts Every Linux User Should Know](10%20Bash%20History%20Shortcuts%20Every%20Linux%20User%20Should%20Know.md)
