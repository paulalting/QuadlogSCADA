# QuadlogSCADA
## Overview
QuadlogSCADA is a software application framework for use in small automation control systems, as a useful component of a larger system for controlling a process.

Generally with automation control systems, a PLC (Programmable Logic Controller) system would be used as the main hardware device that connects to electrical equipment required to be controlled or monitored. Electrical equipment may be motors, actuators, lights or relays as outputs from the PLC and also PLC inputs such as switch inputs, temperatures, pressures, voltages or currents as analogue inputs. PLCs will have specifically designed program for the task required, typically, where it will monitor equipment inputs as well as user input to then control equipment according to the stored PLC program.


PLCs are designed to be rugged and withstand the more extreme environments of industrial situations, where there may be high levels of electrical noise, thermal stress or other environmental contaminants. Essentially, a PLC is a small computer that has been programmed for a specific task, which requires little or no attention for many years or operation.

To be able to know what is going on in a PLC system at any given moment, we could connect to the PLC system a typical computer system via a communications channel based on a standard protocol, such as Modbus for example. Being connected to the PLC system can then provide a means to remotely have control of the process from the computer system that may provide visual displays representing the control process or status held within the PLC.

The computer system must therefore have an application that can communicate with the PLC system to facilitate this. The computer system may be physically located close by or far away from the PLC which is generally located in an electrical switchboard where equipment is electrically terminated. The communications between the PLC and computer system is often over a hard-wire cable and is typically one of a few standards, such as Ethernet or optical fibre or asynchronous serial like RS-232 or TIA-485.

As mentioned, the computer system must have appropriate software installed which itself must be configured for the specified process and also for communications to function to connected PLC equipment. This is the aim of QuadlogSCADA.

QuadlogSCADA is a comparatively small and simple SCADA framework system, with SCADA being Supervisory Control And Data Acquisition. It operates on a GNU/Linux based systems, though untested, may also work on other operating systems successfully. One of its aims is to facilitate easy and cost effective entry into the arena of SCADA systems, especially for small and low-critical risk process systems where the cost of traditional SCADA software suits may be cost prohibitive. The QuadlogSCADA framework is extendable to suit the needs of such process applications.

Being a framework, it requires programmatic configuration for for it to function. This aspect of configuration is detailed in a separate document where the various components are described in greater detail using examples.

QuadlogSCADA is primarily made up of two stand-alone applications, namely the IOServer and Webserver. Both applications operate independently of each other, but communicate with each other via a central data-store, Redis. Redis is a fast and efficient non SQL data storage system. The Redis data-store is used for storing of live process data as well as logging of alarms and historical data which can then be accessed and used for further analysis.

**IOserver:**  
The IOserver communicates with PLC equipment via the Modbus RTU/TCP protocol, where data is both retrieved or sent to connected PLC devices on a cyclic time poll period. Data is held internally in the IOserver according to configured mappings as data tags and is scaled to engineering terms as well as checked for alarm conditions. Data tags can also be configured to have their data logged for long term historical analyses, by storing to Redis. The IOserver also checks for user set-points and accepts this data from the Redis data store to be sent to specific PLC devices. The IOserver can be configured to communicate with multiple PLCs via the Modbus protocol.  
Application specific configuration of the IOserver is described in the configuration document under section IOserver.

**Webserver:**  
The Webserver is exactly that, a lightweight and fast web server with some simple configuration required for the particular end process application. The web server allows a user to connect via a standard web browser, where the user is required to log in to gain further access. Once a user has successfully logged in to the web server, they will then have access to the SCADA system, where they can view and alter process data via configured HTML web based screens.  
Application specific configuration of the Webserver is described in the configuration document under section Webserver.

## Steps to install QuadlogSCADA components

### Installation Objectives:
The following installation steps describe a complete fresh system install, beginning with the operating system.  
You may choose to bypass the initial steps if you already have a system already setup appropriately.

Software to be installed

- Operating system
- Redis Server
- Redis Time Series Module
- Poetry (Python Package Management Tool)


### Prerequisites:
- **Hardware:** stand alone computer system, x64 or ARM (maybe even a humble Raspberry Pie).

### Operating System:
QuadlogSCADA is tested to operate on a Debian GNU/Linux based system. It is possible to have a single computer setup as the SCADA server while it also acts as a display client. For this setup, the computer needs a display and keyboard/mouse, a fairly typical computer hardware. For setups where the SCADA system is stand alone or headless mode, then there is no need for the display and keyboard/mouse. The following install steps are based on the former, where the computer is SCADA server as well as a display client, so an install with desktop environment.

Download and install latest stable Debian GNU/Linux headless or with desktop environment as appropriate.

During the installation process, set up the main user account with username `quadlog`. This will be the main administrative account and where the installation of various software components will take place.

Once the operating system is installed, login using the quadlog account. If isolation is required between the operator user and the SCADA system, then separate system accounts may be created in the standard method. If required, these additional user accounts can be given any suitable name as it is simply there to allow a user to log in and have access to a web browser for the SCADA displays. If not required, then it can all be done from the main quadlog account.

Since the quadlog account can have administrative root privileges, there are some initial system settings to set if required, which can assist with automatic start up of the SCADA server.