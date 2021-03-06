# ![PyDDNS](https://i.imgur.com/kOrgTBW.png)
Complete system to create your own dynamic DNS server.

Based on the <b>dprandzioch</b> project: https://github.com/dprandzioch/docker-ddns


## Description
PyDDNs is a complete solution, allows you to set up and manage their own dns, compatible with the dyndns2 protocol, the user can update his ip by web interface or using a compatible client for example ddclient.
<br><br><br>

### Screenshots
![screenshots](https://i.imgur.com/6HTwrfn.png)

<br><br><br>
**VIDEO**: https://www.youtube.com/watch?v=ALN9901EoyA&feature=youtu.be
<br><br><br>


### Prerequisites
Install git
Install docker - Dockerhttps://docs.docker.com/install/
Install docker-composer - https://docs.docker.com/compose/install/

**important**: if you use ubuntu 18 you should see the note at the end of this text
<br><br><br>
## Quick Start

**IMPORTANT**: If you are using PyDDNS v1 before updating, make a backup of the file docker-compose.yml

- Clone de proyect
- ```cd PyDDNS```
- copy the configuration file ```cp .env-demo .env```
- Edit the configuration file ```nano .env```

```
DOMAIN=ddns.demo.com  <-- our domain
SHARED_SECRET=el@sadsadyS58 <-- password for internal API-REST

DATABASE_NAME=pyddns
DATABASE_USER=pyddns
DATABASE_PASS=PyDyn@m1cDNSP0s
DATABASE_HOST=postgres
DATABASE_PORT=5432

DJANGO_SU_NAME=admin
DJANGO_SU_EMAIL=admin@company.com
DJANGO_SU_PASSWORD=1234 <-- Password to default administrator
DJANGO_DEBUG=1
DJANGO_LOG_LEVEL=INFO
DJANGO_PYTHONUNBUFFERED=1
OWN_ADMIN: 1  <-- 1 = all users can create subdomains, 0 = only the administrator can create subdomains
DNS_ALLOW_AGENT: ddclient3,ddclient <-- If you want to control by client, put their names separated by comma

WEB_PORT=80
DNS_PORT=53
```

- Install docker and docker-compose
- Start with command: `docker-compose up`
<br><br><br>
### Configuration of DNS
You need a subdomain for example: ddns.demo.com

Then you must create an **NS record** as follows:
ddns.demo.com IN NS X.X.X.X <-- SERVER PUBLIC IP (CHECK)

<br><br><br>
## Architecture
![screenshots](https://i.imgur.com/KWZzxOs.png)
<br><br><br>
## DDNS clients
You can use any client compatible with the DynDNS2 protocol.

###### For Windows
I recommend using `DynDNS Simply Client`, you can download it here: https://sourceforge.net/projects/dyndnssimplycl/
![screenshots](https://i.imgur.com/cTwjRFS.png)


###### For Linux and Mac OS X
I recommend using `ddclient`, basic configuration:
```
protocol=dyndns2
use=web, web=checkip.dyndns.com, web-skip='IP Address'
server=localhost.com
ssl=no
login=userdemo
password='userpassword'
yourdomain.ddns.demo.com
```

<br><br><br>
### Translation :us::es:
The system automatically detects the language of your browser.
If you want to add your translations you must follow the following steps:

1. Enter the container console: `docker-compose exec python bash`
2. You must execute the following command, replacing the last attribute: `python manage.py makemessages --locale es`
3. Edit the file: `appdata/pyddns/locale/XXXX/LC_MESSAGES/django.po`
4. Once the translations are finished, it must be compiled: `python manage.py compilemessages`

<br><br><br>
### NOTE
On ubuntu 18 port 53 is busy with the systemd-resolve service.
To solve this you must disable.

I'm going to also mask it so it doesn't auto start on reboot.

```
sudo systemctl disable systemd-resolved
sudo systemctl mask systemd-resolved
reboot
```
To undo what you did:
```
sudo systemctl unmask systemd-resolved
sudo systemctl enable systemd-resolved
```

### Contact :email:
https://www.linkedin.com/in/peraltaleandro/
