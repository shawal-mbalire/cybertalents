# Mailer


Category: Digital Forensics
Level: easy
Points: 50

## Description

We got the evidence for the phishing Email but we need to know the name of malware file 

Get the file

``` wget https://hubchallenges.s3-eu-west-1.amazonaws.com/Forensics/mail_bak.7z ```

Download p7zip for archlinux using the yay aur handler

``` yay -S p7zip```

Unzip the file

``` 7z e mail_bak.7z ```

tThis generates two files ```Inbox``` and ```Sent```

Find out the type of the files

```
file Inbox Sent

Inbox: HTML document, ASCII text, with very long lines (707), with CRLF line terminators
Sent:  Non-ISO extended-ASCII text, with CRLF line terminators
``` 

since its ascii, we can just cat the two files and look for windows.exe files as these are most likely to run malicous commands

```cat Inbox Sent | grep ".exe"```

We check for links among the executables

```
cat Inbox Sent | grep ".exe" | grep href
```
 and we get the following output
```
grep: (standard input): binary file matches
href="http://ctbank.com/Mal_strike8941934890753353453.exe">ctbank.com/Mal_strike8941934890753353453.exe</a><br>
flag{href="http://www.ctbank.com/Mal_strike8941934890753353453.exe"
```
thus our file name is ```Mal_strike8941934890753353453.exe```
flag is ```flag{Mal_strike8941934890753353453.exe}```