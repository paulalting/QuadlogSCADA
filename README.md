# Welcome to: QuadlogSCADA
SCADA system for GNU/Linux with Modbus communications and with inbuilt HTTP server

**What is it:**

QuadlogSCADA system is in many respects a functional SCADA system in the true sense of what a SCADA does. It performs Supervisory Control function for processes as well as Data Acquisition from process equipment.

QuadlogSCADA is an application program written in the C language to be compiled into an executable designed to operate on the GNU/Linux operating systems.

QuadlogSCADA communicates to connected IO modules using a standard industrial communication protocol via Ethernet TCP, RS-485 or USB, and maintains a regular scan of data from defined IO modules.

An inbuilt HTTP server allows a remote computer using standard web browsing software to view the data for displaying real-time data, history charts as well as and alarm conditions.

QuadlogSCADA is aimed for small process control environments, typically used on industrial sites, but is equally at home with building automation and energy renewable systems.

The scope of a QuadlogSCADA system is for small to medium automation or process control systems, being particularly more suited for non critical and non life threatening tasks. It is not designed to replace critical or safety systems. Such systems must be designed to use dedicated safety control equipment such as accredited PLC's.

**Features overview:**
* makes use of well proven libraries for the HTTP server as well as Modbus protocol support
* offers an API to handle specific HTTP requests such as user authentication and AJAX calls
* scans connected Modbus devices and reads and writes configured tags
* scans tags for alarm conditions
* scans tags to maintain basic stats
* scans tags to maintain history log for charting
* SQLite3 used to store all configuration data as well as logged data
* operates in a terminal screen as text mode using Ncurses library
