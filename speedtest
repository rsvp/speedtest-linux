#!/usr/bin/env bash
#              bash 4.3.11(1)     Linux Ubuntu 14.04.1        Date : 2017-03-06
#
# _______________|  speedtest : ping, download and upload speeds.
#                               Commandline using speedtest.net resources.
#                               This standalone script is a wrapper. 
#
#           Usage:  speedtest [--log|--simple|--verbose|--list|--fav|--version]
#
#                   Takes about a minute for results to appear.
#                   For logfile, directory variable $logdir should be modified.
#
#        Examples:  $ speedtest --simple 
#                   Ping: 22.602 ms
#                   Download: 0.62 Mbit/s
#                   Upload: 0.25 Mbit/s
#                   
#                   $ speedtest   #  No args for single line timestamped.
#                   2015-03-13, 19:25, 22.602, 0.62, 0.25
#
#                   $ speedtest --log  #  Will cat logfile with latest result.
#
#                   $ speedtest --log tmp.log  #  else default: speedtest.log
#
#    Dependencies:  curl [ Used to download the following Python script: ]
#                   speedtest.py ( https://github.com/sivel/speedtest-cli )
#
#  CHANGE LOG  ORIGIN: https://github.com/rsvp/speedtest-linux 
#  2017-03-06  Upstream deprecates speedtest-cli.py in favor of speedtest.py
#  2016-01-18  Fix issue #2 by using $HOME instead of /home/${USER} for logdir.
#                 @oeolartep: $USER was unbound variable in cron jobs.
#  2015-03-19  Second argument names log file. Directory's existence tested.
#  2015-03-17  Clarify some comments.
#  2015-03-13  This script ALWAYS retrieves the latest dependent code.
#                 Currently it is version 0.3.2 from the primary source.


#           _____ PREAMBLE_v3: settings, variables, and error handling.
#
LC_ALL=POSIX
#      locale means "ASCII, US English, no special rules, 
#      output per ISO and RFC standards." 
#      Esp. use ASCII encoding for glob and sorting characters. 
shopt -s   extglob
#     ^set extended glob for pattern matching.
shopt -s   failglob
#         ^failed pattern matching signals error.
set -e
#   ^errors checked: immediate exit if a command has non-zero status. 
set -o pipefail
#   ^exit status on fail within pipe, not (default) last command.
set -u
#   ^unassigned variables shall be errors.
#    Example of default VARIABLE ASSIGNMENT:  arg1=${1:-'foo'}

arg1=${1:-'NULL'}
arg2=${2:-'speedtest.log'}
#         ^default name for logfile, see $logf below.

program=${0##*/}   #  similar to using basename
memf=$( mktemp /dev/shm/88_${program}_tmp.XXXXXXXXXX )
errf=$( mktemp /dev/shm/88_${program}_tmp.XXXXXXXXXX )


cleanup () {
     #  Delete temporary files, then optionally exit given status.
     local status=${1:-'0'}
     rm -f  $memf $errf
     [ $status = '-1' ] ||  exit $status      #  thus -1 prevents exit.
} #--------------------------------------------------------------------
warn () {
     #  Message with basename to stderr.          Usage: warn "message"
     echo -e "\n !!  ${program}: $1 "  >&2
} #--------------------------------------------------------------------
die () {
     #  Exit with status of most recent command or custom status, after
     #  cleanup and warn.      Usage: command || die "message" [status]
     local status=${2:-"$?"}
     cat $errf >&2
     cleanup -1  &&   warn "$1"  &&  exit $status
} #--------------------------------------------------------------------
trap "die 'SIG disruption: but finish needs about one minute.' 114" 1 2 3 15
#    Cleanup after INTERRUPT: 1=SIGHUP, 2=SIGINT, 3=SIGQUIT, 15=SIGTERM
trap "die 'unhandled ERR via trap, but cleanup finished.' 116" ERR
#    Cleanup after command failure unless it's part of a test clause.
#
# _______________     ::  BEGIN  Script ::::::::::::::::::::::::::::::::::::::::


favorite='1335'
#        ^DreamHost in Los Angeles for --fav option.
#        Use --list to find your favorite.

logdir="$HOME/var/log/net"
#      ^RENAME log directory for your personal use; for --log option.

[ -d "$logdir" ]  ||  mkdir -p "$logdir"  ||  die "fail creating $logdir" 117
#  Check directory's existence, else create it.

logf="$logdir/$arg2"
#     Suggested first line HEADER for CSV: Date, Time, Ping, Down, Up


#  Relying on a STATIC LOCAL VERSION may get outdated, so
#  DOWNLOAD and execute LATEST PRIMARY VERSION of speedtest-cli.py:
source='https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py'
#  If @sivel disappears for any reason, try mirror @rsvp.
#
#  Retrieve source and place it in memory with execute permission:
curl -kL --silent $source  >  $memf  \
     ||  die "curl unable to retrieve $program source code."  113
chmod 755 $memf


timestamped () {
     #  Get time, then --simple in one line, finally combine into CSV format.
     epoch="$( date '+%Y-%m-%d, %H:%M' )" 
     speeds="$( echo $( $memf --simple | sed -e 's/^.*: //' -e 's/ .*s$/, /' ))"
     #      ^on a single line: ping, download, upload speeds -- given output:
     #                   Ping: 22.602 ms
     #                   Download: 0.62 Mbit/s
     #                   Upload: 0.25 Mbit/s
     echo "$epoch, $speeds"  |  sed -e 's/,$//'
     #  Sample result:  "2015-03-13, 19:25, 22.602, 0.62, 0.25"
}


case "$arg1" in 
       NULL)  timestamped                                                     ;;
      --log)  timestamped >> "$logf"  &&  cat "$logf"                         ;;

   --simple)  $memf --simple                                                  ;;
              #     Not specifying favorite server lets the program 
              #     pick the server with lowest latency.
      --fav)  $memf --simple --server $favorite                               ;;
  --verbose)  $memf                                                           ;;
  --version)  $memf --version  ||  true                                       ;;
     --list)  $memf --list                                                    ;;
              #       list of worldwide servers.

  --default)  echo "Default log directory: $logdir "
              echo "Default log file:      $arg2 "
              echo "--fav test server:     $favorite"                         ;;

          *)  die "undefined arg: $arg1"  115                                 ;;
esac



cleanup    #  Instead of: trap arg EXIT
# _______________ EOS ::  END of Script ::::::::::::::::::::::::::::::::::::::::

#  vim: set fileencoding=utf-8 ff=unix tw=78 ai syn=sh :
