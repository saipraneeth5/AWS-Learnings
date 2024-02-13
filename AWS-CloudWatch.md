# Cloud Watch Installation and Configuration
## Create an IAM role
- Navigate to IAM and select `Roles` option under Access Management.
- Click on `create role` option.
- Under `Selected trusted entity`, select `AWS Service`.
- Under `Use case`, select `EC2` from dropdown and click on `Next`.
- Under `Permission policies`, use `search` box for finding CloudWatch Agent policy. Type `cloudwatchagent`, from poplulated  list select `CloudWatchAgentServerPolicy` and `CloudWatchAgentAdminPolicy` and click `Next`.
- Provide `Role name` and click on `Create role`.

## Create a EC2 Instance.
- Navigate to `EC2` menu by using `Search` box on top.
- Launch an instance. Go with defaults.
- Check the created instance and click `Actions`, hover and click `Security`, and select `Modify IAM role`. Select the created IAM for CloudWatch from dropdown.
- Connect to the instance by using `EC2 Instance Connect` option.
- Elevate your privileges by executing `sudo su`.
- Execute `yum install httpd -y` to generate logs for the application and to send to CloudWatch`
- Create a index.html file at path `/var/www/html/index.html` with some content.
- Start the httpd service by exectuing `sudo systemctl start httpd`.

## CloudWatch agent installation and setup.
- Install the CloudWatch agent in the EC2 instance by exectuing `sudo yum install amazon-cloudwatch-agent -y`.
- Execute `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard` for performing CloudWatch configuration. Configure according to your needs.
- For generating logs in CloudWatch or For a new instance if we want to use same CloudWatch configuration from SSM parameter store, execute `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c ssm:{name_of_the_parameter} -s`
