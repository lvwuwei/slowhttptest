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
  
  EXAMPLES
     Start a slowloris test of host.example.com with 1000 connections, statistics goes into
     my_header_stats, interval between follow up headers is 10 seconds and connection rate is 200
     connections per second:

           $ slowhttptest -c 1000 -H -g -o my_header_stats -i 10 -r 200 -t GET -u https://host.example.com/index.html -x 24 -p 3

     Start slow POST test of host.example.com with 3000 connections, statistics goes into
     my_body_stats, interval between follow up headers is 110 seconds, connection rate is 200
     connections per second, Content-Length header value is 8192, maximum length of follow up
     data is random value limited by 10 bytes and probe connections waits 3 seconds for HTTP
     response before marking server as DoSed:

           $ slowhttptest -c 3000 -B -g -o my_body_stats -i 110 -r 200 -s 8192 -t FAKEVERB -u http://host.example.com/loginform.html -x 10 -p 3

     Start Range Header test of host.example.com with 1000 connections, use HEAD verb, and
     generate HTTP header Range:0-, x-1, x-2, x-3, ... x-y, where x is 10 and y is 3000,
     connection rate is 500: interval between follow up headers is 10 seconds and connection rate
     is 200 connections per second:

           $ slowhttptest -R -u http://host.example.com/ -t HEAD -c 1000 -a 10 -b 3000 -r 500

     Start Slow Read test of host.example.com with 8000 connections, no statistics is generated,
     connection rate is 200 connections per second, TCP advertised window size is a random value
     between 512 and 1024, slowhttptest reads 32 bytes from each connections every 5 seconds, 3
     requests are pipelined per each connections, probe connection waits 3 seconds for HTTP
     response before marking server as DoSed:

           $ slowhttptest -c 8000 -X -r 200 -w 512 -y 1024 -n 5 -z 32 -k 3 -u https://host.example.com/resources/index.html -p 3

     Start Slow Read test of host.example.com through HTTP proxy server at 10.10.0.1:8080 with
     8000 connections, no statistics is generated, the rest test vaules are default.
     slowhttptest most likely would test HTTP proxy server itself, rather than target server, but
     it all depends on the HTTP proxy server implementation:

           $ slowhttptest -d 10.10.0.1:8080 -c 8000 -X -u https://host.example.com/resources/index.html

     Start Slow Read test of host.example.com and direct probe traffic through HTTP proxy server
     at 10.10.0.1:8080 with 8000 connections, no statistics is generated, the rest test vaules
     are default.  Specifying another connection channel for probe connections helps to make sure
     that slowhttptest shows valid statistics for availability of server under test:

           $ slowhttptest -e 10.10.0.1:8080 -c 8000 -X -u
           https://host.example.com/resources/index.html

