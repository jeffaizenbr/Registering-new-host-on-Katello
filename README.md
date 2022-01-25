# Registering-new-host-on-Katello

## Edit  /etc/hosts .
```bash
vim /etc/hosts
```

```bash
10.33.245.107 katello katello.allin.com.br
OR
177.153.231.135 katello katello.allin.com.br
```
## Download the certificate
```bash
curl --insecure --output katello-ca-consumer-latest.noarch.rpm https://katello.allin.com.br/pub/katello-ca-consumer-latest.noarch.rpm ; yum localinstall -y katello-ca-consumer-latest.noarch.rpm
```
## Register the machine
```bash
subscription-manager --force register --org="Allin" --activationkey="CentOS_7_Non_Prod_Key"
```
## Install dependencies 
```bash
yum install -y https://yum.theforeman.org/client/1.23/el7/x86_64/foreman-client-release-1.23.1-1.el7.noarch.rpm ; yum install -y katello-host-tools katello-host-tools-tracer katello-agent
```
## Start agent and verify status
```bash
systemctl restart goferd ; katello-package-upload -f ; systemctl restart rhsmcertd
```
