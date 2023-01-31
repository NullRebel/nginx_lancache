# Nginx LanCache

On premises caching for multiple bandwidth-heavy services.

## Overview

The Nginx Lancache is an on premise caching solution initially designed for schools, but its application can be used anywhere.

## Fork

This fork is currently running in an educational environment and will receive updates that may reflect that. 

## Supported Zones

Microsoft Zones:

       download.windowsupdate.com
       
       *.download.windowsupdate.com
       
       tlu.dl.delivery.mp.microsoft.com
       
       *.tlu.dl.delivery.mp.microsoft.com
       
       officecdn.microsoft.com
       
       officecdn.microsoft.com.edgesuite.net

Google Chrome/ChromeOS Zones:

       dl.google.com
       
       *.gvt1.com

Adobe Zones:

       ardownload.adobe.com, agsupdate.adobe.com, ccmdl.adobe.com
       

APT (Please add to the list and submit a pull request if you find one missing.) 

      *.ubuntu.com
      
      *.debian.org

      ppa.launchpad.net, *.ppa.launchpad.net

      repo.steampowered.com, *.repo.steampowered.com


	   

* All zone's need a base '@' A record and a wildcard * record pointing to your on premises cache.

## Implementation using Local DNS

This method is for sites with a pre-existing onsite DNS server.

1. Create a linux VM and install nginx as well as the nginx stream module
2. Install the nginx.conf and the services directory into /etc/nginx/
3. On your local DNS server, install the zones listed in the Supported Zones section and point them towards your cache server


## Design

Cache only caches HTTP content, and specifically only content that is explicitly set to cached. HTTPS content is passed through automatically using SNI.
It is important to note that you can technically send any traffic through the proxy but that will obviously cause some performance issues.

For example, you could send *.adobe.com through the server, but it would only cache ardownload.adobe.com, ccmdl.adobe.com, and agsupdate.adobe.com and pass through the HTTPS and HTTP traffic for www.adobe.com without performing any caching. 

You really should try to be as specific as possible.


## Supported Zones

### Microsoft:
- download.windowsupdate.com
- *.download.windowsupdate.com
- tlu.dl.delivery.mp.microsoft.com
- *.tlu.dl.delivery.mp.microsoft.com
- officecdn.microsoft.com
- officecdn.microsoft.com.edgesuite.net

### Google Chrome/ChromeOS Zones:
- dl.google.com
- *.gvt1.com

### APT [Ubuntu]
- archive.ubuntu.com
- *.archive.ubuntu.com

### Adobe Zones:
- ardownload.adobe.com
- ccmdl.adobe.com
- agsupdate.adobe.com
