# Prerequisites<a name="prerequisites"></a>

To perform this getting started exercise, you need the following:
+ An AWS account with the permissions necessary to create an Amazon FSx for Lustre file system and an Amazon EC2 instance\. For more information, see [Setting up](setting-up.md)\.
+ An Amazon EC2 instance running a supported Linux release in your virtual private cloud \(VPC\) based on the Amazon VPC service\. You will install the Lustre client on this EC2 instance, and then mount your FSx for Lustre file system on the EC2 instance\. The Lustre client supports Amazon Linux, Amazon Linux 2, CentOS and Red Hat Enterprise Linux 7\.5, 7\.6, 7\.7, 7\.8, 7\.9, 8\.2, and 8\.3, SUSE Linux Enterprise Server 12 SP3, SP4, and SP5, and Ubuntu 16\.04, 18\.04, and 20\.04\. For this getting started exercise, we recommend using Amazon Linux 2\.

  When creating your Amazon EC2 instance for this getting started exercise, keep the following in mind:
  + We recommend that you create your instance in your default VPC\.
  + We recommend that you use the default security group when creating your EC2 instance\.
+ An Amazon S3 bucket storing the data for your workload to process\. The S3 bucket will be the linked durable data repository for your FSx for Lustre file system\.
+ Determine which type of Amazon FSx for Lustre file system you want to create, *scratch* or *persistent*\. For more information, see [File system deployment options for FSx for Lustre ](using-fsx-lustre.md#lustre-deployment-types)\.