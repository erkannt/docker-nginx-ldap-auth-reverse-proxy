# Reverse proxy with LDAP auth using Docker compose

The goal is to have one container provide LDAP authentication for access to the content served by another container.

## Usage

Bring up LDAP, phpldapadmin, auth-proxy and example-page with compose:

    docker-compose up -d

Go to `localhost:8080` in your browser and log in to phpldapadmin with:

    cn=admin,dc=example,dc=com
    secret

Import the `sample.ldif` from this repo. Now when you visit `localhost` the user `alice, pw:secret` should get you to the basic nginx page but `bob, pw:secret` shouldn't have access since he isn't in the `admin` group.

## Configuration

To configure access rights, edit `nginx-ldap-auth-proxy.conf` to your liking. The options are explained the [original example config](https://github.com/kvspb/nginx-auth-ldap/blob/master/example.conf) of the nginx module.

## Credits

 - __Henrik Sachse__ [nginx-ldap image](https://github.com/g17/nginx-ldap/)
 - __Valery Komarov__ [nginx ldap auth module](https://github.com/kvspb/nginx-auth-ldap)
 - __dinkel__ [openldap](https://github.com/dinkel/docker-openldap) and [phpldapadmin](https://github.com/dinkel/docker-phpldapadmin) images
