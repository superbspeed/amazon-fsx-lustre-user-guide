# Mounting Amazon FSx file systems from on\-premises or a peered Amazon VPC<a name="mounting-on-premises"></a>

You can access your Amazon FSx file system in two ways\. One is from Amazon EC2 instances located in an Amazon VPC that's peered to the file system's VPC\. The other is from on\-premises clients that are connected to your file system's VPC using AWS Direct Connect or VPN\.

You connect the client's VPC and your Amazon FSx file system's VPC using either a VPC peering connection or a VPC transit gateway\. When you use a VPC peering connection or transit gateway to connect VPCs, Amazon EC2 instances that are in one VPC can access Amazon FSx file systems in another VPC, even if the VPCs belong to different accounts\.

Before using the following the procedure, you need to set up either a VPC peering connection or a VPC transit gateway\. 

A *transit gateway* is a network transit hub that you can use to interconnect your VPCs and on\-premises networks\. For more information about using VPC transit gateways, see [Getting Started with Transit Gateways](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-getting-started.html) in the *Amazon VPC Transit Gateways Guide*\.

A *VPC peering connection* is a networking connection between two VPCs\. This type of connection enables you to route traffic between them using private Internet Protocol version 4 \(IPv4\) or Internet Protocol version 6 \(IPv6\) addresses\. You can use VPC peering to connect VPCs within the same AWS Region or between AWS Regions\. For more information on VPC peering, see [What is VPC Peering?](https://docs.aws.amazon.com/vpc/latest/peering/Welcome.html) in the *Amazon VPC Peering Guide*\.

You can mount your file system from outside its VPC using the IP address of its primary network interface\. The primary network interface is the first network interface returned when you run the `aws fsx describe-file-systems` AWS CLI command\. You can also get this IP address from the Amazon Web Services Management Console\.

The following table illustrates IP address requirements for accessing Amazon FSx file systems using a client that's outside of the file system's VPC\.

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/fsx/latest/LustreGuide/mounting-on-premises.html)

If you need to access your Amazon FSx file system that was created before December 17, 2020 using a non\-private IP address range, you can create a new file system by restoring a backup of the file system\. For more information, see [Working with backups](using-backups-fsx.md)\.

**To retrieve the IP address of the primary network interface for a file system**

1. Open the Amazon FSx console at [https://console\.aws\.amazon\.com/fsx/](https://console.aws.amazon.com/fsx/)\.

1. In the navigation pane, choose **File systems**\.

1. Choose your file system from the dashboard\.

1. From the file system details page, choose **Network & security**\.

1. For **Network interface**, choose the ID for your primary elastic network interface\. Doing this takes you to the Amazon EC2 console\.

1. On the **Details** tab, find the **Primary private IPv4 IP**\. This is the IP address for your primary network interface\.

**Note**  
You can't use Domain Name System \(DNS\) name resolution when mounting an Amazon FSx file system from outside the VPC it is associated with\.