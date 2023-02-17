
Installing wordpress on a server is not a difficult task, right?, you only need to install the required packages,then downloading and configuring the wordpress files and database

But what if you need to install wordpress on more than one server, let's say 20 servers, it is a hectic task. But using ansible you can done the whole process in a single command.

Here we are creating a playbook to configure wordpress on remote servers using ansible.

Ansible is the simplest way to automate apps and IT infrastructure.

So let's start. Before proceeding further you have to make sure that you have installed ansible on your machine and you have created the inventory files with the details of the remote server.
You also need to copy the keypairs of the remote machines to the host machine,

In this example, we are deploying our application in amaon-linux 
Following are the steps 

# 1. installing ansible
======================

You can install ansible using amazon-linux-extras
```
$ sudo amazon-linux-extras install ansible2 -y
```
Once installed, check the version to confirm the installation was successful.
```
[ec2-user@ip-172-31-44-159 ~]$ ansible --version
ansible 2.9.23
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/ec2-user/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.18 (default, May 25 2022, 14:30:51) [GCC 7.3.1 20180712 (Red Hat 7.3.1-15)]
```
In the next step you need to copy the key file to the hostmachine and make sure to change the permission to 400.

Once it is done, we can create the inventory file, which contains the details of the remote servers, which includes, their IP, keyfile, username, ssh port etc.

You can group the servers as per your requirement.

In our example, we are passing the required fileds such as mysql root password, wordpress db name, user etc, so that if you need to update these values, you only need to update the variables.yml file.
also ,we are copying the files such as wp-config.php, virtual host files from the hostmachine using the template module.

While running the playbook it will complte the following tasks/operations.

- Installation of apache on the remote machines
- PHP installation
- Copying of httpd-config file (we are passing the httpd port as a variable)
- Creation of document root
- Creation of sample pages (to make sure apache&php installed successfully)
- MySQL installation
- Service restart
- Updating root password & removing anonymous users
- Creating db and setting up permissions
- Configuring wordpress

Once you have created the playbook, we can check for any syntax errors, in this example our playbook is named as "wordpress-playbook.yml"

Use the following command to check for syntax errors in playbook.
```
 $ansible-playbook -i inventory.txt wordpress-playbook.yml --syntax-check
playbook: wordpress-playbook.yml
```
You will get the following output if your code passed the syntax error.

Now we can run our playbook using the following command.
```
 $ansible-playbook -i inventory.txt wordpress-playbook.yml
```
You will get the output as following, also you can check the progress of task execution.

Once the execution is completed, will be able to access wordpress from browser by using the public DNS and you can proceed with setting up wordpress.

![wordpress](https://user-images.githubusercontent.com/61390678/219599397-f4cead59-b597-471a-b17e-212cac3609d9.png)


Please have a check and let me know the suggessions :).




