# Lauch-AWS-resources-via-Ansible
Ansible playbook to deploy AWS resources, "SSH key", "Security Group" and "Instance".


</br>
</br>
</br>
</br>
We are deploying "Auto Scaling group" feature via Ansible script.</br>
This playbook has major 2 parts.

##### 1. Multiple resources creation.

Resources includes: </br>
`a) SSH key pair`
</br>  
`b) Security group`
</br>
Inbound rules for ports 22, 80 and 443 is enabled.</br>
All traffic is set for outbound rule. </br>
</br>
`c) EC2 instance using Security group and SSH key pair created`
 </br>
We are launching 2 instances with option "exact_count". </br>
</br>
Ansible "pause" module is enabled with 2 mins inorder to get the instances ready and proceed to next tasks.
</br>

The next task is for gathering facts based on the instances created.</br> Facts are fectched in such a way that a filter is setup to sort instances based on tags</br>
These will be passed for the execution of next tasks. </br>
</br>
Another task is for a dynamic inventory.</br>
A dynamic inventory plugin allows users to point at data sources to compile the inventory of hosts that Ansible uses to target tasks via inventory file.
</br>
Here we define the parameters to login to those instances via SSH, so that the tasks in next part shoulbe deployed on each instances.
</br>
</br>

</br>

##### 2. Deploying website to the instances created using the first part.

In previous part, we have created a dynamic inventary on the Auto scaling group developed via facts gathering. </br>
Here, we clone a website from [Github repo](https://github.com/Haashmi-h/aws-elb-site.git)


</br>
We install and configure webserver with the contents clonned from Github repository on all instances from the "Dynamic Inventory". </br>

</br>
</br>
</br>

**Final o/p from ansible playbook:**


```sh
PLAY RECAP **************************************************************************************************************************************
3.110.170.110              : ok=12   changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
43.205.198.245             : ok=12   changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
localhost                  : ok=7    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```
</br>
</br>

***Website preview on one of the instance***
</br>
Same will be shown on other instance with hostname updated.

![image](https://user-images.githubusercontent.com/117455666/221665980-47e13dc6-5e2d-4e3b-bf54-c36f0af0cf08.png)
