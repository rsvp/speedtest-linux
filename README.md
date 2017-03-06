# speedtest-linux

Get download / upload speeds via speedtest.net or fast.com 
from the Linux command line using bash script -- suitable for logs.

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
                 speedtest-cli.py ( https://github.com/sivel/speedtest-cli )
                               ^tested on Python versions 2.4 through 3.4. 
```

## fasttest

Download speed via fast.com from the Linux command line, suitable for logs. 

```
______________|  fasttest : download speed in Mbps, optional to log results.
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
                 fast_com.py ( https://github.com/sanderjo/fast.com )

```

