Cascadeo Training Ansible Practice Project
-----------------------------------------------------------------------------

- Tested with Ansible 2.3
- Expects CentOS/RHEL 7 hosts
- depends on roles: see requirements.yml

This example is a three tier simple web applicatiom (i.e. LAMP) deployment. Here we'll install and configure a web server with an HAProxy load balancer in front, and deploy an application (i.e. Wordpress) to the web servers. 

### Initial Site Setup

After checking out this repo, install role dependencies by running:

        ansible-galaxy install -r requirements.yml --roles-path roles/

We configure the entire stack by listing our hosts in the 'hosts' inventory file, grouped by their purpose:

		[webservers]
		webserver1
		webserver2
		
		[databases]
		dbserver
		
		[balancers]
		lbserver

Next we replace the vault variable file group_vars/all/vault with a new file which contains vault_wordpress_db_password variable. Default password for the vault is 'password' (without the quotes)

After which we execute the following command to deploy the site:

		ansible-playbook -i hosts site.yml --ask-vault-pass

The deployment can be verified by accessing the IP address of your load balancer host in a web browser: http://<ip-of-lb>. 
