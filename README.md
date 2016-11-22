# Requirements
1. Install [Docker Toolbox]( https://www.docker.com/docker-toolbox ) or [`docker-machine`]( https://docs.docker.com/machine/install-machine/ ).
2. Sign up for an [AWS]( https://aws.amazon.com ) account.
3. Possibly a [Docker Hub]( https://hub.docker.com ) account if needed for logging in.

# Setting up AWS
1. Follow all the steps in configuring [IAM]( https://aws.amazon.com/iam ). The most important are the following.
   1. Delete your root access keys
   2. Create individual IAM users
   3. Use groups to assign permissions
2. Get a copy of your access and secret user keys.
3. Make sure your user and/or group have access to all relevant AmazonEC2 policies (choosing all works). Ignore ECS policies as they are unneeded.

# Creating a machine
1. Run `docker login` if you have a Docker Hub account.
2. Create a machine on AWS with `docker-machine`
   1. Run `docker-machine create --driver amazonec2` to get a sense of relevant options that are available.
   2. The following are required options.
      1. Access Key
      2. Secret Key
      3. VPC ID
      4. Machine name
   3. The following are recommended options (have defaults, but should be set).
      1. Instance Type
      2. Root Size (or Root Disk Size)
      3. Region (if not on the US East Coast)
      4. Zone (if not "a").
   4. Using your options create a new machine.

# Start and connect to AWS VM
1. Run `docker-machine start <MACHINE NAME>` if it is not already running.
2. Regenerate certificates `docker-machine regenerate-certs -f <MACHINE NAME>`. Could skip to 3, but return and continue from here if it suggest doing this.
3. Activate your environment `eval $(docker-machine env <MACHINE NAME>)`.
4. Now you can use `docker` remotely.

# Other thoughts.
1. We have mentioned AWS here, but other host services could use a similar procedure with modifications.
2. Port mapping is possible by editing the inbound ports using the EC2 Dashboard and looking for "Network & Security" then "Security Group". Set the inbound ports.
