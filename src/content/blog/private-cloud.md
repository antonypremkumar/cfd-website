---
title: 'Private cloud infrastructure'
description: 'Freedom from onedrive'
pubDate: 'Mar 28 2026'
heroImage: '../../assets/blog-placeholder-2.jpg'
---

I would like to document here all the hurdles I faced and how I overcame them while setting up `next cloud`

## Schematic

I took my old HP r007tx and installed proxmox.
I did this when I was travelling in a train and realized that I need internet access to a local router.
Immediately, I ordered a ethernet cable from Amazon.
Two days later, after getting the cable and when I was home I learned that I actually could have chosen to install wifi drivers and could have proceeded.

## Nextcloud

I used this [community script](https://community-scripts.org/scripts/nextcloud-vm?from=scripts&fromQ=nextcloud) to install turnkey nextcloud

## Hurdle 1: not able to log in

After installation, nextcloud was not letting me to log in from another laptop in the same network through the browser.
So, I manually added the IP of my laptop to its list of trusted domains just as chatGPT told me to.
This is found in the file `/var/www/nextcloud/config/config.php `.

```
  'trusted_domains' =>
  array (
    0 => localhost,
    1 => '192.168.8.10',
  ),
```

Even this didn't work.
It was frustrating for two days.
Then I started experimenting taking unsecure steps.
I added a wild card entry `192.168.8.*`.
And it worked.


## Hurdle 2: next cloud has been tampered with

Even though the above technique worked, nexcloud webapp was complaining that it has been tampered with.
Ofcourse it was.
It was me.
After much seeking, I got the solution from my work colleague.
I had to do this using the cli.
I reinstaled everything and add my unsecure wildcard IP using the cli as follows.

```
su -s /bin/bash www-data -c "php /var/www/nextcloud/occ config:system:set trusted_domains 1 --value=192.168.8.*"
su -s /bin/bash www-data -c "php /var/www/nextcloud/occ config:system:get trusted_domains"
su -s /bin/bash www-data -c "php /var/www/nextcloud/occ integrity:check-core"
```

## Hurdle 3: had to change the ownership for some reason

WIP

## Hurdle 4: access it outside of my LAN

WIP
<!-- I thought this would be very hard and was postponding it for weeks.
Then one day, I decided to just do it.
And realized how easy it was.
All I had to do was to install tailscale on my turnkey nexcloud instance and my laptop.
And authenticate and start the service.

```
turnscale up
```

I then added the tailscale IP to the list of trusted domains. -->