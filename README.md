#QuadlogSCADA
SCADA system with inbuilt HTTP web server and Modbus protocol communications.

##Overview:
QuadlogSCADA is in many respects a functional SCADA system in that, when properly configured, is able to perform Supervisory Control function for processes as well as Data Acquisition from connected process equipment.

QuadlogSCADA is a personal project started in early 2014, with active ongoing development.
Over time, numerous new features are hoped to be implemented that might offer greater appeal and opportunities for users.

The application is written in C and readily able to be compiled into a runtime executable for operation on GNU/Linux and OSX operating systems.
Systems can be based on Intel 32/64 bit or ARM CPUs, with the ARM platform appearing ideal for small and low power consumption applications such as found in solar installations and sensor data monitoring and logging at remote sites.

QuadlogSCADA communicates to connected devices using the standard industrial Modbus communication protocol, with connections made via Ethernet TCP mode or by RTU mode, allowing for many forms of asynchronous serial communications such as RS-232, EIA-485, async TTL and USB. Multiple devices can be connected using any combination of communications ports.

An inbuilt HTTP server allows a remote computer to view devices for displaying real-time data, alter setpoints, view history charts as well as and alarm conditions.
The user interface may be built in any language supporting HTTP protocol, but typically a standard javascript web application would be used.
The style and complexity of the user interface GUI can be as simple or complex as required by the application.
For a simple interface, it might just be a matter of a HTML page with some embedded css and javascript to present the required data.
Alternatively, for complex systems, a full web application using full javascript with framework and helper libraries can be used to present 
clever and effective real-time data visualisation screens.

This aspect of user GUI is left up to the user to create and develop in the way best suited for the needs of the application.
QuadlogSCADA provides the centralised hub for connection to devices and gathering and making the data available to the user GUI.

It should be pointed out here, that QuadlogSCADA does not rely on what many traditional server technologies use, being the LAMP/WAMP component stack.  
No use is made of Apaché or PHP or MySQL. These components are fine for typical web pages, where speed and resources are not a consideration.
Take for example, a user with a small RPi system, wanting to develop a home automation system. By the time the resource hungry Apaché, MySQL and PHP are installed, the poor RPi has very little else in terms of memory resource to be effective at its main task. Further, traditional systems using Apaché, MySQL and PHP are not at all well suited for as close to real-time data processing as needed by SCADA systems demand. Add to that, the connectivity to external devices is difficult and tricky, with data flow from device through to to user a convoluted and twisted path.

Instead, Quadlog is a tightly integrated application that effectively and efficiently processes and handles data from device through short term or long term storage through to user interface GUI. The application initiates and maintains communications with all configured and connected I/O devices to either get or set their data. The data received is checked for alarm conditions and may also be logged to long term storage in a SQLite database. The inbuilt HTTP server is started and run as a daemon, passing HTTP requests back into the main application for direct processing and response.

Being a highly integrated application, QuadlogSCADA is lightweight in terms of system memory and other resources as well as being highly responsive in terms of actual data processing.

QuadlogSCADA is aimed initially for connecting into and monitoring renewable energy systems, small building automation and for small process automation.
It is suited for non critical and non life threatening control. It is not designed for or to be used in critical or safety systems.
Such systems must be designed to use dedicated safety control equipment such as accredited PLC's.

##Feature Points:
QuadlogSCADA

* application can be compiled and run on Intel 32/64 as well as ARM based systems.
* uses well proven libraries for HTTP server, database storage as well as Modbus protocol support.
* offers an API to handle specific HTTP requests such as user authentication and AJAX calls.
* scans connected Modbus devices and reads and writes configured tags.
* scans device tags for alarm conditions.
* scans device tags to maintain basic statistics.
* scans device tags to maintain history log for charting.
* SQLite3 used to store all configuration data as well as logged data.
* operates in a terminal screen with simple text mode GUI to display system status.
* communications with devices operate in their own process threads.
* built in memory based IO device for HTTP access to other data, such as totalisers and counters.

##Todo List:
* add in framework for user process tasks
* review and expand general logging of system runntime
* add in email handler
* add in alarm action logic for email handler
* review adding more statistical options
* review and expand HTTP API for object based requests


##Installation:
Installation of QuadlogSCADA in not a trivial task, and requires installing a number of additional components to prepare a system.  
It will be assumed that the user will have an appropriate level of skill with Unix/Linux operating systems to perform the following installation tasks.  
The following is a typical setup for on a Debian based GNU/Linux system, other GNU/Linux systems as well as OSX will be similar.

The first prerequisite is that you already have a system that is setup with a working C compiler and toolchain, such as GNU GCC.

