# SerialModbusProbe

# Diagnostic/testing tool for serial MODBUS (MODBUS-RTU), DCON, simply serial, anything serial

### Indispensable tool in automation engineer's toolbox, when something fails to work.

(c) 2019-2020, Leonid Titov.

Diagnostic testing tool for serial Modbus. Indispensable tool in automation engineer's toolbox, when something fails to work. Useful to probe and configure IO modules. Also can be used to troubleshoot RS485 communication buses.

Tested on Linux and Windows.

Written in Go. (Source code? Ask for it).

Usage:

	./SerialModbusProbe <device> <JSON_config_file> <message> 

Message:

	"1 2 3 55 255 0xaa 0xEE numbers in any base, and text"
	-m="text 0x20 with 0x20 spaces"
	-m="any 0x20 ascii, 0x20 ABC$**SERIAL"
	-m="add MODBUS CRC to any preceding data +CRC"

Syntax notes:
- You can use numbers in any base, e.g. 12, 0x0a, etc.
- You can use +CRC to generate CRC on previous data, from the beginning.
- You can use 0x20 or 32 to explicitly add spaces (otherwise they're ignored).
- CR (carriage return) would be 0x0D or 13.

JSON example, with default values:

	{	"BaudRate":	9600,
		"DataBits":	8,
		"Parity":	"N",	// N/O/E/M/S
		"StopBits":	1	// 1/15/2
	}	// no comments allowed in JSON itself! And no trailing comma!

Example:

	./SerialModbusProbe /dev/ttyS0 s1.json "0x01 0x02 0x03 0x00 +CRC"

On Windows:

	SerialModbusProbe.exe COM3 s1.json "0x01 0x02 0x03 0x00 +CRC"

Note, this program operation requires access (possibly root?) to /dev/tty*

This can be useful (Linux):

	stty -F /dev/ttyS0 9600 cs8 -cstopb -parenb -echo raw

On Windows, you can set the COM port mode with MODE command, https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/mode

__PLUS, you can start this program with void message, and conveniently monitor
port traffic in HEX. E.g. on another port or machine.__

