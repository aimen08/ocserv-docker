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
- [MacOS](https://www.cisco.com/c/en/us/support/docs/smb/routers/cisco-rv-series-small-business-routers/smb5642-install-cisco-anyconnect-secure-mobility-client-on-a-mac-com-rev1.html)
- [Windows](https://www.cisco.com/c/en/us/support/docs/smb/routers/cisco-rv-series-small-business-routers/smb5686-install-cisco-anyconnect-secure-mobility-client-on-a-windows.html)
- [Ubuntu](https://www.cisco.com/c/en/us/support/docs/smb/routers/cisco-rv-series-small-business-routers/Kmgmt-785-AnyConnect-Linux-Ubuntu.html)




### Not Valid SSL

If you can't create one ( ports 80 and 443 are not available on your server, or you don't have a domain), a fallback script will generate a self-signed certificate for you inside the container. The only difference is a ***warning message about the certificate not being trusted*** when logging in.


# References

- [cisco-anyconnect-server-docker](https://github.com/soreana/cisco-anyconnect-server-docker)
- [TommyLau/docker-ocserv](https://github.com/TommyLau/docker-ocserv)
