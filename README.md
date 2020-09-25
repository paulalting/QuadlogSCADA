QuadlogSCADA
------------

  QuadlogSCADA is an application framework for use in small automation or control systems. 
  It allows users to develop elegant SCADA systems based on Python together with HTML5 and JavaScript 
  and other web technologies of the users choice. It is lightweight and capable of operating 
  on systems with minimal hardware resources.
  
  Once configured for the specific process application, it allows users via a secure web 
  browser connection to interact with real world process systems running on PLCs or 
  micro-controller type devices such as Arduino to view data and alter set-points.

Features
--------

 - Communicates via Modbus protocol with devices like PLCs or Arduino.
 - Provides a modern and flexible web-based user interface framework using HTML5/JavaScript.
 - Ability to monitor and log sensor data as well as alarm conditions.
 - Able to accept user input such as set-points and on/off controls.

### Simple

- QuadlogSCADA is an application framework, built upon Python 3 (3.6). 
- User configuration is largely separated from base code.
  
#### Centralised or Distributed

- QuadlogSCADA has two main components that share data through a central Redis-Server, the IOServer communicating with PLCs and the Webserver for web clients.
- This allows the two components to exist on a single system or to exist over multiple network connected systems.
  
#### Efficient

- Quadlog code makes use of asynchronous co-routines for non-blocking execution. 
- Applications can be set to operate on system boot via systemd service files.
  
#### Extensible

- Being a framework, all aspects of QuadlogSCADA are able to be extended by the user.
  
#### Compatible
- QuadlogSCADA should work on just about everything except for Microsoft Windows. 
- It is tested and supported on GNU/Linux, with future testing for Mac OS X, Solaris, and FreeBSD. The core components are written entirely in Python with the web application written with standard web language tools.
  
#### Proven

- QuadlogSCADA has successfully been deployed in situations where traditional PLC and SCADA systems have been used.


Installation
------------

This is still a preliminary project set up with only the documentation uploaded as of September 25 2020.

Installation instructions can be found at http://quadlogscada.paulalting.com



### License

QuadlogSCADA is licensed under the MIT license.

