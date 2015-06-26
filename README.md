# sql-dump-git-commit
Semi-automatic MAMP SQL dumps on git commit

## Overview
Currently, this utility is designed to run on Mac using MAMP. If someone wants to fork this and add onto 
it to provide more compatibility for other platforms (Windows, MAMP-alternatives, etc) that's fine. I will 
likely add Windows support to it at some point, but not anytime soon.

The functionality works as follows:

* User commits code to their local repo
* User intentionally includes a "#sql" within the first 10 lines of their commit message
* The installed git hook will automatically create an SQL dump of the configured database and put it in **./sql-dump/<current git user's email>/**

Configuration for MAMP SQL server creds, database name, etc are provided in the sql-dump.config file, which is expected 
to be located in the root of your repo. Gitignore files should be configured to ignore this file as it's an environment-specific 
file. SQL dumps are intentionally separated by git user so that any developer can import another's SQL dump if he needs 
to. Each SQL dump is automatically committed to the repo and will therefore be diffed the same as any code/text file.

## Installation
Installation is simple and is done by inserting the "commit-msg" and "post-commit" bash script files into your repo's .git/hooks/ 
folder. Make sure you have the "execute" bit set for those files (chmod +x .git/hooks/commit-msg, etc) so git can execute 
the file.

Insert the sql-dump.config into the root of your repo and set any of the variables you need. There are a couple of 
default variables in the commit-msg script that you can override.

## Other Thoughts
A lot of git commit sql dump solutions tend to make timestamped sql dumps, which did nothing for us other than take up 
more hard drive space, and since git versions everything anyway, you can always pull an SQL dump out for any commit via 
cherrypick or checkout. Our team shares DB dumps a lot when we're helping each other out, or when someone takes over an 
existing project and someone else has to check their progress. We are planning on creating another SQL import utility 
to quickly import these scripts as well.

## Disclaimer
I don't claim to be a bash expert, nor do I claim to have much effort into this solution, but it works great for us. 
Suggestions are welcome. Let me know if you have any issues.