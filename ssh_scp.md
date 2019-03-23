# SSH and SCP related
## ssh/scp via a proxy
We have to make use of `ProxyCommand`

### Method 1 (Preferred for long term usage)
In ~/.ssh/config
```
Host proxy
  Hostname proxy.tld
  User proxy_user
Host target
  Hostname target.tld
  User target_user
  ProxyCommand ssh -W %h:%p proxy
```
Source: https://unix.stackexchange.com/a/296217/247675

### Method 2 (For short term usage)
With IdentityFile
```
scp -i user2-cert.pem -o ProxyCommand="ssh -i user1-cert.pem -W %h:%p user1@server1" user2@server2:/<remotePath> <localpath>
```
With password authentication
```
scp -o ProxyCommand="ssh -W %h:%p user1@server1" user2@server2:/<remotePath> <localpath>
```
With password authentication and same credentials on both servers
```
scp -o ProxyCommand="ssh -W %h:%p commonuser@server1" commonuser@server2:/<remotePath> <localpath>
```



