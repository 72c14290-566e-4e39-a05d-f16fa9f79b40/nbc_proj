## NBC Project

I did this project using ansible and the ansible aws modules because that is what I've been working in for the past couple of years.
Additionally, I used aws for the same reason.  I didn't even try and run this code so I'm sure its full of errors

### Things I did

For this project, I tried to focus on getting the basic best practices in place, and getting the skeleton in place for all the requirements
* Webservers and SQL must be spread across many AZs in case of provider errors
* Everything has a reasonable security group, i.e. MySQL and redis are not exposed to the public internet 
* Minimal Public IPs are used
* IAM Roles are attached to machines when they are created.
* ELB is set up to offload ssl 
* Logging is enabled for the ELB
* Instances join to the ELB at runtime

### Things I skipped in the interest of time, or could have improved

To make this close to runnable there are alot of things which need doing
* I didn't template many things which are rightly variables
* I didn't fill out the group\_vars files for the things which I did template
* I didn't write the IAM policy files for the machines
* I didn't have or follow a great naming convention
* I didn't put in enough tags
* Too much yank and paste, should be DRYer (i.e with\_items for buckets and security groups, a role for instances)

### Assumptions I made

I assumed many things existed outside of this project, or were designed in a specific way
* SSH keys
* VPC
* Public and Private Subnets exist
* redis is a cache for mysql and doesn't need to be HA


### Lists of things I did get done
#### Three running web servers behind a load balancer, which is publicly accessible. The web servers should have NodeJS, Ruby and Java installed

1. Create security groups for ELB and webserver nodes
2. Create bucket for ELB logs
3. Create ELB
4. Create Role for s3
5. Create 3 nodes in 3 different AZs with role attached
6. Install dependencies
7. Start httpd
8. Add nodes into ELB


#### A Redis installation accessible by the web servers

1. Create security group for redis
2. Create redis node
3. Install redis
4. Start redis service

#### A relational database of your choice accessible by the web servers

1. Create security group for RDS instance
2. Provision RDS instance

#### A cloud storage bucket (S3 or similar) with read-only access from the web servers.

1. Create s3 bucket
2. Create role for s3 readonly on the bucket
3. Ensure role is attached to webserver machines
