# getting_started_with_sed_and_awk

## Grep

  grep --color=auto <pattern> file
    the --color=auto will highlight the matched patterns

  grep -c <regex> <input>
    display the number of matches. Example: grep -c '^#' my_script.sh (will print number of lines that start with #)

  grep banana /home/*
    search for the string banana in all files at /home/

  Other flags:

    -i : makes the search case insensitive
    -v : reverse de search, example: grep -v banana --> it will print everyhing but banana
    -A : print n lines after the match. Example: grep -A2 banana
    -B : print n lines before the match. Example: grep -B2 banana
    -C : print n lines before and after the match (C stand for context). Example: grep -C2 banana


## Sed

### Print Command
  sed -n 'p' <file>
    -n: will supress the standard output
    'p': will print the content
    example:
      sed '/^#/ d' /etc/crontab --> will print the content of the file but will remove all lines started with #

  sed -n '1,3 p' /etc/passwd
    adds a range. Will print only the first 3 lines
  
  sed -n '5,$ p' /etc/passwd
    will print from line 5 to the end of the document
  
  sed -i.bkp '/^#/ d' /etc/banana.conf
    -i: will really edit the file (in-place)
    -i.<sufix>: will really edit the file but will do a backup of the original file with the sufix

### Substitute Command
Substitute some string by a replacement (will not edit the file)

  g option: will substitute every occurence in the line, without -g it will substitute only the first match in the line

  sed '[optional_range] s[delimiter]<string>[delimiter]<replacement>[delimiter]'
    Usually the delimiter is /

  sed -n '/^developer/ s@/bin/bash@/bin/banana@ p ' /etc/passwd
    Will print the line begining with developer and will substitute /bin/bash for /bin/banana (in this example we are using @ as the delimiter)
    
  sed -n '/^developer/ s@/bin/bash@/bin/banana@g p ' /etc/passwd
    Will print the line begining with developer and will substitute /bin/bash for /bin/banana (in this example we are using @ as the delimiter) globally because of the g option at the end of substitute command.

### Append Insert and Delete commands


## Awk

  awk 'BEGIN {print "banana header\n" } { print NR,$0} END { print NR }' <file>
    NR: prints the line number
    begin and end are blocks where I can do something at the start and at the end
    $0 is the whole line

  ifconfig wlp2s0 | awk '/ether/ { print toupper($2) }'
    filter lines that contain the string ether and print the second field with uppercase letters
