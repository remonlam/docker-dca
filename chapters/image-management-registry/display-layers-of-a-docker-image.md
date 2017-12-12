# Display layers of a Docker image

## Pull some example Docker images;
Before you can see any layers in a Docker image, we first need to download one ;-)<br>
NOTE: take a close look at how many layers we need to download.

### An Alpine Linux Docker image
```
$ docker pull alpine

Using default tag: latest
latest: Pulling from library/alpine
2fdfe1cd78c2: Pull complete
Digest: sha256:ccba511b1d6b5f1d83825a94f9d5b05528db456d9cf14a1ea1db892c939cda64
Status: Downloaded newer image for alpine:latest
```
Just one layer!

### And a Wordpress Docker image
NOTE: take a close look at how many layers we need to download.<br>
      This one is different!
```

$ docker pull wordpress

Using default tag: latest
latest: Pulling from library/wordpress
e7bb522d92ff: Pull complete
2580aa42d1b6: Pull complete
1a8abb84c6a3: Pull complete
7bff113cc3d6: Pull complete
dd1a4dcbc4ec: Pull complete
ab893328ce84: Pull complete
13367be12a3f: Pull complete
892f2a2b8c32: Pull complete
f17d3f3dc1af: Pull complete
b6e71bdb2060: Pull complete
36ee5f422b46: Pull complete
f57ac824c32c: Pull complete
f62afcfdde73: Pull complete
c315d6df5bb1: Pull complete
21b0fa595035: Pull complete
176a9ac56651: Pull complete
26d4680488be: Pull complete
07a88cd98fd5: Pull complete
Digest: sha256:2d907dbc2aac81fcfcbae13c7ed4597f57d82142ca7653cc28102f087c5be4d5
Status: Downloaded newer image for wordpress:latest
```
This will download many layers, 18 in total!

## Show Docker images;
To show the Docker images we just have downloaded.
```
$ docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
wordpress           latest              f345336550a0        12 hours ago        410MB
alpine              latest              e21c333399e0        11 days ago         4.14MB
```


## Display layers of a existing Docker image;
Now we have download the example images it's time to take a close look at how many layers the image exists.

### Show layers of the Alpine Docker image
```
$ docker history alpine

IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
e21c333399e0        11 days ago         /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B                  
<missing>           11 days ago         /bin/sh -c #(nop) ADD file:2b00f26f6004576...   4.14MB   
```
Just one layer, like we have seen before while downloading the Docker image.

### Show layers of the Wordpress Docker image

```
$ docker history wordpress

IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
f345336550a0        12 hours ago        /bin/sh -c #(nop)  CMD ["apache2-foreground"]   0B                  
<missing>           12 hours ago        /bin/sh -c #(nop)  ENTRYPOINT ["docker-ent...   0B                  
<missing>           12 hours ago        /bin/sh -c #(nop) COPY file:db1f48c4963a43...   6.85kB              
<missing>           12 hours ago        /bin/sh -c set -ex;  curl -o wordpress.tar...   28.1MB              
<missing>           12 hours ago        /bin/sh -c #(nop)  ENV WORDPRESS_SHA1=892d...   0B                  
<missing>           12 hours ago        /bin/sh -c #(nop)  ENV WORDPRESS_VERSION=4...   0B                  
<missing>           12 hours ago        /bin/sh -c #(nop)  VOLUME [/var/www/html]       0B                  
<missing>           12 hours ago        /bin/sh -c a2enmod rewrite expires              60B                 
<...snip...>                       
<missing>           15 hours ago        /bin/sh -c apt-get update  && apt-get inst...   8.31MB              
<missing>           15 hours ago        /bin/sh -c mkdir -p $PHP_INI_DIR/conf.d         0B                  
<missing>           15 hours ago        /bin/sh -c #(nop)  ENV PHP_INI_DIR=/usr/lo...   0B                  
<missing>           15 hours ago        /bin/sh -c apt-get update && apt-get insta...   244MB               
<missing>           15 hours ago        /bin/sh -c #(nop)  ENV PHPIZE_DEPS=autocon...   0B                  
<missing>           19 hours ago        /bin/sh -c #(nop)  CMD ["bash"]                 0B                  
<missing>           19 hours ago        /bin/sh -c #(nop) ADD file:f30a8b5b7cdc9ba...   55.3MB   
```

Again multiple layers, and you can also see what each layer is doing and how large the layer is.

## Cleanup
Remove the images we just have downloaded.

```
$ docker rmi alpine wordpress

Untagged: alpine:latest
Untagged: alpine@sha256:ccba511b1d6b5f1d83825a94f9d5b05528db456d9cf14a1ea1db892c939cda64
Deleted: sha256:e21c333399e0aeedfd70e8827c9fba3f8e9b170ef8a48a29945eb7702bf6aa5f
Deleted: sha256:04a094fe844e055828cb2d64ead6bd3eb4257e7c7b5d1e2af0da89fa20472cf4
Untagged: wordpress:latest
Untagged: wordpress@sha256:2d907dbc2aac81fcfcbae13c7ed4597f57d82142ca7653cc28102f087c5be4d5
Deleted: sha256:f345336550a098b51fff2549202853f67fe47aa1d8e87208cac8e6d88de5752c
Deleted: sha256:eb4c943cecd88cee45b8414c193245cb1412fe815456847a3555bd4f3956e343
Deleted: sha256:71e9ea0faebceefc97a86ace00b4861678f61f59f877610099f11f3cb1f64917
Deleted: sha256:0b286708415abd30366a59563ce0eff23c469c0ba0659ab0a6cf39fe95f7a012
Deleted: sha256:fdbe332cac1142bfd95703141936772bdb5d4e689ce2d07a7a51ae5d7edadcec
Deleted: sha256:195a05c833954613cf5e9e22ed5bd2229d6fd1244580abfcca52df1cea2a6c2a
Deleted: sha256:9ab46bfda16c2b74c1e87fd6f6bc62801a51e1e5314d08534616674213b404a3
Deleted: sha256:313adaa36842c271aa856402f11c0265a2d37235986267de073dbc5f7cf48470
Deleted: sha256:19ba283b21d6a9d3aaca309310d635b68cd5833502d2de08731481c642757deb
Deleted: sha256:d9dde898eb8e481997ea19bf66a6bb3f748895e565f8a9c4ed319c2c11e796be
Deleted: sha256:48a7a1091890b97aa91db4ebe687a5743cfba433aeea78d5745c4d22ba9793c9
Deleted: sha256:5d3095033ac709b397b532d29a59bbbd3f7a969b83e71cd2bfe921096b21c400
Deleted: sha256:b16350359ce18bc5658be1da92271c50014fef3038d49ed47d0ba7c52dbb33df
Deleted: sha256:f68745c5b954e100f068237e87a26228dba596a23b3078235c6018d95b9fe7e3
Deleted: sha256:ae5bc71d737ae444765e217e2f0ac7362c1c313816fe654ffa817a4110644d0b
Deleted: sha256:f38b6d0e110982959a0710ad3472af9c6568a7be261218863890c61fe914cf5d
Deleted: sha256:399a8ae46a9f778ab3f48975052fa5c14578526915fc3afc2fd4769184508c5e
Deleted: sha256:828dd1e27780ede1369cda5e6b133b30477cb22ee971e74fcb055fc3112a776c
Deleted: sha256:2ec5c0a4cb57c0af7c16ceda0b0a87a54f01f027ed33836a5669ca266cafe97a
```

And make sure they are gone.

```
$ docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```
