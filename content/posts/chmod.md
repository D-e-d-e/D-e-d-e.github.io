+++
title = "Chmod"
date = "2026-08-15T22:45:38+02:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = "Denis Sabau"
tags = ["linux", "commands", "ctf"]
description = "Reflecting on usage of chmod: differences between high pressure situations and architectural decisions."
showFullContent = false
+++

Today I completed one of pwn.college's challenges about the `chmod` command. I was wondering why symbolic notation (`u+x`, `g-w`) is the preferred way to teach the usage of this command, since I really think that octal notation (`0755`) is much more versatile and intuitive. 

After a little analysis of the use cases, I found 2 different cases in which one notation may outperform the other.

### CTFs
During attack-defense ctfs, where making a hot-patch or launching an exploit must be done as quickly as possible, using the symbolic notation is clearly faster, since you can just run `chmod +x file`, and don't really need to check previous permissions of the file.

It's more elegant: you just flip the execution bit on leaving the rest untouched, saving some seconds (and brain energy) instead of calculating octal sums.

### The architecture
On the other hand, when you are writing code for projects that involve more low-level programming, it is necessary to not mess up permissions. For this specific task (which is probably more common in real-world scenarios compared to the previous one), using octal notation is more intuitive, and it's very easy to modify specific permissions like SUID (`4755`).

That's why I think octal notation should be thaught right from the start: it's cleaner, more secure (since it forces you to really calculate the octal value of the permission), and probably more useful for everyday tasks.


