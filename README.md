# QuadlogSCADA
SCADA system for GNU/Linux with Modbus communications and with inbuilt HTTP server

### This document is very much in draft form and will be updated as progress on QuadlogSACAD is made: 15 Feb 2015

## Overview:
QuadlogSCADA is in many respects a functional SCADA system in that it performs Supervisory Control function for processes as well as Data Acquisition from process equipment.

QuadlogSCADA is an application program written in the C language to be compiled into an executable designed to operate on GNU/Linux operating systems.

QuadlogSCADA communicates to connected IO modules using a standard industrial communication protocol via Ethernet TCP, RS-485 or USB, and maintains a regular scan of data from defined IO modules.

An inbuilt HTTP server allows a remote computer using standard web browsing software to view the data for displaying real-time data, alter setpoints, view history charts as well as and alarm conditions.

QuadlogSCADA is aimed initially for renewable energy systems, building automation and for small process automation.
It is suited for non critical and non life threatening control. It is not designed for or to be used in critical or safety systems. Such systems must be designed to use dedicated safety control equipment such as accredited PLC's.

## Feature Points:
* makes use of well proven libraries for the HTTP server as well as Modbus protocol support
* offers an API to handle specific HTTP requests such as user authentication and AJAX calls
* scans connected Modbus devices and reads and writes configured tags
* scans tags for alarm conditions
* scans tags to maintain basic stats
* scans tags to maintain history log for charting
* SQLite3 used to store all configuration data as well as logged data
* operates in a terminal screen as text mode using Ncurses library
* communications with devices operate in their own process thread(s)
* built in memory based IO device for HTTP access to other data, such as totalisers or counters

## Todo List:
* add in framework for user process tasks
* add in alarm action logic
* add in email handler
* add in more statisical options

