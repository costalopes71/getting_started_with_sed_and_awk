# Getting Started with AWK, SED and GREP

## Grep

The --color=auto will highlight the matched patterns :
```
grep --color=auto <pattern> file
``` 

Display the number of matches :
```
grep -c <regex> <input>
grep -c '^#' my_script.sh # will print number of lines that start with #
``` 

Search for the string banana in all files at /home/ :
```
grep banana /home/*
```


Other flags:

    -i : makes the search case insensitive
    -v : reverse de search, example: grep -v banana --> it will print everyhing but banana
    -A : print n lines after the match. Example: grep -A2 banana
    -B : print n lines before the match. Example: grep -B2 banana
    -C : print n lines before and after the match (C stand for context). Example: grep -C2 banana


## Sed

### Print Command

Will print the content of the file supressing the standard output :
```
sed -n 'p' <file>
# -n: will supress the standard output
# 'p': will print the content
```
  
will print the content of the file but will remove all lines started with # :
```
sed '/^#/ d' /etc/crontab
``` 
  
Adds a range. Will print only the first 3 lines :
```
sed -n '1,3 p' /etc/passwd
```
  
Print from line 5 to the end of the document :
```
sed -n '5,$ p' /etc/passwd
```
  
Edit the file (in-place) and creates a backup of the original file :  
```
sed -i.bkp '/^#/ d' /etc/banana.conf
# -i: will really edit the file (in-place)
# -i.<sufix>: will really edit the file but will do a backup of the original file with the sufix
```
  
### Substitute Command
Substitute some string by a replacement (will not edit the file)
The g option: will substitute every occurence in the line, without -g it will substitute only the first match in the line

Usually the delimiter for the substitute command is /
```
sed '[optional_range] s[delimiter]<string>[delimiter]<replacement>[delimiter]'
``` 

Will print the line begining with developer and will substitute /bin/bash for /bin/banana (in this example we are using @ as the delimiter) :
```
sed -n '/^developer/ s@/bin/bash@/bin/banana@ p ' /etc/passwd
```

Will print the line begining with developer and will substitute /bin/bash for /bin/banana (in this example we are using @ as the delimiter) globally because of the g option at the end of substitute command :    
```
sed -n '/^developer/ s@/bin/bash@/bin/banana@g p ' /etc/passwd
``` 

### Append Insert and Delete commands

Append a new line after a line :
```
sed ' /^server 3/ a append.a.new.line.after.the.line.starting.with.server.3' /etc/ntp.conf
```

Insert a new line before a line :
```
sed ' /^server 3/ i insert.a.new.line.before.the.line.starting.with.server.3' /etc/ntp.conf
```

Delete lines from a file :
```
sed ' /^server\s[0-9]\.ubuntu/ d ' /etc/ntp.conf
# deletes the line that begin with 'server [some_number].ubuntu' from the file
```


## Awk

Begin statement do some command before the file starts, End statement do some command after the end of the file.
```
awk 'BEGIN {print "banana header\n" } { print NR,$0} END { print NR }' <file>
# NR: prints the line number
# $0 is the whole line
``` 

Filter lines that contain the string ether and print the second field with uppercase letters :
```
ifconfig wlp2s0 | awk '/ether/ { print toupper($2) }'
```

