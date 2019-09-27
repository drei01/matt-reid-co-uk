---
layout: post
title: Automatically backup ec2 instance
---

Here's a little bash script I've been using to backup ec2 instances

``` bash
#!/bin/bash
#Before running this script, add the following to your ~/.bashrc 
#export AWS_ACCESS_KEY=your_access_key
#export AWS_SECRET_KEY=your_secret_key
#export AWS_REGION=eu-west-1

# initialize the EC2 environment
[ -e /etc/profile.d/aws-apitools-common.sh ] && source /etc/profile.d/aws-apitools-common.sh

# load the access keys
source ~/.bashrc

# locate the instance ID of this VM
instanceid="$(ec2-describe-instances --region $AWS_REGION | grep $(hostname -f) | cut -f2 | head -1)"

if [ -z "$instanceid" ]; then
echo "Failed to locate instance ID" >&2
exit 5
fi


# locate the EBS volume ID for the root file system
rootvolumeid="$(ec2-describe-volumes --region $AWS_REGION | grep "$instanceid" | grep $(mount | egrep 'on / type' | cut -d' ' -f1 | sed -e 's/xvd/sd/;') | cut -f2)"

if [ -z "$rootvolumeid" ]; then
echo "Failed to locate root volume ID" >&2
exit 5
fi


# create the snapshot
snapshotid="$(ec2-create-snapshot --region $AWS_REGION -d "backup-${instanceid}-$(date +"%Y%m%d")" $rootvolumeid | cut -f2)"



if [ -z "$snapshotid" ]; then
echo "Failed to take snapshot" >&2
exit 4
fi

# wait for the snapshot to complete
while [ "$(ec2-describe-snapshots --region $AWS_REGION | grep "$snapshotid" | cut -f4)" != "completed" ]; do
sleep 5
done


# delete old snapshots
ec2-describe-snapshots --region $AWS_REGION | grep "$rootvolumeid" | cut -f2 | grep -v "$snapshotid" | while read snapid; do
if ! ec2-delete-snapshot "$snapid" > /dev/null; then
echo "Failed to delete old snapshot $snapid" >&2
exit 4
fi
done
```

[gist link](https://gist.github.com/drei01/943fa74a6d2a889a346b#file-ebs_backup-sh)

