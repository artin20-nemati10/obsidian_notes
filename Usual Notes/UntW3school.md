# Linux Commands

Last update on November 07 2025 12:16:54 (UTC/GMT +8 hours)

A shell is a program that provides the traditional, text-only user interface for Linux and other Unix-like operating systems. The shell is an intermediary program which interprets the commands that are typed into a console (an all-text display mode) or terminal window (an all-text window) in a GUI (graphical user interface) and translates them into commands that the kernel (the core of the operating system) understands. A shell is the most fundamental way that a user can interact with the system, and the shell hides the details of the underlying operating system from the user. Almost all Linux distributions supply a shell program from the GNU Project called bash. The name "bash" is a Unix shell written by Brian Fox for the GNU Project as a free software replacement for the Bourne shell (sh). Released in 1989, it has been distributed widely as the shell for the GNU operating system and as a default shell on Linux and Mac OS X.

A shell prompt, also referred to as a command prompt is a character or set of characters at the start of the command line that indicates that the shell is ready to receive commands. It usually ends with a dollar sign ($) for ordinary users and a pound sign (#) for the root (i.e., administrative) user. The term command line is sometimes used interchangeably with the shell prompt, because that is where the user enters commands. For example, instructions for performing some activity might say "Enter the following at the command line," which is the same as saying "Enter the following at the shell prompt." However, a command line is not a program but rather just the space to the right of a shell prompt.

### Administrative Login

![linux login as a root](https://www.w3resource.com/w3r_images/linux-root-login.png)

### User Login

![linux user  login](https://www.w3resource.com/w3r_images/linux-user-login.png)

### Command Navigation

Here is a list of commonly used keyboard shortcuts using the default shell, bash :

|Keyboard shortcuts|Description|
|---|---|
|Up Arrow & Down Arrow|Previously used commands in the current session.|
|Ctrl-A|Move the cursor to beginning of the current line.|
|Ctrl-E|Move the cursor to the end of the current line.|
|Ctrl-U|Delete all the line from the start of the line to the current cursor position.|
|Ctrl-H|Same as backspace.|
|Ctrl-K|Delete all the line from the current cursor position.|
|Ctrl-W|Delete the word before the current cursor position.|
|Ctrl-D|On a blank line is the same as the exit command. Otherwise, it deletes the character in front of the cursor.|
|Ctrl-C|Stop the current running command.|
|Ctrl-Shift-C|Copy|
|Ctrl-Shift-V or Shift-Insert|Paste|
|Tab|Command completion.|

Let's work with some simple commands. The first one is an exit.

### exit

The exit command is used to exit the shell.

datasoft @ datasoft-linux ~$ exit

**clear**

The clear command is used to clear the terminal screen.

**help**

The help command is used to display information about commands

**Syntax:**

help [-d | -m  | -s]

**Example:**

```bash
datasoft @ datasoft-linux ~$ help exit
exit: exit [n]
    Exit the shell.
    
    Exits the shell with a status of N.  If N is omitted, the exit status
    is that of the last command executed.
 datasoft @ datasoft-linux ~$
```

**Option**:

**-d**

**Description**: Display a short description for each topic.

Example :

```bash
datasoft @ datasoft-linux ~$ help -d exit
exit - Exit the shell.
 datasoft @ datasoft-linux ~$
```

**Option**:

### -m

**Description**: Display usage in pseudo-manpage format.

Example:

```bash
datasoft @ datasoft-linux ~$ help -m exit
NAME
    exit - Exit the shell.

SYNOPSIS
    exit [n]

DESCRIPTION
    Exit the shell.
    
    Exits the shell with a status of N.  If N is omitted, the exit status
    is that of the last command executed.

SEE ALSO
    bash(1)

IMPLEMENTATION
    GNU bash, version 4.3.8(1)-release (i686-pc-linux-gnu)
    Copyright (C) 2013 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

 datasoft @ datasoft-linux ~$
```

**Option**:

**-s**

**Description**: Display a short usage synopsis for each topic matching.

Example:

```bash
datasoft @ datasoft-linux ~$ help -s exit
exit: exit [n]
 datasoft @ datasoft-linux ~$
```

Arguments: PATTERN  
If PATTERN is specified, gives detailed help on all commands matching PATTERN, otherwise the list of help topics is printed.

**Calendar**

Cal or ncal is used to display a calendar and the date of Easter. The cal utility displays a simple calendar in traditional format and ncal offers an alternative layout.

**Syntax:**

cal [-3hjy] [-A number] [-B number] [[month] year]  
cal [-3hj] [-A number] [-B number] -m month [year]  
ncal [-3bhjJpwySM] [-A number] [-B number] [-S country_code] [[month] year]  
ncal [-3bhjJeoSM] [-A number] [-B number] [year]
ncal [-CN] [-H yyyy-mm-dd] [-d yyyy-mm]  

**Example:**

```bash
datasoft @ datasoft-linux ~$ cal
    August 2014       
Su Mo Tu We Th Fr Sa  
                1  2  
 3  4  5  6  7  8  9  
10 11 12 13 14 15 16  
17 18 19 20 21 22 23  
24 25 26 27 28 29 30  
31                    
 datasoft @ datasoft-linux ~$ ncal
    August 2014       
Su     3 10 17 24 31
Mo     4 11 18 25   
Tu     5 12 19 26   
We     6 13 20 27   
Th     7 14 21 28   
Fr  1  8 15 22 29   
Sa  2  9 16 23 30   
 datasoft @ datasoft-linux ~$
```

Note: Not all options can be used together. For example "-3 -A 2 -B -y -m 7" means, show the three months around the seventh month, three before that, two after that and the whole year. ncal will warn about these combinations.

**Date**

The date command is used to display the current time in the given FORMAT, or set the system date. The command can display the date, time, time zone and more.

**Syntax:**

date [OPTION]..[+FORMAT]  
date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]

**Example:**

```bash
datasoft @ datasoft-linux ~$ date
Sat Aug 23 17:40:43 IST 2014
 datasoft @ datasoft-linux ~$
```

Note: Running date with no options will output the system date and time.

**Option**:

**-d, --date=STRING**

**Description**: Display time described by STRING, as opposed to the default, which is 'now'.

Examples:

```bash
datasoft @ datasoft-linux ~$ date --date="4/15/2015"
Wed Apr 15 00:00:00 IST 2015
 datasoft @ datasoft-linux ~$ date --date="15 apr 2015"
Wed Apr 15 00:00:00 IST 2015
 datasoft @ datasoft-linux ~$ date --date="Apr 15 2015"
Wed Apr 15 00:00:00 IST 2015
 datasoft @ datasoft-linux ~$
```

Display date of next Sunday :

```bash
datasoft @ datasoft-linux ~$ date
Sat Aug 23 17:46:37 IST 2014
 datasoft @ datasoft-linux ~$ date --date="next sun"
Sun Aug 24 00:00:00 IST 2014
 datasoft @ datasoft-linux ~$
```

Display past dates :

```bash
datasoft @ datasoft-linux ~$ date
Sat Aug 23 17:48:03 IST 2014
 datasoft @ datasoft-linux ~$ date --date='15 seconds ago'
Sat Aug 23 17:48:36 IST 2014
 datasoft @ datasoft-linux ~$ date --date='1 day ago'
Fri Aug 22 17:49:13 IST 2014
 datasoft @ datasoft-linux ~$ date --date='yesterday'
Fri Aug 22 17:49:29 IST 2014
 datasoft @ datasoft-linux ~$ date --date='1 month ago'
Wed Jul 23 17:49:52 IST 2014
 datasoft @ datasoft-linux ~$ date --date='2 years ago'
Thu Aug 23 17:50:14 IST 2012
 datasoft @ datasoft-linux ~
```

**Option**:

**-f, --file=DATEFILE**

**Description**: like --date once for each line of DATEFILE.

Example:

```bash
datasoft @ datasoft-linux ~$ cat datefile
datasoft @ datasoft-linux ~$ cat datefile
Feb 21 1993
Jan 02 2012
datasoft @ datasoft-linux ~$ date --file=datefile
Sun Feb 21 00:00:00 IST 1993
Mon Jan  2 00:00:00 IST 2012
 datasoft @ datasoft-linux ~$
```

**Option**:

**-r, --reference=FILE**

**Description**: display the last modification time of FILE.

**Option**:

**-R, --rfc-2822**

**Description**: output date and time in RFC 2822 format.

Example:

```bash
Mon, 07 Aug 2006 12:34:56 -0600
```

**Option**:

**--rfc-3339=TIMESPEC**

**Description**: output date and time in RFC 3339 format. TIMESPEC=‘date’, ‘seconds’, or ‘ns’ for date and time to the indicated precision.

Example: Date and time components are separated by a single space.

```bash
2006-08-07 12:34:56-06:00
```

**Option**:

**-s, --set=STRING**

**Description**: Set time described by STRINGS.

Example:

```bash
datasoft @ datasoft-linux ~$ date
Sat Aug 23 18:00:18 IST 2014
datasoft @ datasoft-linux ~$ date -s "08/23/2014 06:01:00"
Sat Aug 23 06:01:00 IST 2014
datasoft @ datasoft-linux ~$ date
Sat Aug 23 18:02:50 IST 2014
```

**Option** :

**-u, --utc, --universal**

**Description** :

Example:

```bash
datasoft @ datasoft-linux ~$ date
Sat Aug 23 18:05:23 IST 2014
 datasoft @ datasoft-linux ~$ date -u
Sat Aug 23 12:35:30 UTC 2014
 datasoft @ datasoft-linux ~$
```

**Various Date Command Formats**

**Syntax:**

date +%<format-option>

FORMAT controls the output. Interpreted sequences are :

|Options|Description|Related with|Values or example|
|---|---|---|---|
|%%|a literal %|||
|%a|Locale’s abbreviated weekday name|Date|Sun|
|%A|locale’s full weekday name|Date|Sunday|
|%b|locale’s abbreviated month name|Month|Jan|
|%B|locale’s full month name|Month|January|
|%c|locale’s date and time|Date and time|Thu Mar 3 23:05:25 2005|
|%C|century; like %Y, except omit last two digits|Century|20|
|%d|day of month (two digits, zero filled)|Day|01|
|%D|date; same as %m/%d/%y [_mm_/_dd_/_yy_]|Date|01/27/14|
|%e|day of month, space padded; same as %_d|Day|27|
|%F|full date; same as %Y-%m-%d|Date|2014-01-27|
|%g|last two digits of year of ISO week number (see %G)|Year|14|
|%G|year of ISO week number (see %V); normally useful only with %V|Year|2014|
|%h|same as %b|Month|Jan|
|%H|hour|Hours|00..23|
|%I|hour|Hours|01..12|
|%j|day of year|Day|001..366|
|%k|hour|Hours|0..23|
|%l|hour|Hours|1..12|
|%m|month|Month|01..12|
|%M|minute|Minutes|00..59|
|%n|a newline|||
|%N|nanoseconds ()|Seconds|000000000..999999999|
|%p|locale’s equivalent of either AM or PM; blank if not known|Hours|AM or PM|
|%P|like %p, but lower case|Hours|am or pm|
|%r|locale’s 12-hour clock time|Time|11:11:04 PM|
|%R|24-hour hour and minute; same as %H:%M|Time|10:23|
|%s|seconds since 1970-01-01 00:00:00 UTC|Seconds|1390831606|
|%S|second (00..60)|Seconds|30|
|%t|a tab|||
|%T|time; same as %H:%M:%S|Time|10:24:48|
|%u|day of week (1..7)|Day|1 is Monday|
|%U|week number of year, with Sunday as first day of week (00..53)|Week|04|
|%V|ISO week number, with Monday as first day of week (01..53)|Week|05|
|%w|day of week (0..6)|Day|0 is Sunday|
|%W|week number of year, with Monday as first day of week (00..53)|Week|04|
|%x|locale’s date representation|Date|01/27/2014|
|%X|locale’s time representation|Time|10:30:41 AM|
|%y|last two digits of year|Year|14|
|%Y|year|Year|2014|
|%z|+hhmm numeric timezone (e.g., -0400)|Time zone|+0530|
|%:z|+hh:mm numeric timezone (e.g., -04:00)|Time zone|+05:30|
|%::z|+hh:mm:ss numeric time zone (e.g., -04:00:00)|Time zone|+05:30:00|
|%:::z|numeric time zone with : to necessary precision (e.g., -04, +05:30)|Time zone|+05:30|
|%Z|alphabetic time zone abbreviation (e.g., EDT)|Time zone|IST|

**Example:**

# Display a date in mm-dd-yyyy format.

```bash
datasoft @ datasoft-linux ~$ date +%d-%m-%Y
23-08-2014
 datasoft @ datasoft-linux ~$
```