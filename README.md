# speedtest-linux
Download and upload speeds via speedtest.net from the Linux command line, suitable for logs. 

```
_______________|  speedtest : ping, download and upload speeds.
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


  Dependencies:  speedtest-cli.py ( https://github.com/sivel/speedtest-cli )
                 curl             ( to directly get the latest version.    )


CHANGE LOG  Origin: https://github.com/rsvp/speedtest-linux
2015-03-13  This script ALWAYS retrieves the latest dependent code.
               Currently it is version 0.3.2 from the primary source.

```