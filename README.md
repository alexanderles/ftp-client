# FTP Client

## Description (From Assignment)
This project implements an FTP client which supports the following commands:

- `ls <URL>` Prints out the directory listing from the FTP server at the given URL
- `mkdir <URL>` Creates a new directory on the FTP server at the given URL 
- `rm <URL>` Deletes the file on the FTP server at the given URL
- `rmdir <URL>` Delete the directory on the FTP server at the given URL
- `cp <ARG1> <ARG2>` Copy the file given by ARG1 to the file given by
                          ARG2. If ARG1 is a local file, then ARG2 must be a URL, and vice-versa.
- `mv <ARG1> <ARG2>`         Move the file given by ARG1 to the file given by
                          ARG2. If ARG1 is a local file, then ARG2 must be a URL, and vice-versa.

### URL Format and Defaults

Remote files and directories should be specified in the following URL format:

`ftp://[USER[:PASSWORD]@]HOST[:PORT]/PATH`

Where USER and PASSWORD are the username and password to access the FTP server,
HOST is the domain name or IP address of the FTP server, PORT is the remote port
for the FTP server, and PATH is the path to a file or directory.

HOST and PATH are the minimum required fields in the URL, all other fields are optional.
The default USER is 'anonymous' with no PASSWORD. The default PORT is 21.

## Approach
I implemented this client by first using the Python argparse library to support the
necessary program arguments. After parsing arguments I established connection to the 
server via the control channel and added support for sending commands and receiving 
responses. I then divided the main method into cases based on the operation being used.
Note that this program uses chained `if/elif` statements because `match` is not supported
by the submission server. I implemented general functionalities such as receiving data 
as bytes and opening data channels as needed while creating functionality for
the operations.

## Challenges
One challenging aspect of this project was opening and correctly using data channels. 
It was particularly challenging to support file download because it required determining
when the data channel was done sending the file bytes, which was different from receiving
messages from the control channel (which always end in `\r\n`). 

## Testing
I tested my code by creating files locally, and performing the various operations on
files and directories using the FTP client. This included creating and removing directories,
copying files to the server, deleting files, and copying files back to my local environment. 
I used print statements and the list command to ensure proper communication between the client
and server throughout the program execution.
