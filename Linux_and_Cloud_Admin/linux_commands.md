#Linux Commands

## Simple Stuff

### grep - search for a string

search for word "stuff" in a file called filename and returns all lines with the word "stuff"

​	`grep "stuff" filename.ext` 

search for word "stuff" in all files in the folder directory

​	`grep "stuff" -r ./folder/` 



| Option | Function                                                     |
| ------ | ------------------------------------------------------------ |
| r      | searches all files and sub folders in a directory using recursion |
| l      | used with r to return just the file names where the string exists |
| E      | grep for a regex instead of exact string                     |
| c      | count the number of occurrences of the string                |

### wget - download stuff and save it to a file

download contents from some http endpoint and saves it to a destination file

​	`wget "url.com" -o destination_file.ext`

### cURL - Also download stuff

download and view contents from some endpoint

​	`curl "url.com"`

​	`curl -X GET "url.com" -H 'User: me' - H 'content-type: application-json'` 

​	Upload a file (yes you need the `@` symbol)

​	`curl -X POST "url.com" -F key=@<path to file>`

 ### find - search for a file

search for a file within a given path

​	`find /folder -name filename`

## Cloud Stuff

### lsof - list all open files

list all the open files and see what processes or connections (internet or other) are using them

​	`lsof -i <protocol>:<port>`

### ps - list all running processes

​	`ps` - see all running processes

​	`ps | grep ruby` - see running ruby processes

### kill - stop a process

​	`kill -9 <pid>`

### systemctl - see if a service is active and ready to use

​	`systemctl <status, is-active, is-enabled, is-failed> <service>`

​	`systemctl status docker`

### ssh - use shell on other computer sending info over encrypted connections on port 22

Basic SSH that will prompt you for username password

​	`ssh username@other_computer_url_or_ip`

If you have a .pem file from the other computer use -i to specify that path

​	`ssh -i <path to .pem id file from other computer> username@other_computer`

