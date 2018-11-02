# Devenv
Basic example configuration for containerizing a development environment  

  
**Prerequisites**

- docker (18.02.0+)
- docker-compose


**Usage**

```
git clone https://github.com/mikengocdo/devenv.git && cd devenv
docker-compose up -d
```


**Format**

The example assumes the environment contains three containers.

- One redis instance 
- One mongodb instance (Not this is not actually used in the example)
- One frontend app

Redis and mongodb have their datastores persisted via volume mounts.


**Testing**

To test the frontend + redis integration example is working:
```
curl 127.0.0.1:5000
```


**Discussion**

Normally the frontend app would be in a separate repo, but to keep it clean it has been placed within the same repo here. The .env file would contain the path to the frontend repo, and expects a dockerfile to build. The .env file also is used to specify specific versions of each app. So if pushing tagged apps to a docker registry, these tagged versions can be specified, so they do not need to be rebuilt every time.  

Adding apps, is done with adding the repo path to .env file (This would be changed to ./env with the added requirement to copy to .env, and adding it to .gitignore) allowing developers to bring up only apps they need. This would allow developers to build with other components tagged versions or from master/development branches, all locally and test changes before tagging and deploying to stages, and provides a standised set of components and linked libraries used when building. 

It was initally planned to use ansible to inject configs to apps with jinja2 templates and group vars for different stages, but I didn't use an app with a configuration file, so this part was skipped for now. 
