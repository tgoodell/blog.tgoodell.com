# Setting Up the Blog - Wrapping Cloudflare Around a DigitalOcean Droplet

_Tristan Goodell on Project, Website, Cloudflare, Digital Ocean | 03 Aug 2018_

I have been wanting to construct a blog for quite a while; a place to document my various projects and goals with the hope that I can maybe help others reach their own goals.

I really didn't want to use WordPress for my blog. It is much too bloated and slow for my purposes. I wanted to use something that was snappy and super fast.

I considered several options: Pico CMS, Anchor CMS, or Grav CMS; however, at the end of the day, I decided to use Ghost for my blog.
[Troy Hunt](https://www.troyhunt.com/) uses Ghost Pro for his blog, and his blog is beautiful. He makes a very compelling argument for [why he went with Ghost Pro, rather than hosting it on his own](https://www.troyhunt.com/its-a-new-blog/).

I really did not want to have to pay $79 a month for [Ghost Pro](https://ghost.org/pricing/), when I could host my own with [Digital Ocean](http://pages.news.digitalocean.com/dcn/AyKQ30vur1Nt8H30LIWxk-j5xHmafGnoECQwn1ooO75-n4tuZXTwGdYjSIr5qbK0xTcckfnLm_U1fCT4uON9bg==/Y0Vs207XI00WN0236IE03D7) for only $5 a month. Furthermore, [GhostPro actually uses Digital Ocean](https://www.digitalocean.com/customers/ghost/) for their hosting.

So, I went ahead and activated a droplet with the [Ghost one-click app](https://www.digitalocean.com/products/one-click-apps/ghost/). Setup was a breeze. I went to my email, grabbed the IP address I was given, pasted it into Firefox, and was greeted with a message saying that I needed to set up my Ghost instance.

I typed in `ssh root@xxx.xxx.xxx.xxx` into my terminal, entered the password that was given to me, and then changed it to a new one. Next, I typed in several lines into my terminal to finish the backend setup process.

### SSH into your Droplet

`ssh root@xxx.xxx.xxx.xxx` where `xxx.xxx.xxx.xxx` is your Droplet's IP Address.

### Switch to user ghost-mgr

`sudo -i -u ghost-mgr`

### Go to the directory where Ghost is installed

`cd /var/www/ghost`

### Update Ghost

`ghost update`

### Configure Ghost

`ghost setup`

Follow the prompts and you'll be finished there.

---

It was now time to set up everything else. I navigated to https://xxx.xxx.xxx.xxx/ghost to begin configuring what visitors to my website would see.

I set up my administrator account with all of the right credentials and a strong password. Next, I simply skipped the invitation to invite other writers to this blog (I will be the only one writing here). The initial setup process was finished.

I now wanted to wrap [Cloudflare](https://www.cloudflare.com/) around my blog and actually connect my domain https://tristangoodell.com to my Droplet.

---

On DigitalOcean, I navigated to Networking --> Domains. I then proceeded to type in my domain tristangoodell.com into the box with the placeholder "Enter Domain" (NOTE: you cannot type in the protocol; https / http). You will be greeted with a screen that features a DNS record. You can either connect your Domain to DigitalOcean's DNS or connect your domain to Cloudflare.

I wanted my blog to be as fast as possible, so I connected my domain to Cloudflare's DNS and set up everything over there. [Here is a great guide](https://httpsiseasy.com/) by Troy Hunt that will teach you how to connect Cloudflare to your domain and configure various security features, such as HTTPS.

Once I connected my domain to Cloudflare, I needed to connect Cloudflare to my Droplet. Navigate to the `DNS` tab on your selected website.

Record Type:
`A`

Name:
`@` (Will automatically become domain, i.e tristangoodell.com)

Value:
`xxx.xxx.xxx.xxx` (Will be the IP address of your Droplet)

TTL:
`Automatic`

Finally, ensure that there is an orange cloud under "Status". This means that your website actually goes through Cloudflare's trademark caching.

> One thing though: Be extremely patient

When I did this, it took a good day and half for this to consistantly work. I kept modifying my DNS settings, which simply made the wait even longer. Your domain should be connected to your Droplet through Cloudflare after a couple of hours to a full day.

---

Well, https://tristangoodell.com is now up and running and looks quite pretty. I will be making several key changes over the coming weeks and months that I really hope improve the look and quality of the site. A couple of key features that are missing at the time of this writing are:

- Comments: comments are not operational yet, however they are planned and are a top priority.
- Newsletters: you may have noticed several places asking for your email. You are welcome to register your email, however there is no newsletter yet due to [legal reasons](https://www.ftc.gov/tips-advice/business-center/guidance/can-spam-act-compliance-guide-business). When there is a newsletter, those registered will be the first ones to receive it however.
- Other pages: I still need to finish writing the Privacy Policy and About pages for the site. Furthermore, I'd like to create a couple of unique graphics for each and every page. I want to also write up several tags and meta stuff for an improved UI.

If you have any suggestions, questions, or feedback, feel free to hit me up on Twitter or shoot an email my way.

---

Links of Interest

- [Digital Ocean](http://pages.news.digitalocean.com/dcn/AyKQ30vur1Nt8H30LIWxk-j5xHmafGnoECQwn1ooO75-n4tuZXTwGdYjSIr5qbK0xTcckfnLm_U1fCT4uON9bg==/Y0Vs207XI00WN0236IE03D7)
- [Ghost One-Click App](https://www.digitalocean.com/products/one-click-apps/ghost/)
- [Cloudflare](https://www.cloudflare.com/)
- [HTTPS is Easy Cloudflare Tutorial](https://httpsiseasy.com/)
