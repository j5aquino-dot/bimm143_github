
## Core Unix commands

Most unix commands have super short names, which makes them quick to type but annoying to learn
Major file system related commands include:

pwd:	Print working directory
ls:	list
cd: 	change directory
mkdir:	make a new directory
rm:	remove files and directories (delete)
cp:	copy files or dirs (source > destination)
mv:	move files or dirs (basically re-name)
nano:	text editor (basic but always available) 

curl: Download files from the web or ftp
wget: Download files from the web
tar -zxvf: UnTar (package) Tar archive files
gunzip: UnZip files
$PATH: the places (directory) to look for programs 


## AWS EC2 Instance

Connect to my instance with:
ssh -i ~/OneDrive/Desktop/bimm143_ja.pem ubuntu@ec2-35-85-145-154.us-west-2.compute.amazonaws.com


Secure copy files between machines, in this case, from our instance to our laptop

scp -i ~/OneDrive/Desktop/bimm143_ja.pem ubuntu@ec2-35-85-145-154.us-west-2.compute.amazonaws.com:/home/ubuntu/work/bimm143_github/class16/results.txt .


## Class 17 Instance

ssh -i ~/OneDrive/Desktop/bimm143_ja.pem ubuntu@ec2-44-255-185-118.us-west-2.compute.amazonaws.com

export KEY=~/OneDrive/Desktop/bimm143_ja.pem

export SERVER=ubuntu@ec2-44-255-185-118.us-west-2.compute.amazonaws.com

ssh -i $KEY $SERVER

scp -r -i $KEY $SERVER:~/*_quant . 


