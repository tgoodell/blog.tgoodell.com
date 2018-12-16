# Hosting Multiple Websites on One Server

_Tristan Goodell on Tutorial, Project, Apache Virtual Hosts, Digital Ocean, Website | 28 Sep 2018_

I have had an issue that I have been trying to tackle since I started to get into Web Design and Development: the cost of hosting.

I use Digital Ocean to host https://tristangoodell.com. I have really liked using Digital Ocean thus far and I wanted to continue to use them. Only issue is that they do not natively support the hosting of multiple websites on one droplet.

I have a total of nine domains at the time of me writing this. $5 a month for a single server is fairly affordable. $5 x 9 is $45. While that is manageable, it gets pretty expensive pretty quickly. Hosting a single website per server can not only get expensive fast, but there is also an issue of manageability. I knew that there had to be a better way.

---

After doing a couple of hours of research, I concluded that [Apache Virtual Hosts](https://httpd.apache.org/docs/2.4/vhosts/) were the way to go.

I ran into two major roadblocks: the documentation on how to set up Apache Virtual Hosts was subpar at best, if not outdated, and Cloudflare did not want to cooperate.

---

## Setup

I wanted to try this out with three websites at first:

- https://meecso.com
- https://tgoodell.com
- https://appin.space

Simply replace my domain names with yours for this exercise.

SSH into your droplet.

This will make the directory `public_htm`l in `/var/www/yoursite.com/`. The files for the corresponding website will be in `public_html`.

`sudo mkdir -p /var/www/meecso.com/public_html`

`sudo mkdir -p /var/www/tgoodell.com/public_html`

`sudo mkdir -p /var/www/appin.space/public_html`

This will ensure that the directories that we just made will have the correct permissions for us to continue to prepare the Apache Virtual Hosts.

`sudo chown -R $USER:root /var/www/meecso.com/public_html`

`sudo chown -R $USER:root /var/www/tgoodell.com/public_html`

`sudo chown -R $USER:root /var/www/appin.space/public_html`

`sudo chmod -R 755 /var/www`

Next, we need to modify the index.html file within one of the directories.

`nano /var/www/meecso.com/public_html/index.html`

Use some basic HTML to validate that you are in fact viewing the right files for your website. Something like this will do:

```
<HTML>

<head>

<h1>Success!</h1>

</head>

<body>

<p>You are now viewing meecso.com!</p>

</body>

</html>
```

Replace `meecso.com` with your domain. We need to do the same with the other domains, so you can simply copy the `index.html` file that we just worked on to the new directory.

`cp /var/www/meecso.com/public_html/index.html /var/www/tgoodell.com/public_html/index.html`

Make sure to nano the new index.html file and modify the domain name to ensure that we can validate the website later on.

`nano /var/www/tgoodell.com/public_html/index.html`

Next, we need to copy the current .conf file for the default web host location to the new ones.

`sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/meecso.com.conf`

Nano in to modify the necessary areas.

`sudo nano /etc/apache2/sites-available/meecso.com.conf`

Webmaster email.

`ServerAdmin contact@tristangoodell.com`

The directory where the files of the website is located.

`DocumentRoot /var/www/meecso.com/public_html`

The domain names with any necessary subdomains.

`ServerName meecso.com`

`ServerAlias meecso.com`

The directory where files are located.

`<Directory /var/www/meecso.com/public_html>`

Copy the .conf file that we just worked on to the other locations.

`sudo cp /etc/apache2/sites-available/meecso.com.conf /etc/apache2/sites-available/tgoodell.com.conf`

Modify the necessary entries.

`sudo nano /etc/apache2/sites-available/tgoodell.com.conf`

Finally, we need to enable and disable some directories.

Enable our first website.

`sudo a2ensite meecso.com.conf`

Enable our second website.

`sudo a2ensite tgoodell.com.conf`

Disable the default directory.

`sudo a2dissite 000-default.conf`

Restart apache.

`sudo systemctl restart apache2`

Voila! Test out your websites to ensure that everything is working perfectly. If it isn't feel free to let me know in the comments below.

Make sure that Digital Ocean is pointing to your domain and that your domain's DNS settings are properly configured.
Pushing Out Updates

A website isn't very useful if it does not have any content. The best way to push updates that I have found is by uploading files to Github and then cloning them to the server.

Navigate to the proper directory.  

`cd /var/www/meecso.com`

Make sure that there is a public_html.

`ls`

Remove public_html.

`rm -rf public_html`

Clone the Github repo into a new public_html.

`git clone https://github.com/tgoodell/meecso.com public_html`

Theoretically, you should be able to host Ghost and Wordpress websites using Apache Virtual Hosts as well, although I have not tried this yet.
