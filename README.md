# private-docker-registry
Create your own private docker registry with ssl by letsencrypt and basic auth

Official docs: [https://docs.docker.com/registry/deploying/](https://docs.docker.com/registry/deploying/)

## Config it

Before you can start registry service, you should make a little setup: config your **domain**, create **htpasswd** for auth

### Domain name

Open `docker-compose.yml` and replace `<your_domain>` and  `<your_email>` to your domain name and email.

### Create a password file

```
mkdir auth
docker run --entrypoint htpasswd registry:2 -Bbn testuser testpassword > auth/htpasswd
```

**Note:** do not use default login \ pass form example!

## Up it

Just up service:
```
docker-compose up
```

This configuration will get security cert automatically by [lets-nginx](https://github.com/smashwilson/lets-nginx). 
It may take a bit of time. 

## Use it

Now you can login and try to upload some image into your private docker registry:
```
docker pull alpine
docker tag alpine <your_domain>:5000/alpine
docker login <your_domain>:5000

    Username: testuser
    Password: testpassword
    Login Succeeded

docker push <your_domain>:5000/alpine
```

## Contributing

Bug reports, bug fixes, and new features are always welcome. Please open issues, and submit pull requests for any new code.