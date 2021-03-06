# MariaDB Galera Cluster Training Berlin 

## Documentation for training 
http://schulung.t3isp.de/documents/pdfs/mariadb/mariadb-galera-cluster.pdf

## Download for mysql - server with wsrep extension 
https://galeracluster.com/downloads/#downloads

## Necessary packages for manual installation 
```
MariaDB-client           x86_64  10.3.21-1.el7.centos           mariadb   11 M
MariaDB-compat           x86_64  10.3.21-1.el7.centos           mariadb  2.8 M
MariaDB-server           x86_64  10.3.21-1.el7.centos           mariadb   24 M
MariaDB-common           x86_64  10.3.21-1.el7.centos           mariadb   81 k
galera                   x86_64  25.3.28-1.rhel7.el7.centos     mariadb  8.0 M

They can be found here:
http://mariadb.mirror.iweb.com//mariadb-10.3.21/yum/centos7-amd64/rpms/
```
## Block firewall to simulate non-primary (drop out of cluster) 
```
for i in 3306 4567 4568 4444; do iptables -A INPUT -p tcp --destination-port $i -j DROP; iptables -A OUTPUT -p tcp --destination-port $i -j DROP; done
iptables -L 
```

## Metrics Performance 
https://severalnines.com/database-blog/monitoring-galera-cluster-mysql-or-mariadb-understanding-metrics-updated

## MaxScale 
https://mariadb.com/projects-using-bsl-11/

## Download MaxScale binary 
https://mariadb.com/downloads/#mariadb_platform-mariadb_maxscale

## MaxScale 

### Monitor (Health Checks) for Galera 

parameters for all monitors:
https://mariadb.com/kb/en/mariadb-maxscale-24-common-monitor-parameters/
specifically galera:
https://mariadb.com/kb/en/mariadb-maxscale-24-galera-monitor/
best option is to use cli with socket not with port 
https://mariadb.com/kb/en/mariadb-maxscale-24-cli/
```
[CLI-Unix-Listener]
type=listener
service=CLI
protocol=maxscaled
socket=default
```

### MaxScale - set / clear server for maintenance 

set server galera3 maintenance
clear server galera3 maintenance

### Connect through maxscale to cluster 
mysql -uroot -p -h 127.0.0.1 -P 3307

### Create user on galera - node 
```
CREATE USER 'training'@'%' IDENTIFIED BY 'password';

```

## Sudo list ## 

```
lsof -i 
top 
sestatus 
pkill -9 mysqld 
yum autoremove MariaDB-* 
yum install maxscale 
# journalctl -u mariadb 
# systemctl start mariadb 
# systemctl stop mariadb 
# systemctl status mariadb 
ä systemctl start maxscale 
# systemctl stop maxscale 
# systemctl status maxscale 


iptables -L 

# evtl.
galera_new_cluster 
```

``` 
