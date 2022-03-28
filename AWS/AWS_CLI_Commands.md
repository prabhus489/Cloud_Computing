# Set the Region
AZ=`curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone`

export AWS_DEFAULT_REGION=${AZ::-1}

# Obtain latest Linux AMI
AMI=$(aws ssm get-parameters --names /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2 --query 'Parameters[0].[Value]' --output text)

echo $AMI

#### to get Subnet detail
SUBNET=$(aws ec2 describe-subnets --filters 'Name=tag:Name,Values=LabPublicSubnet' --query Subnets[].SubnetId --output text)

echo $SUBNET

#### to get SG
SG=$(aws ec2 describe-security-groups --filters Name=tag:Name,Values=LabInstanceSecurityGroup --query SecurityGroups[].GroupId --output text)

echo $SG

#### to download userdata script
cd ~

wget https://EC2/scripts/UserDataInstanceB.txt

cat UserDataInstanceB.txt

#### To launch an instance

INSTANCE=$(\
aws ec2 run-instances \
--image-id $AMI \
--subnet-id $SUBNET \
--security-group-ids $SG \
--user-data file://./UserDataInstanceB.txt \
--instance-type t3.micro \
--tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=InstanceB}]' \
--query 'Instances[*].InstanceId' \
--output text \
)

echo $INSTANCE

#### detailed info of created new instance
aws ec2 describe-instances --instance-ids $INSTANCE

#### instance running state information
aws ec2 describe-instances --instance-ids $INSTANCE --query 'Reservations[].Instances[].State.Name' --output text

#### instance public DNS name to check the response in browser
aws ec2 describe-instances --instance-ids $INSTANCE --query Reservations[].Instances[].PublicDnsName --output text


