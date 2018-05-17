# active-action
Tool for running commands repeatedly so long as the screen is active.

Need a command running whenever your screen is on or off? Want to implement an activity tracking system using Unix tools? Send data to a server about system utilization when you're logged in?

active-action is a shell script that runs a command at a given interval so long as some other program (default: xscreensaver) isnt running. By default, it checks for xscreensaver and runs at an interval of 5 minutes, but the check condition and interval can be changed depending on your needs.

## Examples
~~~bash
# retrieve the specified url every 5 minutes the screen is actve
active-action -- curl www.mysite.com/active
~~~

~~~bash
# retrieve the specified url every 5 minutes the screen is inactive
active-action -r -- curl www.mysite.com/active
~~~

~~~bash
# run the custom script every 15 minutes that gnome-screensaver isnt running
active-action -i 15m -k gnome-screensaver -- my-custom-script
~~~

~~~bash
# run the custom script every 5 minutes user foo is logged in
active-action -k bash -u foo -- my-custom-script
~~~

## Options
~~~bash
 -h|--help           : this help
 -k|--check command  : command that isnt running when active \(default to xscreensaver \)
 -u|--user checkuser : user the command is running as \(default to \$USER \)
 -r|--reverse        : opposte: run when inactive instead
 -e|--explain        : dry-run / explain what it will do
 -v|--verbose        : explain what is being done
 -x|--errorexit      : exit on first error
 -o|--output file    : append command output to file
~~~

## Checks
active action can perform the following checks:

1. if `--check xscreensaver` (default) then it uses `xscreensaver-command` to determine whether the screensaver is active or not.
2. else, it will check if the program is running as the checkuser (default current user) via pgrep
