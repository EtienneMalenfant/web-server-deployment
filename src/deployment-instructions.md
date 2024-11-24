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
![apache default page screenshot](../assets/apache-default.png)

##### Customise website

You can now import your website in the `/var/www/` directory.
Example importing from github
```
cd /var/www
git clone git@github.com/MyUsername/MyRepo.git
```
###### Updating the directory

Edit the config file for your website directoy with 
`sudo nano /etc/apache2/sites-available/000-default.conf`
Locate the line `DocumentRoot /var/www/html`, and update the directory. (example: `/var/www/my-website-dir`)

#### Configure a domain name for your website

1. Buy a domain name (I use namecheap)
2. In you domain name provider website
   1. Manage your domain name
   2. Link your domain to your server's ip adress
   3. Enter your domain in a web browser, you should see your website

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

#### HTTPS
> Provide encrypted connection to our website

We'll be using certbot to create our certificate

Install certbot
```
sudo apt install certbot python3-certbot-apache
```

###### Generate the SSL certificate
```
sudo certbot --apache
```

Answer the questions
1. Provide email adress
2. Anwser yes to term of service
3. Yes/no to sharing your email
   
Check for sucess and reload your website, your url should look like this: `https://mywebsite.com` 