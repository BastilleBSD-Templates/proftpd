# proftpd
Bastille Template to create a ProFTP Server Jail

 STATUS:  Testing


Once the jail is running we need to adjust the configuration slightly to our needs. The 
configuration file for Proftp is located here /usr/local/etc/proftpd.conf

Change the Server Name. 

Please note this will have no effect if you are using “ServerIdent Off” So find this line.

	ServerName                      "ProFTPD Default Installation"

And change it to something fancy like the example below.

	ServerName                      "FTP Server"

Next we want to chroot users to their home directory. Find this line.

	#DefaultRoot ~

And remove the # so it looks like this.

	DefaultRoot ~

If you are not going to use IPV6 turn IPV6 support off by finding this line.

	UseIPv6                         on
And change it to.

	UseIPv6                         off

Optional Hide Identity Start
In order to hide your FTP servers identity find this line.

	ServerName                      "ProFTPD Default Installation"
And “above” that line insert the following.

	# Hide server identity
	ServerIdent off

So it looks something like this when done.

	# Hide server identity
	ServerIdent off
	ServerName                      "ProFTPD Default Installation"
	Optional Hide Identity Stop

	Optional Set Passive Ports Range Start

If your firewall requires a passive port range you need to find this line.

	Port                            21

And below that insert the following “replace 00000 and 99999” with the passive port numbers.

	PassivePorts 00000 99999

So it would end up looking something like this.

	Port                            21
	PassivePorts 30000 30200
	Optional Set Passive Ports Range Stop

Restart proftpd with the following:
	service proftpd restart



A  Simple Stripped Down ProFTPD Config File

	ServerIdent             off
	ServerName              "Ftp Server"
	ServerType              standalone
	DefaultServer           on
	ScoreboardFile          /var/run/proftpd/proftpd.scoreboard
	Port                    21
	# PassivePorts          00000 99999
	UseIPv6                 off
	Umask                   022
	MaxInstances            30
	CommandBufferSize       512
	User                    nobody
	Group                   nogroup
	DefaultRoot ~
	AllowOverwrite          on
	# Bar use of SITE CHMOD by default
	<limit site_chmod="">
	DenyAll
	</limit>
	
And we are done here.
