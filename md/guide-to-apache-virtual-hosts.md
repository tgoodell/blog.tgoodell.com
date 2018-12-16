# Guide to Apache Virtual Hosts

_Tristan Goodell on Tutorial, Apache Virtual Hosts | 18 October 2018_

Virtual Hosts are an easy and affordable way to host multiple websites on one server. This guide is a summed up version of [this project](https://blog.tristangoodell.com/hosting-multiple-websites-on-one-server/).

## Step 1 - Prerequisites
### i. Have a server.

Head over to [Digital Ocean](http://pages.news.digitalocean.com/dcn/AyKQ30vur1Nt8H30LIWxk-j5xHmafGnoECQwn1ooO75-n4tuZXTwGdYjSIr5qbK0xTcckfnLm_U1fCT4uON9bg==/Y0Vs207XI00WN0236IE03D7) or your host of choice to setup a server.

### ii. Install Apache.

SSH into your Droplet.

`ssh root@xxx.xx.xxx.xxx`

Update your droplet

`sudo apt-get update`

Next, install Apache

`sudo apt-get install apache2`

## Step 2 - Configuring Apache Virtual Hosts

Navigate to `/var/www`

`cd /var/www`

You can use the command `ls` to view any folders or files in the directory; there should only be `html` (the default web directory).

Create necessary directories for the websites that you are wanting to configure. Replace 'tristangoodell.com' and 'meecso.com' with your domains (You are not limited to just two domains).

`sudo mkdir -p /var/www/tristangoodell.com/public_html`

`sudo mkdir -p /var/www/meecso.com/public_html`

Modify Permissions:

`sudo chown -R $USER:root /var/www/tristangoodell.com/public_html`

`sudo chown -R $USER:root /var/www/meecso.com/public_html`

`sudo chmod -R 755 /var/www`

In order to test if the Virtual Hosts are working, navigate to your first domain's directory.

`cd /var/www/tristangoodell.com/public_html`

Create an index.html file.

`nano /var/www/tristangoodell.com/public_html/index.html`

Create some basic HTML with a few indicators showing that the web page is showing up for the right domain. Something like this will do:

```
<HTML>

<head>

<h1>Success!</h1>

</head>

<body>

<p>You are now viewing tristangoodell.com!</p>

</body>

</html>
```

Next, copy the `index.html` file that was just created and move it to the correct directory.

`cp /var/www/tristangoodell.com/public_html/index.html /var/www/meecso.com/public_html/index.html`

Modify the necessary areas.

`nano /var/www/meecso.com/public_html/index.html`

Next, we need to copy the current `.conf` file for the default webhost and modify them for the new domains.

`sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/tristangoodell.com.conf`

Modify the precise areas.

`sudo nano /etc/apache2/sites-available/tristangoodell.com.conf`

The end result should look similar to this:

```
<VirtualHost *:80>

ServerAdmin contact@tristangoodell.com

DocumentRoot /var/www/tristangoodell.com/public_html

ServerName tristangoodell.com

ServerAlias tristangoodell.com

<Directory /var/www/tristangoodell.com/public_html>

Options Indexes FollowSymLinks

AllowOverride All

Require all granted

</Directory>

ErrorLog ${APACHE_LOG_DIR}/error.log

CustomLog ${APACHE_LOG_DIR}/access.log combined

<IfModule mod_dir.c>

DirectoryIndex index.php index.pl index.cgi index.html index.xhtml index.htm

</IfModule>

</VirtualHost>
```

Next, copy the configuration file for your first site in preparation for your second.

`sudo cp /etc/apache2/sites-available/tristangoodell.com.conf /etc/apache2/sites-available/meecso.com.conf`

Modify the necessary information:

`sudo nano /etc/apache2/sites-available/meecso.com.conf`

Finally, we need to disable the default web server config file and activate the files that were just created.

Enable site 1:

`sudo a2ensite tristangoodell.com.conf`

Enable site 2:

`sudo a2ensite meecso.com.conf`

Disable the default web config file:

`sudo a2dissite 000-default.conf`

Restart Apache:

`sudo systemctl restart apache2`

---

Make sure to connect your web server to your DNS and your DNS to your web server. Test out your websites afterwards to ensure that everything is working as it should.

---

## Step 3 - Pushing Out Updates

A website isn't very useful if it does not have any content. The best  way to push updates that I have found is by uploading files to [Github](https://github.com/) and then cloning them to the server.

Navigate to the proper directory:

`cd /var/www/meecso.com`

Check if there is a `public_html` directory.

`ls`

If there is, remove it.

`rm -rf public_html`

Clone the Github repo into a new public_html.

`git clone https://github.com/tgoodell/meecso.com public_html`

---

Hope this helped!
