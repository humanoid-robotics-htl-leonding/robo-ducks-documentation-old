# Documentation

## Notes

* Hardlinks (ln) actually work on Windows.
* When using Docker Toolbox, you have to link your working directory to your VirtualBox as a shared folder with a matching name (e.g. D:\Documents\Work\Directory to d/Documents/Work/Directory).
* When using Docker Toolbox, you also have to forward a port (e.g. 2375).

## Scripts

### linkBuild

Whenever something is build, the current build_mode of a target ({target}/{build_mode}) is linked to {target}/current.

### shutdown

Shuts down (default) or reboots all NAOs using a list of their numbers, names or IPs.

### connect

Opens an ssh connection to a nao using the generated ssh key. Uses the naonet.sh file which will be modified by us.

### compile

Cds into the {target}/{build_type} directory and executes make (can also be changed to cmake --build)

### setup

Cleans all {target}/{build_type} folders and executes cmake in them.

### pregame

Compiles for build_type RELEASE and uploads the files to all NAOs in a given network (default ethernet). Is also terminates all hulk processes, sets the network, restarts naoqi and starts the hulk process again.

### postgame

Terminates all hulk processes and sets the network.

### gammaray

Sets up the NAO with all important HULK features. It can install everything or only the sysroot and remove all other sysroots from the NAO.