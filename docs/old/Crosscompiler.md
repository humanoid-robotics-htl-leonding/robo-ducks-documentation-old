# RoboDuck Crosscompiler #

## Requirements ##

To run the RoboDuck Crosscompiler/Toolchain following programs are needed:

* Docker/Docker-compose
* ssh

Running the Crosscompiler on Windows will require a Unix-type shell (powershell /git bash).
To run the whole process passwordless one will need a ssh-key.

## Usage ##

The password of all components in the toolchain is 'quack'.

1. Installing/Starting the machine with startup.sh  
2. Compile code with compile.sh / add compile.sh as run-configuration in CLion.
   compile.sh expects at least a running mode (run/test/onlyrun/onlytest/recompile)
   and you can pass arguments to the call with the -a parameter.

Files/Directories that should NOT be uploaded to the machine can be put  
into .toolignore.

## Known inconveniences ##

Windows machines will run into a problem with CRLF/LF incompabilities.  
This can be resolved by converting the files manually or running the dos2unix  
command in the toolchain directory.
