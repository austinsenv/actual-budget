[Actual Budget](https://actualbudget.com/) is a great way to manage your finances. It is free to use and [open source](https://github.com/actualbudget/actual). When you self host Actual, you get the benefits of the security and privacy of your sensitive financial information. 

---
## Setup Instructions

After cloning the repository, make a new directory called `actual-data`. This directory will be mounted to the container and is where Actual will store its data. 

The docker compose configuration provided in this repository assumes you are going to connect to Actual from outside of the local host. If this is the case, you'll need to create a `selfhost.crt` and `selfhost.key` for enabling HTTPS (see below). If you are going to access Actual from localhost, those lines in the 'environment' section of `docker-compose.yml` will need to be removed. 
#### Setting up your self signed certificate to enable HTTPS
Creating a self signed certificate can be pretty complex, and there are several ways to do so. This way utilizes the [openssl](https://packages.debian.org/bookworm/openssl) package normally installed on Linux distributions. 

The following command will generate a SSL self signed certificate.
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout selfhost.key -out selfhost.crt
```
The files `selfhost.key` and `selfhost.crt` will be generated and added to the current working directory. Make sure these files are in the `actual-data` directory you created or change the path to the files in `docker-compose.yml`.

#### Starting Actual 
You can use `bash start.sh` to start the compose stack. Actual will be reachable at `https://<serverip>:5006`. Your browser won't recognize the self-signed certificate, so you'll need to choose to proceed with the connection. 
