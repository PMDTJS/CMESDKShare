CMESDK Readme.txt
============================================================

This readme file contains information pertaining to the
Performance Motion Devices C-Motion Engine Software Development Kit (PMD CME SDK).

The optional editor, Programmer's Notepad, can be installed.
The installer can be found at 
http://www.pnotepad.org/download/
or 
\CMECode\utils\ProgrammersNotepadInstaller.exe
This editor can be used for the CMECode examples.
PMD provides a file that adds build tools to the "Tools" menu in Programmer's Notepad.
Copy the 
\CMECode\utils\UserTools.xml 
file to
%appdata%\Echo Software\PN2\


The HostCode examples use Microsoft Visual Studio 
Microsoft Visual Studio can also be used for the CMECode examples.
However, building the CMECode examples is accomplished with the build.bat file.

Most of the examples have the option to use several different
communication interfaces.  Each example contains the necessary interface 
connection functions appropriate for the particular product 
(ie. PMDPeriphOpenTCP).  It will be necessary to uncomment the desired one.

Many of the interface options may require more editing for
configuration, for example to select IP addresses, CANBus node
identifiers, serial communications ports, and so forth.  Comments in
the individual source files indicate which settings are likely to need
editing.

Preprocessor directives may be used to select specific modes of operation
such as: 

#define CME
Some of the provided examples can run on both the CME device and a Windows
PC, while others will only run on one or the other, but not both.  Whether or
not an example is being compiled to run on a CME device or Windows PC will 
affect what commands are supported.  Once again, a preprocessor directive is
used to assist with the compilation.  When "#define CME" is true, the example
will compile for use on a CME device using build.bat.  Otherwise if "CME" is not defined then the
example will compile for use on a Windows PC (this would be the typical case
when Visual Studio is in use).  Note that "CME" is a directive defined in the
Makefile used to compile all CME code.


Some examples will have a mating example. For instance if 
HostCode\Examples\GenericUserPacket.c is to be run on a Windows PC,  
the corresponding CMECode\Examples\GenericUserPacket.c should
be running on the CME device.  


Example set as of Dec 1, 2020:

CME Examples:
CMECode\Examples\Hello
CMECode\Examples\nIONCME
CMECode\Examples\GenericUserPacket
CMECode\Examples\Multitask

Host Examples (Windows PC):
CMECode\Examples\nIONCME
HostCode\Examples\GenericUserPacket

The nIONCME example shares one source file that can be compiled to run on a CME device or a Windows PC.


Hello.c
===============
This example runs on the CME device only.  It will print out a debug “Hello” message
to the Console window.  It will then query the ActualPosition of Axis1 of the on board 
Magellan controller and will send the ActualPosition value over to the debug console
if the position changes.  It will also blink the green LED on the N-Series ION/CME.


nIONCME.c
================
This example can be run on the device or from a PC host. After the
interface is established it will call several functions that demonstrate
features of the device.

The SetupAxis1() function sets all the parameters of the processor based on the 
ProMotionExport.c file exported from Pro-Motion. (select File/Export as C-Motion).

The AllMagellanCommands() function send all supported commands through the interface.
This example is really only meant to be used as a command reference. 

The ProfileMove() will attempt to perform a trapezoidal profile move. 
The function will return when the profile completes or a timeout occurs.

The IOExample() function reads/writes the IO signals of the device's IO connector.


GenericUserPacket.c
====================
This example contains two distinct pieces of source code.  One that runs on the
CME device card (found in the CMECode/Examples folder) and another that runs on
a Windows PC (found in HostCode/Examples). 

On the CME device side this example will open a port and query that port in a loop to
check for received data.  If data if received it will send the data back out the peripheral.

On the Windows PC side this example will open a port and send a few bytes of data, it will
then wait to receive data.


