# WordPress on Nginx + php-fpm with PerconaDB as database

## Requires
- Ansible 1.9.4 or newer
- Vagrant 1.8.1 or newer
- VirtualBox 5.0.3 or newer

All Nodes use Centos7, Ubuntu/Debian and other doesn't supported.

## Settings
This Vagrant file use IP addresses by default:
- 192.168.10.2 - haproxy as loadbalancer Webservers and failover for DataBases
- 192.168.10.3 - PerconaDB as Master database
- 192.168.10.4 - PerconaDB as Slave database
- 192.168.10.5 - Nginx + php-fpm as Webserver 1
- 192.168.10.6 - Nginx + php-fpm as Webserver 2

You can change all settings in:
- servers.yml
- vars/all.yml

## Usage
Clone this repo, run vagrant:  
`$ git clone https://github.com/Extor/nginx-wp-cluster-test.git `  
`$ cd nginx-wp-cluster-test && vagrant up`  
`$ firefox localhost:8037`  

Please start master-slave replication manually.

## ToDo
1. Use one file for create VM and Ansible configuration.
2. More setting for nginx, perconadb and haproxy in setting file
