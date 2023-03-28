<!-- Make sure we don't have an existing Issue that reports the bug you are seeing (both open and closed).
If you do find an existing Issue, re-open or add a comment to that Issue instead of creating a new one. If your issue is not specific to aws-elastic-beanstalk-cli try posting it to the AWS Elastic Beanstalk forum(https://forums.aws.amazon.com/forum.jspa?forumID=86).-->

### Description


Eb and EB CLI going haywire

### Steps to reproduce

1. create a simple flask application that outputs your env vars
2. eb init -p python-3.7 findmyrole-test --region us-east-1
3. eb init to get keypairs to access the EC2 isntance
4. eb create findmyrole-test-env
5. eb setenv FLASK_BACKEND_ENV="dev"
6. eb setenv FLASK_BACKEND_ENV="[ANY OTHER STRING]"

you will find that the value does not change even updating the code, if there was an error in the beginning then its like the whole application is cached and theres nothing you can do

this worked on the miminal application but on the actual application is where the phantom stuff starts to happen

### Observed result

Please provide command output with `--debug` flag set.
root@e7ef131a9cdd:~/eb-flask# eb setenv FLASK_BACKEND_ENV="PREVIEW" -e findmyrole-eb-env-dev-0 --debug
2023-03-28 04:56:40,937 (DEBUG) cement.core.foundation : laying cement for the 'eb' application
2023-03-28 04:56:40,937 (DEBUG) cement.core.hook : defining hook 'pre_setup'
2023-03-28 04:56:40,937 (DEBUG) cement.core.hook : defining hook 'post_setup'
2023-03-28 04:56:40,937 (DEBUG) cement.core.hook : defining hook 'pre_run'
2023-03-28 04:56:40,938 (DEBUG) cement.core.hook : defining hook 'post_run'
2023-03-28 04:56:40,938 (DEBUG) cement.core.hook : defining hook 'pre_argument_parsing'
2023-03-28 04:56:40,938 (DEBUG) cement.core.hook : defining hook 'post_argument_parsing'
2023-03-28 04:56:40,938 (DEBUG) cement.core.hook : defining hook 'pre_close'
2023-03-28 04:56:40,938 (DEBUG) cement.core.hook : defining hook 'post_close'
2023-03-28 04:56:40,938 (DEBUG) cement.core.hook : defining hook 'signal'
2023-03-28 04:56:40,938 (DEBUG) cement.core.hook : defining hook 'pre_render'
2023-03-28 04:56:40,938 (DEBUG) cement.core.hook : defining hook 'post_render'
2023-03-28 04:56:40,938 (DEBUG) cement.core.hook : registering hook 'add_handler_override_options' from cement.core.foundation into hooks['post_setup']
2023-03-28 04:56:40,938 (DEBUG) cement.core.hook : registering hook 'handler_override' from cement.core.foundation into hooks['post_argument_parsing']
2023-03-28 04:56:40,938 (DEBUG) cement.core.handler : defining handler type 'extension' (IExtension)
2023-03-28 04:56:40,938 (DEBUG) cement.core.handler : defining handler type 'log' (ILog)
2023-03-28 04:56:40,938 (DEBUG) cement.core.handler : defining handler type 'config' (IConfig)
2023-03-28 04:56:40,938 (DEBUG) cement.core.handler : defining handler type 'mail' (IMail)
2023-03-28 04:56:40,938 (DEBUG) cement.core.handler : defining handler type 'plugin' (IPlugin)
2023-03-28 04:56:40,938 (DEBUG) cement.core.handler : defining handler type 'output' (IOutput)
2023-03-28 04:56:40,938 (DEBUG) cement.core.handler : defining handler type 'argument' (IArgument)
2023-03-28 04:56:40,938 (DEBUG) cement.core.handler : defining handler type 'controller' (IController)
2023-03-28 04:56:40,938 (DEBUG) cement.core.handler : defining handler type 'cache' (ICache)
2023-03-28 04:56:40,939 (DEBUG) cement.core.handler : registering handler '<class 'cement.core.extension.CementExtensionHandler'>' into handlers['extension']['cement']
2023-03-28 04:56:40,956 (DEBUG) cement.ext.ext_plugin : plugin config dir /etc/eb/plugins.d does not exist.
2023-03-28 04:56:40,956 (DEBUG) cement.ext.ext_plugin : plugin config dir /root/.eb/plugins.d does not exist.
2023-03-28 04:56:40,963 (DEBUG) ebcli.core.hooks : -- EBCLI Version: 3.20.5
2023-03-28 04:56:40,964 (DEBUG) ebcli.core.hooks : -- Python Version: 3.11.2 (main, Mar 24 2023, 23:30:44) [GCC 11.3.0]
2023-03-28 04:56:40,964 (DEBUG) ebcli.core.fileoperations : Project root found at: /root/eb-flask
2023-03-28 04:56:40,966 (DEBUG) ebcli.core.fileoperations : Project root found at: /root/eb-flask
2023-03-28 04:56:40,968 (DEBUG) ebcli.core.fileoperations : Project root found at: /root/eb-flask
2023-03-28 04:56:40,970 (DEBUG) ebcli.core.fileoperations : Project root found at: /root/eb-flask
2023-03-28 04:56:40,972 (DEBUG) ebcli.core.fileoperations : Project root found at: /root/eb-flask
2023-03-28 04:56:40,974 (DEBUG) ebcli.core.fileoperations : Project root found at: /root/eb-flask
2023-03-28 04:56:40,976 (DEBUG) ebcli.core.fileoperations : Project root found at: /root/eb-flask
2023-03-28 04:56:40,979 (DEBUG) ebcli.core.fileoperations : Project root found at: /root/eb-flask
2023-03-28 04:56:40,981 (DEBUG) ebcli.core.fileoperations : Project root found at: /root/eb-flask
2023-03-28 04:56:40,983 (DEBUG) ebcli.core.fileoperations : Project root found at: /root/eb-flask
2023-03-28 04:56:40,984 (DEBUG) ebcli.lib.elasticbeanstalk : Inside update_environment api wrapper
2023-03-28 04:56:40,985 (DEBUG) ebcli.lib.aws : Creating new Botocore Session
2023-03-28 04:56:40,985 (DEBUG) ebcli.lib.aws : Botocore version: 1.29.81
2023-03-28 04:56:40,994 (DEBUG) ebcli.lib.aws : Creating new Botocore Client for elasticbeanstalk
2023-03-28 04:56:41,078 (DEBUG) ebcli.lib.aws : Successfully created session for elasticbeanstalk
2023-03-28 04:56:41,078 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, update_environment) to region: us-east-1 with args:{'EnvironmentName': 'findmyrole-eb-env-dev-0', 'OptionSettings': [{'Namespace': 'aws:elasticbeanstalk:application:environment', 'OptionName': 'FLASK_BACKEND_ENV', 'Value': 'PREVIEW'}]}
2023-03-28 04:56:43,173 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:56:43,173 (DEBUG) ebcli.lib.aws : Response: {'EnvironmentName': 'findmyrole-eb-env-dev-0', 'EnvironmentId': 'e-3gbkcrymyd', 'ApplicationName': 'findmyrole-eb-app-dev-0', 'VersionLabel': 'app-230328_044151261453', 'SolutionStackName': '64bit Amazon Linux 2 v3.5.0 running Python 3.7', 'PlatformArn': 'arn:aws:elasticbeanstalk:us-east-1::platform/Python 3.7 running on 64bit Amazon Linux 2/3.5.0', 'Description': 'Environment created from the EB CLI using "eb create"', 'EndpointURL': 'awseb-AWSEB-11XJIB5CZ42CV-1578997106.us-east-1.elb.amazonaws.com', 'CNAME': 'findmyrole-eb-env-dev-0.eba-rtq3h3an.us-east-1.elasticbeanstalk.com', 'DateCreated': datetime.datetime(2023, 3, 28, 4, 8, 13, 345000, tzinfo=tzlocal()), 'DateUpdated': datetime.datetime(2023, 3, 28, 4, 56, 42, 124000, tzinfo=tzlocal()), 'Status': 'Updating', 'AbortableOperationInProgress': True, 'Health': 'Grey', 'Alerts': [], 'Tier': {'Name': 'WebServer', 'Type': 'Standard', 'Version': '1.0'}, 'EnvironmentArn': 'arn:aws:elasticbeanstalk:us-east-1:085681231235:environment/findmyrole-eb-app-dev-0/findmyrole-eb-env-dev-0', 'ResponseMetadata': {'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:56:42 GMT', 'RetryAttempts': 0}}
2023-03-28 04:56:43,173 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:56:43,173 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48'}
2023-03-28 04:56:43,441 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:56:43,441 (DEBUG) ebcli.lib.aws : Response: {'Events': [{'EventDate': datetime.datetime(2023, 3, 28, 4, 56, 42, 46000, tzinfo=tzlocal()), 'Message': 'Environment update is starting.', 'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'Severity': 'INFO'}], 'ResponseMetadata': {'RequestId': '59d3ed08-47ac-4ef8-a47f-de1312eb28c6', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:56:43 GMT', 'RetryAttempts': 0}}
2023-03-28 04:56:42    INFO    Environment update is starting.
 -- Events -- (safe to Ctrl+C) Use "eb abort" to cancel the command.2023-03-28 04:56:48,441 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:56:48,442 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:42.047000+00:00'}
2023-03-28 04:56:48,504 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:56:48,504 (DEBUG) ebcli.lib.aws : Response: {'Events': [], 'ResponseMetadata': {'RequestId': '981b49c9-df3d-4a88-a0b3-4cd54cb7403e', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:56:48 GMT', 'RetryAttempts': 0}}
2023-03-28 04:56:53,504 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:56:53,505 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:42.047000+00:00'}
2023-03-28 04:56:53,591 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:56:53,591 (DEBUG) ebcli.lib.aws : Response: {'Events': [{'EventDate': datetime.datetime(2023, 3, 28, 4, 56, 49, 925000, tzinfo=tzlocal()), 'Message': "Updating environment findmyrole-eb-env-dev-0's configuration settings.", 'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'Severity': 'INFO'}], 'ResponseMetadata': {'RequestId': 'b157c4c2-f36a-46bb-ba79-bcf79acc8bcc', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:56:53 GMT', 'RetryAttempts': 0}}
2023-03-28 04:56:49    INFO    Updating environment findmyrole-eb-env-dev-0's configuration settings.
 -- Events -- (safe to Ctrl+C) Use "eb abort" to cancel the command.2023-03-28 04:56:58,592 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:56:58,593 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:49.926000+00:00'}
2023-03-28 04:56:58,675 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:56:58,675 (DEBUG) ebcli.lib.aws : Response: {'Events': [], 'ResponseMetadata': {'RequestId': '9b0a2664-a3ac-4c57-b3de-a9de39d326d9', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:56:58 GMT', 'RetryAttempts': 0}}
2023-03-28 04:57:03,676 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:57:03,676 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:49.926000+00:00'}
2023-03-28 04:57:03,752 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:57:03,752 (DEBUG) ebcli.lib.aws : Response: {'Events': [], 'ResponseMetadata': {'RequestId': '45009127-ca6a-4c9f-a67a-2cfc1c641b1d', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:57:04 GMT', 'RetryAttempts': 0}}
2023-03-28 04:57:08,753 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:57:08,753 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:49.926000+00:00'}
2023-03-28 04:57:08,845 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:57:08,845 (DEBUG) ebcli.lib.aws : Response: {'Events': [], 'ResponseMetadata': {'RequestId': '69c2874c-6590-41de-a8ca-dba73689d417', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:57:09 GMT', 'RetryAttempts': 0}}
2023-03-28 04:57:13,845 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:57:13,846 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:49.926000+00:00'}
2023-03-28 04:57:13,899 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:57:13,899 (DEBUG) ebcli.lib.aws : Response: {'Events': [], 'ResponseMetadata': {'RequestId': '1e9b148e-620c-40ec-a3d7-0d847962e75f', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:57:14 GMT', 'RetryAttempts': 0}}
2023-03-28 04:57:18,899 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:57:18,900 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:49.926000+00:00'}
2023-03-28 04:57:18,976 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:57:18,977 (DEBUG) ebcli.lib.aws : Response: {'Events': [], 'ResponseMetadata': {'RequestId': '24c784db-0ca3-4b23-8fa4-a1038f44377d', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:57:18 GMT', 'RetryAttempts': 0}}
2023-03-28 04:57:23,978 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:57:23,978 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:49.926000+00:00'}
2023-03-28 04:57:24,075 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:57:24,075 (DEBUG) ebcli.lib.aws : Response: {'Events': [], 'ResponseMetadata': {'RequestId': '446f16e9-8fe0-4eb9-9155-a40eb7aa1723', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:57:24 GMT', 'RetryAttempts': 0}}
2023-03-28 04:57:29,076 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:57:29,076 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:49.926000+00:00'}
2023-03-28 04:57:29,149 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:57:29,149 (DEBUG) ebcli.lib.aws : Response: {'Events': [], 'ResponseMetadata': {'RequestId': '84fcabf0-313c-4694-b3b8-561f1682b91f', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:57:29 GMT', 'RetryAttempts': 0}}
2023-03-28 04:57:34,150 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:57:34,151 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:49.926000+00:00'}
2023-03-28 04:57:34,227 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:57:34,228 (DEBUG) ebcli.lib.aws : Response: {'Events': [], 'ResponseMetadata': {'RequestId': 'a89c3afe-d327-4ec3-a190-95225e9c5c28', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:57:34 GMT', 'RetryAttempts': 0}}
2023-03-28 04:57:39,228 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:57:39,229 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:49.926000+00:00'}
2023-03-28 04:57:39,311 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:57:39,311 (DEBUG) ebcli.lib.aws : Response: {'Events': [], 'ResponseMetadata': {'RequestId': 'aa32bed1-0294-4027-acba-298fa293b411', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:57:39 GMT', 'RetryAttempts': 0}}
2023-03-28 04:57:44,312 (DEBUG) ebcli.lib.elasticbeanstalk : Inside get_new_events api wrapper
2023-03-28 04:57:44,312 (DEBUG) ebcli.lib.aws : Making api call: (elasticbeanstalk, describe_events) to region: us-east-1 with args:{'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'StartTime': '2023-03-28 04:56:49.926000+00:00'}
2023-03-28 04:57:44,398 (DEBUG) ebcli.lib.aws : API call finished, status = 200
2023-03-28 04:57:44,398 (DEBUG) ebcli.lib.aws : Response: {'Events': [{'EventDate': datetime.datetime(2023, 3, 28, 4, 57, 42, 841000, tzinfo=tzlocal()), 'Message': 'Environment update completed successfully.', 'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'Severity': 'INFO'}, {'EventDate': datetime.datetime(2023, 3, 28, 4, 57, 42, 787000, tzinfo=tzlocal()), 'Message': 'Successfully deployed new configuration to environment.', 'ApplicationName': 'findmyrole-eb-app-dev-0', 'EnvironmentName': 'findmyrole-eb-env-dev-0', 'RequestId': '760d03b6-ea63-443e-a7dc-7f48895cea48', 'Severity': 'INFO'}], 'ResponseMetadata': {'RequestId': 'dd728203-cf55-4758-8da5-c86867611c69', 'HTTPStatusCode': 200, 'date': 'Tue, 28 Mar 2023 04:57:44 GMT', 'RetryAttempts': 0}}
2023-03-28 04:57:42    INFO    Successfully deployed new configuration to environment.

### Expected result

Describe what you expected.
I expected the app to work and to see the env var properly set as expected
### Additional environment details (Ex: Windows, Mac, Amazon Linux etc)

1. Python 3.7 running on 64bit Amazon Linux 2/3.5.0

Change
2. EBCLI version: EB CLI 3.20.5 (Python 3.11.2 (main, Mar 24 2023, 23:30:44) [GCC 11.3.0])
