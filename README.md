ntopng-docker
=============


## Install & Run

```sh
$ sudo mkdir -p /var/lib/ntopng
$ docker run --net=host -t lucaderi/ntopng-docker \
    --http-port 0.0.0.0:3000 \
    --redis REDIS_HOST:REDIS_PORT \

```

### NTOPNG Arguments

```
ntopng x86_64 v.2.3.160419 - (C) 1998-15 ntop.org

Usage:
  ntopng <configuration file path>
  or
  ntopng <command line options>

Options:
[--dns-mode|-n] <mode>              | DNS address resolution mode
                                    | 0 - Decode DNS responses and resolve
                                    |     local numeric IPs only (default)
                                    | 1 - Decode DNS responses and resolve all
                                    |     numeric IPs
                                    | 2 - Decode DNS responses and don't
                                    |     resolve numeric IPs
                                    | 3 - Don't decode DNS responses and don't
                                    |     resolve numeric IPs
[--interface|-i] <interface|pcap>   | Input interface name (numeric/symbolic),
                                    | view or pcap file path
[--data-dir|-d] <path>              | Data directory (must be writable).
                                    | Default: /var/tmp/ntopng
[--install-dir|-t] <path>           | Set the installation directory to <dir>.
                                    | Should be set when installing ntopng
                                    | under custom directories
[--daemon|-e]                       | Daemonize ntopng
[--httpdocs-dir|-1] <path>          | HTTP documents root directory.
                                    | Default: httpdocs
[--scripts-dir|-2] <path>           | Scripts directory.
                                    | Default: scripts
[--callbacks-dir|-3] <path>         | Callbacks directory.
                                    | Default: scripts/callbacks
[--no-promisc|-u]                   | Don't set the interface in promiscuous mode.
[--traffic-filtering|-k] <param>    | Filter traffic using cloud services.
                                    | (default: disabled). Available options:
                                    | httpbl:<api_key>        See README.httpbl
[--http-port|-w] <[addr:]port>      | HTTP. Set to 0 to disable http server.
                                    | Addr can be any valid ipv4 (e.g., 192.168.1.1)
                                    | or ipv6 (e.g., [3ffe:2a00:100:7031::1]) address.
                                    | Surround ipv6 addresses with square brackets.
                                    | Prepend a ':' without addr before the port
                                    | to listen on the loopback address.
                                    | Default port: 3000
                                    | Examples:
                                    | -w :3000
                                    | -w 192.168.1.1:3001
                                    | -w [3ffe:2a00:100:7031::1]:3002
[--https-port|-W] <[:]https port>   | HTTPS. See usage of -w above. Default: 3001
[--local-networks|-m] <local nets>  | Local nets list (default: 192.168.1.0/24)
                                    | (e.g. -m "192.168.0.0/24,172.16.0.0/16")
[--ndpi-protocols|-p] <file>.protos | Specify a nDPI protocol file
                                    | (eg. protos.txt)
[--disable-host-persistency|-P]     | Disable host persistency in the Redis cache
[--redis|-r] <host[:port][@db-id]>  | Redis host[:port][@database id]
[--core-affinity|-g] <cpu core ids> | Bind the capture/processing threads to
                                    | specific CPU cores (specified as a comma-
                                    | separated list)
[--user|-U] <sys user>              | Run ntopng with the specified user
                                    | instead of nobody
[--dont-change-user|-s]             | Do not change user (debug only)
[--shutdown-when-done]              | Terminate when a pcap has been read (debug only)
[--zmq-collector-mode]              | Force ZMQ sockets to operate in collector mode. If
                                    | used nprobe must use --zmq-probe-mode so that it can
                                    | behave as a probe.
--zmq-encrypt-pwd <pwd>             | Encrypt the ZMQ data using the specified password
[--disable-autologout|-q]           | Disable web interface logout for inactivity
[--disable-login|-l] <mode>         | Disable user login authentication:
                                    | 0 - Disable login only for localhost
                                    | 1 - Disable login only for all hosts
[--max-num-flows|-X] <num>          | Max number of active flows
                                    | (default: 131072)
[--max-num-hosts|-x] <num>          | Max number of active hosts
                                    | (default: 65536)
[--users-file|-u] <path>            | Users configuration file path
                                    | Default: ntopng-users.conf
[--pid|-G] <path>                   | Pid file path
[--disable-alerts|-H]               | Disable alerts generation
[--packet-filter|-B] <filter>       | Ingress packet filter (BPF filter)
[--dump-flows|-F] <mode>            | Dump expired flows. Mode:
                                    | es     Dump in ElasticSearch database
                                    |        Format:
                                    |        es;<idx type>;<idx name>;<es URL>;<http auth>
                                    |        Example:
                                    |        es;ntopng;ntopng-%Y.%m.%d;http://localhost:9200/_bulk;
                                    |        Note: the <idx name> accepts the strftime() format.
                                    | mysql  Dump in MySQL database
                                    |        Format:
                                    |        mysql;<host|socket>;<dbname>;<table name>;<user>;<pw>
                                    |        mysql;localhost;ntopng;flows;root;
[--export-flows|-I] <endpoint>      | Export flows using the specified endpoint.
[--dump-hosts|-D] <mode>            | Dump hosts policy (default: none).
                                    | Values:
                                    | all    - Dump all hosts
                                    | local  - Dump only local hosts
                                    | remote - Dump only remote hosts
[--sticky-hosts|-S] <mode>          | Don't flush hosts (default: none).
                                    | Values:
                                    | all    - Keep all hosts in memory
                                    | local  - Keep only local hosts
                                    | remote - Keep only remote hosts
                                    | none   - Flush hosts when idle
--hw-timestamp-mode <mode>          | Enable hw timestamping/stripping.
                                    | Supported TS modes are:
                                    | apcon - Timestamped packets by apcon.com
                                    |         hardware devices
                                    | ixia  - Timestamped packets by ixiacom.com
                                    |         hardware devices
                                    | vss   - Timestamped packets by vssmonitoring.com
                                    |         hardware devices
--capture-direction                 | Specify packet capture direction
                                    | 0=RX+TX (default), 1=RX only, 2=TX only
--online-license-check              | Check license online
[--enable-taps|-T]                  | Enable tap interfaces used to dump traffic
[--http-prefix|-Z] <prefix>         | HTTP prefix to be prepended to URLs. This is
                                    | useful when using ntopng behind a proxy.
[--instance-name|-N] <name>         | Assign an identifier to the ntopng instance.
[--community]                       | Start ntopng in community edition (debug only).
[--check-license]                   | Check if the license is valid.
[--check-maintenance]               | Check until maintenance is included in the license.
[--verbose|-v]                      | Verbose tracing
[--version|-V]                      | Print version and quit
[--help|-h]                         | Help
```
