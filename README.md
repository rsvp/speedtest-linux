# speedtest-linux

From the command line get ping/download/upload stats:

- from https://speedtest.net or https://fast.com
- *without* their ads
- *without* their web GUI interface
- simply **timestamped** in one-line CSV format
- suitable for logs
- using **Bash** shell script
- for all POSIX systems


```
______________|  speedtest : ping, download and upload speeds.
                             Commandline using speedtest.net resources.
                             This standalone script is a wrapper. 
                                        
         Usage:  speedtest [--log|--simple|--verbose|--list|--fav|--version]

                 Takes about a minute for results to appear.
                 For logfile, the variable $logf can be modified.

      Examples:  $ speedtest --simple 
                 Ping: 22.602 ms
                 Download: 0.62 Mbit/s
                 Upload: 0.25 Mbit/s
                 
                 $ speedtest   #  No args for single line timestamped.
                 2015-03-13, 19:25, 22.602, 0.62, 0.25

                 $ speedtest --log  #  Will cat logfile with latest result.

  Dependencies:  curl (Used to download the following Python script:)
                 speedtest.py (https://github.com/sivel/speedtest-cli)
```


## fasttest

Get just the download speed via fast.com from the command line,
suitable for logs. The infrastructure is provided by Netflix
to make sure ISPs are not throttling their streaming movies.


```
______________|  fasttest : download speed in Mbps, flag to log results. 
                            Uses Netflix's fast.com resources,
                            checking via both IPv4 and IPv6.
                            This standalone script is a wrapper. 

         Usage:  fasttest [--log|--verbose]

                 Takes about a minute for results to appear.
                 For logfile, directory variable $logdir should be modified.

      Examples:  $ fasttest   #  No args for single line timestamped.
                 2017-03-06, 19:25, 22.602

                 $ fasttest --log  #  Will cat logfile with latest result.

                 $ fasttest --log tmp.log  #  else default: fasttest.log

  Dependencies:  curl (Used to download the following Python script:)
                 fast_com.py (https://github.com/sanderjo/fast.com)
```


Many thanks to the developers upstream: @sivel and @sanderjo -- 
we rely on their latest updates to the Python source code.

