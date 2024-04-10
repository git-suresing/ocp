 
# Switch to Root User ###########

sudo -i

# Install Docker ######
```
sudo yum -y install docker

systemctl enable docker

cat << EOF >/etc/docker/daemon.json
{
 "insecure-registries": [
 "172.30.0.0/16"
 ]
}
EOF

systemctl start docker
```
## Add Rule in firewall ####

```
firewall-cmd --permanent --new-zone dockerc
firewall-cmd --permanent --zone dockerc --add-source 172.17.0.0/16
firewall-cmd --permanent --zone dockerc --add-port 8443/tcp
firewall-cmd --permanent --zone dockerc --add-port 53/udp
firewall-cmd --permanent --zone dockerc --add-port 8053/udp
firewall-cmd --permanent --zone public --add-port 8443/tcp
firewall-cmd --reload

yum -y install centos-release-openshift-origin39
yum -y install origin-clients

```

# Install the Cluster ########

oc cluster up --version=v3.9.0 --public-hostname=172.28.234.5


###### 172.28.234.5 is publick IP of VM where we installing kubernet ####