## **Documentation for Project 10**

### Updating etc Hostfile

![etc-hostfile-update](./Images/etc-hostFile-updated-for-local-DNS-resolution.png)

### Configuring Nginx as Load Balancer
`sudo apt update`
`sudo apt install nginx`

![Nginx-Installation](./Images/nginx-installation.png)

### Ensuring nginx is up and running
`sudo systemctl restart nginx`
`sudo systemctl status nginx`

![Nginx-status](./Images/making-sure-nginx-is-running.png)

## **Configuring Route 53**

### creating hosted zone

![Hosted-Zone-Creation](./Images/Route53-hosted-Zone-successfully-created.png)
### Name server Configuration

![Nameserver-Config](./Images/Name-server-config.png)

### Creating a record in Route 53 pointing to the Ip-address of our Load Balancer

![Route-53-record-for-Load-balancer](./Images/new-record-created-in-our-load-balancer-with-its-public-Ip-address.png)

### New Route 53 Record with wwww also pointing to Route 53

![New-Route-53-record-with-www-for-Load-balancer](./Images/new-record-with-www-created-pointing-to-Nginx-LB-address.png)

### Configuring NginxLB with Webserver Names defined in etc Hostfile

`sudo vi /etc/nginx/sites-available/load_balancer.conf`
![nginxLB-config-with-webserver-names-defined-in-ect-hostfiles](./Images/configuring-nginx-LB-with-Webserver-names-defined-in-etc-host.png)

### Removing default site to allow reverse proxy to redirect to our new config file and testing to ensure our Nginx config is okay

`sudo rm -f /etc/nginx/sites-enabled/default`

`sudo nginx -t`
![removing-default-site-to-allow-new-config-file-run-and-testing-our-nginx-config](./Images/removing-default-site-to-allow-new-config-file-run-and-testing-our-nginx-config.png)

### Linking our LB config file in site-available to site-enables to allow Nginx access our Config

`sudo ln -s ../sites-available/load_balancer.conf .`
![linking-LB-config-file-in-site-available-to-site-enabled](./Images/linking-LB-config-file-in-site-available-to-site-enabled.png)

### Accessing our newly registered Domian from URL

`http://toolingibk.site/`
![Accessing-our-web-server-using-newly-registered-domain](./Images/Accessing-our-web-server-using-newly-registered-domain.png)

## Securing our Domain

### Installing Certbot and its dependencies
`sudo apt install certbot -y`

`sudo apt install python3-certbot-nginx -y`
![Installing-certbot-and-its-dependencies](./Images/Installing-certbot-and-its-dependencies.png)

### Creating a certificate for our Domain to make it secure
`sudo certbot --nginx -d toolingibk.site -d www.toolingibk.site`

![creating-certificate-to-secure-our-domain](./Images/creating-certificate-to-secure-our-domain.png)

![creating-certificate-to-secure-our-domain-Continued](./Images/creating-certificate-to-secure-our-domain-contd.png)

### Domain is secured 

![Domain-is-secure](./Images/Domain-is-secure.png)

### Creating a Crontab Job to automatically or periodically renew our certificate
`crontab -e`

![Crontab-job-to-periodically-renew-cert](./Images/Crontab-job-to-periodically-renew-cert.png)

![Crontab-job-to-auto-renew-certificate](./Images/Crontab-job-to-auto-renew-certificate.png)
