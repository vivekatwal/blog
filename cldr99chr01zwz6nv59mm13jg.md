---
title: "Logging in python"
datePublished: Mon Jul 04 2022 10:13:29 GMT+0000 (Coordinated Universal Time)
cuid: cldr99chr01zwz6nv59mm13jg
slug: logging-in-python

---

It doesn't matter how long you have been coding, even today while writing any script we need some manual validation of output and we tend to use `print` statement a lot.

`print`: At the initial phase when you have just started writing the code, you are in the flow to set the logic and the flow of the code, and during this phase, you need to verify different things and so developers use `print` to verify things like the value of the variable, error/exceptions, and print statement to verify whether the code has been entered `if/else` statement.

It is very handy and quick and that's why it is built for.

Print makes the development interactive and fast. Interactive development is a very fast way to iterate on your idea, and logic and that's why many developers like jupyter notebooks.

#### why logging is important

But as the application matures it is put to production in the server, and while code is running in the server we don't know what is happening inside it, but we need that visibility to track input and errors. And for this we have `logging`

#### how to quickly setup logs in a python application

#### why log the logs in JSON format

`Json` makes it easy to directly push logs to different log monitoring tools and services.

Logging in a file in the server

```python
# pip install python-json-logger
from pythonjsonlogger import jsonlogger
def get_logger(logger_name):
    file_name = "/tmp/logs/{}.log".format(logger_name)
    logger = logging.getLogger(logger_name)
    logger.setLevel(logging.DEBUG)
    
    formatter = jsonlogger.JsonFormatter(fmt='%(asctime)s :: %(lineno)s :: %(levelname)-8s :: %(name)s ::  %(message)s')
    
    logHandler = logging.FileHandler(filename=file_name)
    handler.setFormatter(formatter)
    logger.addHandler(handler)
    return logger

logger_name = "login"
login_logger = get_logger(logger_name)
```

#### why and when to use cloudwatch

## Setting up cloudwatch

Setting up the cloud watch client on the server

```bash
sudo aws configure
sudo yum install amazon-cloudwatch-agent
```

verify the installation using the below commands

```bash
cat ~/.aws/credentials
cat ~/.aws/config
```

To check the cloud watch status use the below commands or [here](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/ReportCWLAgentStatus.html)

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a stop
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a start
```

Setting up the python environment

```python

#pip install python-json-logger
#pip install boto3
#pip install watchtower

import boto3
from pythonjsonlogger import jsonlogger
import watchtower

credentials = boto3.Session().get_credentials()
access_key = credentials.access_key
secret_key = credentials.secret_key
region = ""

cloudwatch_client = boto3.client("logs", 
region_name=region,
aws_access_key_id=access_key,
aws_secret_access_key=secret_key
)



def get_logger(log_group, logger_name):    
    logger = logging.getLogger(logger_name)
    logger.setLevel(logging.DEBUG)
    
    formatter = jsonlogger.JsonFormatter(fmt='%(asctime)s :: %(lineno)s :: %(levelname)-8s :: %(name)s ::  %(message)s')
    
    handler = watchtower.CloudWatchLogHandler(log_group_name=log_group, log_stream_name=logger_name, boto3_client=cloudwatch_client)

    handler.setFormatter(formatter)
    logger.addHandler(handler)
    return logger


log_group = "app_name"
login_logger = get_logger(log_group, "login")
```

Reference:

* https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-commandline-fleet.html
    
* https://docs.exasol.com/db/latest/administration/aws/monitoring/aws\_cloudwatch\_agent.htm
    
* [Cloudwatch setting with IAM role](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/QuickStartEC2Instance.html)