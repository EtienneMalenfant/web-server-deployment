# How to deploy your own web server

### Prerequisite

- Have an ubuntu server (with sudo access)
  - Can be purchased with provider (OVH, Amazon, Azure, etc.)
  - Can be done with an old PC at home
- *(Optional)* Have a domain name

## Steps to follow

1. Initial setup and installation
   1. Apache installation
   2. Customize website
2. Secure your server
   1. UFW
   2. Fail2Ban
   3. HTTPS

### Inital setup

Firstly, enter you server in command line.

#### Apache installation
> The app that let you host a website

Install apache
```
sudo apt install apache2
```

In a web browser, enter the server ip adress. You should see this :
![apache default page screenshot](assets/apache-default.png)

You can now import your website in the `/var/www/` directory.
Example importing from github
```
cd /var/www
git clone git@github.com/MyUsername/MyRepo.git
```

---
### Securing your server

#### UFW
> A firewall used to block every port except the ones we use

Install ufw
```
sudo apt install ufw
```

Add the port 80 and 443
```
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

Activate the firewall and reboot
```
sudo ufw enable
reboot
```