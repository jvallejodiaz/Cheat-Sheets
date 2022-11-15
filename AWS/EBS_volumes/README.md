# EBS volumes

## Performance penalty when restored from a snapshot.

We had the situation in which we lunched a EC2 instance from an AMI image. The image ran a docker container and had one EBS data volume (gp3). When the AMI was launched, the volume was restored from snapshot. 

EBS volumes have a performance penalty when they are restored form a snapshot. This problem caused taht the docker containers using that data volume were extremely slow the first time the accessed the data. 

This problem was resorved intialising the volumes using userdata scripts and adding a warm pool in the autoscaling to avoid the time to restart: 

```
# using dd
sudo dd if=/dev/nvme0n1 of=/dev/null bs=5M

# using fio performance 
sudo apt-get install -y fio
sudo fio --filename=/dev/xvdf --rw=read --bs=128k --iodepth=32 --ioengine=libaio --direct=1 --name=volume-initialize
```