# Session-4 Notes

###  Working with Shell - 2



### View file size

```
du -sk file.txt   ###  prints size in Kb

du -sh file.txt ### prints size in MB

ls -lh file.txt ### prints size with more details like permissions of file , last updated time of file , along with filename

```

### File compression and Archival

Since we have seen file size , lets check on how to compress file and extract the compressed file

```
tar -cvf file.tar file1 file2 file3  # -c stands for creating tar file and -f refers to tar file name , -v verbose mode, ie; to show files being archived

tar -czvf archive.tar.gz files...   # compress an archive with zip , -z stand for Compress the archive with gzip.

```

```
tar -xzvf archive.tar.gz   # Extract a Compressed Archive

tar -xvf archive.tar # extract a compressed tar file

```

### Searching for Files and Patterns

```
find /path/to/search -name "filename"  

locate file.txt 

# disadvantage is that it gets details/data from database called "mlocate.db" for querying the file. you may sometimes not be able to find the frecently saved file as it might not have updated in db.

ls -l | grep 'filename-2.txt'

ls -R | grep 'filename-3.txt'  

# ls -R recursively lists the contents of directories and subdirectories, while ls -l lists files and directories in a detailed, long-form format

# if we go one step ahead of just searching files in Linux , we can check for empty files and delete them as below

find /path/to/search  -empty -type d -delete  # delete empty directories in that path

find /path/to/search  -empty -type f -delete  # delete empty files  in that path 


```


### IO Redirection


# 3 standard streams of linux 

-Standard Input :- accepts text as input 
-Standard Output :- text output from any command is referred to as standard output
-Standard Error :- any error message for our command is referred to as standard error

To redirect standard output to a file instead of printing on screen 

```
echo 'Hi' > file.txt

echo 'Team , Welcome!!' >> file.txt  # it just appends this content to alreday existing content in file 
```

To redirect  just error messages ie; standard error to file instead of printing on screen, use  2 and then redirect to file


```
ls -l | grep 'file3.txt' 2 > error.txt

ls -l | grep 'file3.txt' 2 >> error.txt 

```

 since we have seen redirecting output / errrors to  some file , lets also check a convenient way to discard unwanted output and is commonly used in shell scripting

 By redirecting output to /dev/null, you can effectively silence commands that produce output you don't want to see. For example, when running a command in a script and you're not interested in its output, you can redirect it to /dev/null to avoid cluttering the terminal or log files.

 It ensures that the data is effectively destroyed and not written to disk.

```
command > /dev/null # Redirecting standard output to /dev/null
command 2> /dev/null  # Redirecting standard error to /dev/null
command &> /dev/null # Redirecting both standard output and standard error to /dev/null

```


### VI editor

Vi is a powerful  text editor available on most Unix-like operating systems, including Linux. It's highly customizable and efficient for editing text files, configuration files, scripts, and more. we can open any file as below

```
vi /home/user1/filename.txt  

```

when editor opens any file , initially it goes to command mode , in this mode editor only understand commands like copy , paste , delete 

In Insert mode , we edit file , add more text , remove text . we can enter into insert mode by esc + i

in last line mode , we can save file (esc + :wq ) , discard changes (esc + :q! ), exit vi editor (esc + :q)





### Cronjob

Cron is a time-based job scheduler in Unix-like operating systems, including Linux. It allows users to schedule tasks (known as cron jobs) to run periodically at fixed intervals, specific times, or dates.

```
* * * * * command_to_execute
0 1 * * * /bin/bash /path/to/script.sh

```
The five asterisks represent the timing fields: minute, hour, day of the month, month, and day of the week in that order. we can list out all crontabs on the server using crontab -l and can edit any  using crontab -e 
