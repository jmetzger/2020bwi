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
