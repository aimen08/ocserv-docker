# ocserv-docker
VPN server (ocserv) on docker

VPN server (ocserv) is an Open Source SSL VPN server.


## Installtion

**It is launched with the following settings**

- 2 Device connections for each user (`max-same-clients=2`)
- Up to 32 clients (`max-clients=32`)
- `10.10.10.0/24` as the internal IP pool
- Listens on port `5443`
- Tunnels DNS to the server



## Edit docker-compse.yml & Run
1- copy `docker-compose.yml` in your Server or clone project

2- Replace the `<IP>` variable in docker-compse.yml with appropriate value.

3- Run `docker-compose up -d`.


# Usage

## User Managment
### Create User

```bash
docker exec -it ocserv ash -c "ocuser create <username>"
```

### Delete a User

```bash
docker exec ocserv ash -c "ocuser delete <username>"
```
### Lock a User

```bash
docker exec ocserv ash -c "ocuser lock <username>"
```
### Unlock a User

```bash
docker exec ocserv ash -c "ocuser unlock <username>"
```

### list of User 
view `ocpasswd` file

```
docker exec ocserv cat /etc/ocserv/data/ocpasswd
```


## Using Client

- [Android (OpenConnect)](https://apkcombo.com/openconnect/com.github.digitalsoftwaresolutions.openconnect/download/apk)
- [iOS](https://apps.apple.com/us/app/cisco-anyconnect/id1135064690)
- [MacOS](https://its.gmu.edu/wp-content/uploads/anyconnect-macos-4.10.07073-core-vpn-webdeploy-k9.zip)
- [Windows](https://www.firewall.cx/downloads/cisco-tools-a-applications/cisco-anyconnect-secure-mobility-client-v4-9-0195.html)
- [Ubuntu](https://www.firewall.cx/downloads/cisco-tools-a-applications/cisco-anyconnect-secure-mobility-client-v4-9-0195.html)


### Not connecting in some clients
if you having problem with android or ios client , make sure to force connecting through TLS1.2 only
go inside container and run 

```
sudo nano /etc/ocserv/ocserv.conf
```
look for this line 

```
tls-priorities = "NORMAL:%SERVER_PRECEDENCE:%COMPAT:-RSA:-VERS-SSL3.0:-ARCFOUR-128"
```
add this to it -VERS-TLS1.3 so it becomes

```
tls-priorities = "NORMAL:%SERVER_PRECEDENCE:%COMPAT:-RSA:-VERS-SSL3.0:-ARCFOUR-128:-VERS-TLS1.3"

```
done , restart now it should fallback to tls1.2 for every connection

### No need to a Valid SSL
 the script will generate a self-signed certificate for you inside the container. so ignore the warning you will get ***warning message about the certificate not being trusted*** when logging in.

