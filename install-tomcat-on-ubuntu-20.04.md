# Install Tomcat 9 on Ubuntu 20.04 <br/><br/>

### Step 1. Install Java

### Step 2. Create Tomcat User

- For security purposes, Tomcat should be run as an unprivileged user (i.e. not root). 
We will create a new user and group that will run the Tomcat service.

- First, create a new `web-server-group` group:

```bash
sudo groupadd web-server-group
```

- Next, create a new tomcat user. We’ll make this user a member of the `web-server-group` group, 
with a home directory of /opt/tomcat (where we will install Tomcat), and with a shell of /bin/false 
(so nobody can log into the account):

```bash
sudo useradd -s /bin/false -g web-server-group -d /opt/tomcat tomcat
```

### Step 3. Install Tomcat

<br/>
<br/>

### References

https://www.digitalocean.com/community/tutorials/install-tomcat-9-ubuntu-1804