# Docker-compose traefik

Here is the base of my configuration for traefik proxy on my Synology Network Area Storage (NAS). I removed my personal information from the files so everyone can take a look.

As I just told you, I'm using a synology NAS and I wanted to expose the DSM User interface. So you will find the configuration to do so under *data/etc/config/app-syno-dsm.yml*

I'm also using pihole and I exposed the admin interface over my network with my ssl certificate. Using a middleware with local IP whitelisting. You will find the configuration to do so under *data/etc/config/app-pihole.yml*

## What can be changed

You may want to change the network name,  I called it *proxy* but you it's just a name. I could have used *tatooine* too but **I hate sand !**

The URL to access your proxy should be changed too ! except if you own the domain *my-domain.tld*... and have a subdomain named *sub* but that's likely not the case so change it to your own domain.  
So every where you see *sub.mydomain.tld* you will need to replace with your domain or subdomain

You will need to create and htpassword file named **htpwd** or change the name of it in the docker-compose file. That is if you want to expose traefik dashboard to the internet witout other autentication method !

```bash
sudo apt-get update
sudo apt-get install apache2-utils
htpasswd -Bn <web_user_you_want_to_use> <password> > htpwd
scp ./htpwd <my_user>@<my_server>:/<path/traefik/docker-compose/folder>
```

My Registrar is the company OVH my configuration is meant to use it you may adapt it to your need !
I will write a complete how to but [la grotte du barbu](https://www.grottedubarbu.fr/traefik-dns-challenge-ovh/) french blog already covered it and help me understand the way to use the API.  
So if you are using OVH as your registrar you will want to create a few files under *./secrets*

- ovh_endpoint.secret
- ovh_application_key.secret
- ovh_application_secret.secret
- ovh_consumer_key.secret

You may want to change the email address in *data/etc/traefik.yml* And to first use the commanted *caServer* line to see if you are all set to get your certificate.

## sources

- Most of my configuration was adapted from :
[Technotim](https://github.com/techno-tim/techno-tim.github.io/blob/master/reference_files/traefik-portainer-ssl/traefik/)
  
- The idea to separate create multiples files middlewares, chains and app came from :
[htpcBeginner](https://github.com/htpcBeginner/docker-traefik)

- How to use OVH API for traefik DNS challenge (in French)
[la grotte du barbu](https://www.grottedubarbu.fr/traefik-dns-challenge-ovh/)
