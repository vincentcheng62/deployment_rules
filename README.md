# deployment_rules
Some rules to follow when doing software deployment:

1. Debug flag, debug information, verbose, debug logging
For example: python logger module
Also, need to log all the parameters during the running, e.g. IsOnlyDetectPerson=False

2. can save debug information so as to repeat it in another machine/ in the future(e.g. save resized boundingbox image as base64)
3. Remote debug (remote ssh)
4. Program/executable can auto restart out of unexpected crash/failure, try/catch phrase
5. config file for c++ program, so no need to recompile after tiny bug fix
6. program run as service in the background, no console output, output all log to syslog (systemctl, daemon)
https://tecadmin.net/setup-autorun-python-script-using-systemd/

7. Running background program for ~2 weeks, see if any crashes related to time of using (e.g. camera connection lost, need to reopen)
for example
    ret, frame = vid.read()
    if not ret:
        logger.warning('connection to the camera lost! reopen now...')
        vid.release()
        vid.open(videopath)
        logger.warning('camera is reopened!')
        ret, frame = vid.read()
        if not ret:
            logger.error('reopened camera is fail again, program exit!!')
            break

8. Logging need to set max log size, use RotatingFileHandler
my_handler = RotatingFileHandler(logFilePath, mode=LoggingFormat, maxBytes=MaxLogFileSizeInMb*1024*1024, 
                                 backupCount=2, encoding=None, delay=False)
my_handler.setFormatter(log_formatter)
my_handler.setLevel(logging.INFO)
logger.addHandler(my_handler)

9. Use relative path for config files, 
for example
script_path=os.path.dirname(os.path.realpath(sys.argv[0]))
config_path=os.path.join(script_path, 'config/yolov3-spp.cfg')

10. time elapse logging between main functions, only need to log at some frequency, e.g. 1 out of 1000

Reference:
http://tempvariable.blogspot.com/2009/07/how-to-add-program-to-run-at-startup-in.html

