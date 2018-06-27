# Inventory 

Common file: `../ansible/hosts`

## Example 1 - Server list:

```
server1.stackbuilders.net
server2.stackbuilders.net
server3.stackbuilders.net
server4.stackbuilders.net
```
## Example 2 - Set an alias to each server:

```
web1 ansible_host=server1.stackbuilders.net 
web2 ansible_host=server2.stackbuilders.net
web3 ansible_host=server3.stackbuilders.net
db1  ansible_host=server4.stackbuilders.net
```

## Example 3 - Define connection type, user and password

List of hosts:


| Alias | Host | Connection | User | Password |
|:-----:|:-------------------------:|:----------:|:----:|:---------:|
| web1 | server1.stackbuilders.net | ssh | root | P45sw0rd! |
| web2 | server2.stackbuilders.net | ssh | root | P45sw0rd! |
| web3 | server3.stackbuilders.net | ssh | root | P45sw0rd! |
| db1 | server4.stackbuilders.net | Windows | root | P45sw0rd! |

The default connection type in Linux is `ssh`, meanwhile for Windows
the default connection is `winrm` 

```
# Web Servers
web1 ansible_host=server1.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_ssh_pass=P45sw0rd!
web2 ansible_host=server2.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_ssh_pass=P45sw0rd!
web3 ansible_host=server3.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_ssh_pass=P45sw0rd!

# Database Servers
db1 ansible_host=server4.stackbuilders.net ansible_connection=winrm ansible_user=administrator ansible_password=P45sw0rd!
```

## Example 4 - Creation of server groups

```
# Web Servers
web1 ansible_host=server1.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_ssh_pass=P45sw0rd!
web2 ansible_host=server2.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_ssh_pass=P45sw0rd!
web3 ansible_host=server3.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_ssh_pass=P45sw0rd!

# Database Servers
db1 ansible_host=server4.stackbuilders.net ansible_connection=winrm ansible_user=administrator ansible_password=P45sw0rd!

[web_servers]
web1
web2
web3

[db_servers]
db1
```
## Example 5 - Creation of group of groups

```
# Web Servers
web1 ansible_host=server1.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_ssh_pass=P45sw0rd!
web2 ansible_host=server2.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_ssh_pass=P45sw0rd!
web3 ansible_host=server3.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_ssh_pass=P45sw0rd!

# Database Servers
db1 ansible_host=server4.stackbuilders.net ansible_connection=winrm ansible_user=administrator ansible_password=P45sw0rd!

[web_servers]
web1
web2
web3

[db_servers]
db1

[all_servers:children]
web_servers
db_servers
```

## Example 6 - Example of a complete hostfile

List of hosts:

| Alias | Host | OS | User | Password |
|:---------:|:-------------------------:|:---------:|:---------------:|:-----------:|
| sql_db1 | sql01.stackbuilders.net | Linux | root | P45sw0rd! |
| sql_db2 | sql02.stackbuilders.net | Windows | administrator | P45sw0rd! |
| web_node1 | web01.stackbuilders.net | Linux | root | P45sw0rd! |
| web_node2 | web02.stackbuilders.net | Linux | root | P45sw0rd! |
| web_node3 | web03.stackbuilders.net | Windows | administrator | P45sw0rd! |

List of groups:

| Group | Members |
|:---------------:|:---------------------------------:|
| db_nodes | sql_db1 - sql_db2 |
| web_nodes | web_node1 - web_node2 - web_node3 |
| quito_nodes | sql_db1 - web_node1 |
| rochester_nodes | sql_db2 - web_node2 - web_node3 |
| sb_nodes | quito_nodes, rochester_nodes |

```
# Web Servers
 web_node1 ansible_host=web01.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_password=P45sw0rd!
 web_node2 ansible_host=web02.stackbuilders.net ansible_connection=shh ansible_user=root ansible_password=P45sw0rd!
 web_node3 ansible_host=web03.stackbuilders.net ansible_connection=winrm ansible_user=administrator ansible_password=P45sw0rd!

# DB Servers
  sql_db1 ansible_host=sql01.stackbuilders.net ansible_connection=ssh ansible_user=root ansible_ssh_pass=P45sw0rd!
  sql_db2 ansible_host=sql02.stackbuilders.net ansible_connection=winrm ansible_user=root ansible_ssh_pass=P45sw0rd!

# Groups
[db_nodes]
 sql_db1
 sql_db2

[web_nodes]
 web_node1
 web_node2
 web_node3

[quito_nodes]
 sql_db1
 web_node1

[rochester_nodes]
 sql_db2
 web_node2
 web_node3

[sb_nodes:children]
 quito_nodes
 rochester_nodes

```























