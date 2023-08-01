# Set the retention period across Cloudwatch log groups with BOT0 3 as a cost saving exercise


If you have multiple log groups across multiple accounts and regions, automation can help to maintain a common configuration for  your log groups.

CAVEAT: This approach will delete log data and it is not recoverable. Set the appropriate retention period for your log groups.

My approach here is to use an inline Lambda as the code is fairly simple and does not require installing non-default modules.
A CloudWatch events rule triggers the function daily. It:

- loops through the configured regions in the AWS account the lambda runs in
- gets a list of all log groups in each region
- creates a sub-list of log groups without a retention period ( if any ) 
- checks what the retention period should be for each group without a retention period
- sets the retention period on the log group

I've used a single retention setting for all log groups in my example. You may wish to have different settings for different log groups on criteria that makes sense to you.