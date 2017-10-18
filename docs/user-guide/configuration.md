i2pd configuration
==================

i2pd can be configured via command-line arguments and config files. 
Options are the same, for example, running i2pd with argument `--port=10123` and setting
option `port = 10123` in config file will have same effect.

There are two separate config files `i2pd.conf` and `tunnels.conf`. `i2pd.conf` is main configuration file, where
you configure all options. `tunnels.conf` is I2P tunnel configuration file, where you configure I2P hidden services
and client tunnels for you needs. `tunnels.conf` options are documented [here](tunnels.md).

INI-like, syntax is the following : <key> = <value>.
Comments are "#", not ";" as you may expect. See [boost ticket](https://svn.boost.org/trac/boost/ticket/808)
All command-line parameters are allowed as keys, but note for those which contains dot (.).

For example:

i2pd.conf:

    # comment
    log = true
    ipv6 = true
    # settings for specific module
    [httpproxy]
    port = 4444
    # ^^ this will be --httproxy.port= in cmdline
    # another comment
    [sam]
    enabled = true

See also commented config with examples of all options in ``contrib/i2pd.conf``.

Options specified on the command line take precedence over those in the config file.
If you are upgrading your very old router (< 2.3.0) see also [this](config_opts_after_2.3.0.md) page.

Available options
-----------------


Run `./i2pd --help` to show builtin help message (default value of option will be shown in braces)

### General options

Option                                 | Description
-------------------------------------- | --------------------------------------
conf                                   | Config file (default: ~/.i2pd/i2pd.conf or /var/lib/i2pd/i2pd.conf). This parameter will be silently ignored if the specified config file does not exist.
tunconf                                | Tunnels config file (default: ~/.i2pd/tunnels.conf or /var/lib/i2pd/tunnels.conf)
pidfile                                | Where to write pidfile (dont write by default)
log                                    | Logs destination: stdout, file, syslog (stdout if not set, file - otherwise, for compatibility)
logfile                                | Path to logfile (default - autodetect)
loglevel                               | Log messages above this level (debug, info, warn, error)
logclftime                             | Write full CLF-formatted date and time to log (default: write only time)
datadir                                | Path to storage of i2pd data (RI, keys, peer profiles, ...)
host                                   | Router external IP for incoming connections
port                                   | Port to listen for incoming connections (default: auto)
daemon                                 | Router will go to background after start
service                                | Router will use system folders like '/var/lib/i2pd'
ifname                                 | Network interface to bind to
ifname4                                | Network interface to bind to for IPv4
ifname6                                | Network interface to bind to for IPv6
nat                                    | If true, assume we are behind NAT. true by default
ipv4                                   | Enable communication through IPv4. true by default
ipv6                                   | Enable communication through IPv6. false by default
notransit                              | Router will not accept transit tunnels, disabling transit traffic completely. false by default
floodfill                              | Router will be floodfill. false by default
bandwidth                              | Bandwidth limit: integer in KBps or letters: L (32), O (256), P (2048), X (>9000)
share                                  | Max % of bandwidth limit for transit. 0-100. 100 by default
family                                 | Name of a family, router belongs to
netid                                  | Network ID, router belongs to. Main I2P is 2.
ssu                                    | Enable SSU transport protocol (use UDP). true by default
ntcp                                   | Enable NTCP transport protocol (use TCP). true by default
ntcpproxy                              | Specify proxy server for NTCP. Should be http://address:port or socks://address:port 

### Windows-specific options

Option                                 | Description
-------------------------------------- | --------------------------------------
svcctl                                 | Windows service management (--svcctl="install" or --svcctl="remove")
insomnia                               | Prevent system from sleeping
close                                  | Action on close: minimize, exit, ask

All options below still possible in cmdline, but better write it in config file:

### HTTP webconsole

Option                                 | Description
-------------------------------------- | --------------------------------------
http.enabled                           | If webconsole is enabled. true by default  
http.address                           | The address to listen on (HTTP server)
http.port                              | The port to listen on (HTTP server) 7070 by default
http.auth                              | Enable basic HTTP auth for webconsole
http.user                              | Username for basic auth (default: i2pd)
http.pass                              | Password for basic auth (default: random, see logs)

### HTTP proxy

Option                                 | Description
-------------------------------------- | --------------------------------------
httpproxy.enabled                      | If HTTP proxy is enabled. true by default  
httpproxy.address                      | The address to listen on (HTTP Proxy)  
httpproxy.port                         | The port to listen on (HTTP Proxy) 4444 by default 
httpproxy.addresshelper                | Enable of disable address helper (jump). true by default  
httpproxy.keys                         | optional keys file for HTTP proxy local destination  
httpproxy.signaturetype                | signature type for new keys if keys file is set. 7 by default
httpproxy.inbound.length               | Inbound tunnels length if keys is set. 3 by default  
httpproxy.inbound.quantity             | Inbound tunnels quantity if keys is set. 5 by default  
httpproxy.outbound.length              | Outbound tunnels length if keys is set. 3 by default  
httpproxy.outbound.quantity            | Outbound tunnels quantity if keys is set. 5 by default    

### Socks proxy

Option                                 | Description
-------------------------------------- | --------------------------------------
socksproxy.enabled                     | If SOCKS proxy is enabled. true by default  
socksproxy.address                     | The address to listen on (SOCKS Proxy)  
socksproxy.port                        | The port to listen on (SOCKS Proxy). 4447 by default  
socksproxy.keys                        | optional keys file for SOCKS proxy local destination  
socksproxy.signaturetype               | signature type for new keys if keys file is set. 7 by default
socksproxy.inbound.length              | Inbound tunnels length if keys is set. 3 by default  
socksproxy.inbound.quantity            | Inbound tunnels quantity if keys is set. 5 by default  
socksproxy.outbound.length             | Outbound tunnels length if keys is set. 3 by default  
socksproxy.outbound.quantity           | Outbound tunnels quantity if keys is set. 5 by default  
socksproxy.outproxy                    | Address of outproxy. requests outside I2P will go there  
socksproxy.outproxyport                | Outproxy remote port  

### SAM interface

Option                                 | Description
-------------------------------------- | --------------------------------------
sam.address                            | The address to listen on (SAM bridge)
sam.port                               | Port of SAM bridge. Usually 7656. SAM is off if not specified
sam.enabled                            | If SAM is enabled. true by default 

### BOB interface

Option                                 | Description
-------------------------------------- | --------------------------------------
bob.address                            | The address to listen on (BOB command channel)
bob.port                               | Port of BOB command channel. Usually 2827. BOB is off if not specified
bob.enabled                            | If BOB is enabled. false by default 

### I2CP interface

Option                                 | Description
-------------------------------------- | --------------------------------------
i2cp.address                           | The address to listen on or an abstract address for Android LocalSocket
i2cp.port                              | Port of I2CP server. Usually 7654. Ignored for Andorid
i2cp.enabled                           | If I2CP is enabled. false by default. Other services don't require I2CP 

### I2PControl interface

Option                                 | Description
-------------------------------------- | --------------------------------------
i2pcontrol.address                     | The address to listen on (I2P control service)  
i2pcontrol.port                        | Port of I2P control service. Usually 7650. I2PControl is off if not specified  
i2pcontrol.enabled                     | If I2P control is enabled. false by default  
i2pcontrol.password                    | I2P control authentication password. itoopie by default  
i2pcontrol.cert                        | I2P control HTTPS certificate file name. i2pcontrol.crt.pem by default  
i2pcontrol.key                         | I2P control HTTPS certificate key file name. i2pcontrol.key.pem by default  

### UPNP

Option                                 | Description
-------------------------------------- | --------------------------------------
upnp.enabled                           | Enable or disable UPnP, false by default for CLI and true for GUI (Windows, Android)  
upnp.name                              | Name i2pd appears in UPnP forwardings list. I2Pd by default  

### Cryptography

Option                                 | Description
-------------------------------------- | --------------------------------------
precomputation.elgamal                 | Use ElGamal precomputated tables. false for x64 and true for other platforms by default  

### Reseeding

Option                                 | Description
-------------------------------------- | --------------------------------------
reseed.verify                          | Verify .su3 signature. fase by default 
reseed.urls                            | Reseed URLs, separated by comma
reseed.file                            | Path to local .su3 file or HTTPS URL to reseed from
reseed.zipfile                         | Path to local .zip file to reseed from
reseed.threshold                       | Minimum number of known routers before requesting reseed. 25 by default

### Addressbook options

Option                                 | Description
-------------------------------------- | --------------------------------------
addressbook.defaulturl                 | AddressBook subscription URL for initial setup
addressbook.subscriptions              | AddressBook subscriptions URLs, separated by comma

### Limits

Option                                 | Description
-------------------------------------- | --------------------------------------
limits.transittunnels                  | Override maximum number of transit tunnels. 2500 by default   
limits.openfiles                       | Limit number of open file descriptors (0 - use system limit)  
limits.coresize                        | Maximum size of corefile in Kb (0 - use system limit)  

### Trust options

Option                                 | Description
-------------------------------------- | --------------------------------------
trust.enabled                          | Enable explicit trust options. false by default
trust.family                           | Make direct I2P connections only to routers in specified Family.
trust.routers                          | Make direct I2P connections only to routers specified here. Comma separated list of base64 identities.
trust.hidden                           | Should we hide our router from other routers? false by default

### Websocket server

Option                                 | Description
-------------------------------------- | --------------------------------------
websockets.enabled                     | Enable websocket server. Disabled by default
websockets.address                     | Address to bind websocket server on. 127.0.0.1 by default
websockets.port                        | Port to bind websocket server on. 7666 by default

### Exploratory tunnels

Option                                 | Description
-------------------------------------- | --------------------------------------
exploratory.inbound.length             | Exploratory inbound tunnels length. 2 by default
exploratory.inbound.quantity           | Exploratory inbound tunnels quantity. 3 by default
exploratory.outbound.length            | Exploratory outbound tunnels length. 2 by default
exploratory.outbound.quantity          | Exploratory outbound tunnels length. 3 by default

Local addressbook
-----------------

There is also a special addressbook config file in working directory `addressbook/local.csv`.
It is used to map long I2P destinations to short, human readable domain names. The syntax is csv.

