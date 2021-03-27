## Disclaimer ##

Any actions and or activities related to the code provided is solely your responsibility.The misuse of the information in this website can result in criminal charges brought against the persons in question. The authors will not be held responsible in the event any criminal charges be brought against any individuals misusing the information in this tool to break the law.
## For install  ##
sudo ./configure && sudo make && sudo make install
slowhttptest 
## for usage ##
slowhttptest -H -u https://loadbal.sni.example.com

attention format like this 

slowhttptest -H -u http://www.xxxv.com -r 200 -l 99999 -c 65539

# SlowHTTPTest #

[![Build Status](https://travis-ci.org/shekyan/slowhttptest.svg?branch=master)](https://travis-ci.org/shekyan/slowhttptest)

SlowHTTPTest is a highly configurable tool that simulates some Application Layer Denial of Service attacks by prolonging HTTP connections in different ways.

Use it to test your web server for DoS vulnerabilites, or just to figure out how many concurrent connections it can handle.
SlowHTTPTest works on majority of Linux platforms, OS X and Cygwin - a Unix-like environment and command-line interface for Microsoft Windows, and comes with a Dockerfile to make things even easier.

Check out [Wiki](https://github.com/shekyan/slowhttptest/wiki) for installation and usage details.

Latest official image is available at [Docker Hub](https://hub.docker.com/repository/docker/shekyan/slowhttptest):
`docker pull shekyan/slowhttptest:latest`

## command for help ##

slowhttptest -h

slowhttptest, a tool to test for slow HTTP DoS vulnerabilities - version 1.8.3

Usage: slowhttptest [options ...]

Test modes:

  -H               slow headers a.k.a. Slowloris (default)
  
  -B               slow body a.k.a R-U-Dead-Yet
  
  -R               range attack a.k.a Apache killer
  
  -X               slow read a.k.a Slow Read
  
Reporting options:

  -g               generate statistics with socket state changes (off)
  
  -o file_prefix   save statistics output in file.html and file.csv (-g required)
  
  -v level         verbosity level 0-4: Fatal, Info, Error, Warning, Debug
  
General options:

  -c connections   target number of connections (50)
  
  -i seconds       interval between followup data in seconds (10)
  
  -l seconds       target test length in seconds (240)
  
  -r rate          connections per seconds (50)
  
  -s bytes         value of Content-Length header if needed (4096)
  
  -t verb          verb to use in request, default to GET for
