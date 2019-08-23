# deployment_rules
Some rules to follow when doing software deployment:

1. Debug flag, debug information, verbose, debug logging
2. can save debug information so as to repeat it in another machine/ in the future
3. Remote debug (remote ssh)
4.  Program/executable can auto restart out of unexpected crash/failure, try/catch phrase
5.  config file for c++ program, so no need to recompile after tiny bug fix
6. program run as service in the background, no console output, output all log to syslog
7. Running background program for ~2 weeks, see if any crashes related to time of using
8. Logging need to set max log size, use RotatingFileHandler
9. Use relative path for config files, 
for example
script_path=os.path.dirname(os.path.realpath(sys.argv[0]))
config_path=os.path.join(script_path, 'config/yolov3-spp.cfg')

Reference:
http://tempvariable.blogspot.com/2009/07/how-to-add-program-to-run-at-startup-in.html