Next, ensure your system has the necessary tools to build the required libraries needed by QuadlogSCADA.  
The tools required are 'build essentials', 'automake' and 'libtool'.

Install build essential tools:  
`$ sudo apt-get install build-essential`  

Next, install automake and libtool:  
`$ sudo apt-get install automake`  
`$ sudo apt-get install libtool`

Next install the first of the helper libraries, ncurses development files:

Ncurses is a toolkit for developing "GUI-like" application software that runs under a terminal emulator and is installed as part of the Debian distribution.  
To use it in QuadlogSCADA, you also need the header files which is supplied by the libncurses5-dev package.

To install:  
`$ sudo apt-get install libncurses5-dev`

Next the three main libraries used by QuadlogSCADA need to be installed.  
Progress through the following steps to download, configure and install.
On completion, check the following libraries are available in the following directories;  
`/usr/include`  
`/usr/local/include`  

First, create a directory to store downloaded library tar files.
For example:
`mkdir Downloads`
`cd Downloads`

####Modbus:
Tested Version: 3.1.2  
Download site:<http://libmodbus.org/>  
GitHub site: <https://github.com/stephane/libmodbus>  

Then:  
`wget http://libmodbus.org/releases/libmodbus-3.1.2.tar.gz`
`$ tar -xf libmodbus-3.1.2.tar.gz`

Go into the new directory libmodbus-3.1.2 and  
`$ ./configure`

On the chance there is no configure script then generate one by running:  
`$ ./autogen.sh.`

If the autogen.sh file is not set as executable, then tell it by:  
`$ sh ./autogen.sh`

This should complete with a message saying you can now run `./configure`

Execute  
`$ ./configure`

This should result in a message tail similar to:

        libmodbus 3.1.1
        ===============
        prefix:                 /usr/local
        sysconfdir:             ${prefix}/etc
        libdir:                 ${exec_prefix}/lib
        includedir:             ${prefix}/include
        compiler:               gcc -std=gnu99
        cflags:                 -g -O2
        ldflags:                

To make:  
`$ make`

To make and install:  
`$ sudo make install`  

####libmicrohttpd:
Tested version: 0.9.49  
Download site: <https://www.gnu.org/software/libmicrohttpd/>  

Then  
`wget http://ftp.gnu.org/gnu/libmicrohttpd/libmicrohttpd-0.9.49.tar.gz`
`$ tar -xf libmicrohttpd-0.9.49.tar.gz`

Go into the new directory libmicrohttpd-0.9.49 and  
`$ ./configure`

This should result in a message similar to:

        configure:          Configuration Summary:
        Operating System:  linux-gnueabihf
        libgcrypt:         no, HTTPS will not be built
        libcurl (testing): no, many unit tests will not run
        Target directory:  /usr/local
        Messages:          yes
        Basic auth.:       yes
        Digest auth.:      yes
        Postproc:          yes
        HTTPS support:     no (lacking libgcrypt or libgnutls)
        epoll support:     yes
        libmicrospdy:      no
        spdylay (testing): no
        configure:
        License:           LGPL or eCos

Then to make:  
`$ make`

To install:  
`$ sudo make install`

####SQLite3:
Tested version: 3.12.2  
SQLite site for more info SQLite database engine: <https://www.sqlite.org>  
Set location to $HOME/dev/libraries

Get the file:  
`$ wget https://www.sqlite.org/2016/sqlite-autoconf-3120200.tar.gz`

To unpack:  
`$ tar -xf sqlite-autoconf-3120200.tar.gz`

To build and install as a system shared library:  
`$ cd sqlite-autoconf-3120200`  
`$ ./configure`  
`$ sudo make install`

To install as a source for inclusion into a project:

First install unzip if not already installed:  
`$ sudo apt-get install unzip`

Get the file from:  
`$ wget http://www.sqlite.org/2015/sqlite-amalgamation-3080803.zip`

To unzip:  
`$ unzip sqlite-amalgamation-3080803.zip -d sqlite-3.8.8.3`

This will provide files needed for inclusion into the source code for QuadlogSCADA.
Contents of $HOME/dev/libraries/sqlite-amalgamation-3080803/ will be the following:

>	shell.c  
>	sqlite3.c  
>	sqlite3ext.h  
>	sqlite3.h  


##Compile QuadlogSCADA:
To compile the source code of QuadlogSCADA, ensure all source files exist and are the latest.
All source files reside in the parent directory HOME/dev/quadlog.

Go into this directory to compile.  
`$ make clean`  
`$ make`  


###Fin du document pour installation de QuadlogSCADA
