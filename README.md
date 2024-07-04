# INF1070ETE2024-LAB9

# CONNECTION : 

Se connecter au serveur avec SSH :

```sh 
ssh xxxxxxxx@java.labunix.uqam.ca
The authenticity of host 'java.labunix.uqam.ca (132.208.132.55)' can't be established.
ED25519 key fingerprint is SHA256:2Ykb7YfGfZTr8zjTeHaA98qY0A4aQBKhb33Ye1SeA+U.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'java.labunix.uqam.ca' (ED25519) to the list of known hosts.
ha891983@java.labunix.uqam.ca's password: 
```

`xxxxxxx` : votre code ms
mot de passe : mot de passe lie au code ms !


`who` : doit afficher au moins votre nom d'utilisateur

Il est possible que votre systeme ne possede pas de fichiers ! 
(Ils devraient apparaitre si vous faites le cours de base de donnees).

`ls home` : affiche les noms de tous les utilisateurs... 

`cd` : ne permet pas l'accès aux fichiers des autres utilisateurs.  

`permissions` : `drwx------` ainsi seulement des droits pour l'utilisateur propriétaire. 

`exit` : se déconnecte du serveur !

`ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 -o HostKeyAlgorithms=+ssh-rsa ha891983@zeta2.labunix.uqam.ca`

`-oKexAlgorithms=+diffie-hellman-group1-sha1` : algorithme d'echange de clés.
`-o HostKeyAlgorithms=+ssh-rsa` : algorithme de la clé de l'hote.

Références supplémentaires : [link](https://wiki.uqam.ca/display/SWSI/Labunix)

# GÉNÉRATION DE CLÉS : 

`ssh-keygen` : génère une clé SSH. (Lisez les instructions qui apparaissent)

`cat` : ne pas faire de cat sur la clé privée (il faut "vraiment" la protéger...) 

```
ssh-copy-id xxxxxxx@java.labunix.uqam.ca
The authenticity of host 'java.labunix.uqam.ca (132.208.132.55)' can't be established.
RSA key fingerprint is e7:a2:18:b5:a9:50:91:79:83:98:96:84:39:f0:21:be.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'java.labunix.uqam.ca,132.208.132.55' (RSA) to the list of known hosts.
xxxxxxx@java.labunix.uqam.ca's password: 
Now try logging into the machine, with "ssh 'xxxxxxx@java.labunix.uqam.ca'", and check in:

  .ssh/authorized_keys

to make sure we haven't added extra keys that you weren't expecting.
```

`xxxxxxx@java.labunix.uqam.ca` : devrait nous laisser nous connecter sans mot de passe.

Note : Utile pour github/gitlab ! 

# TMUX : 

Ici, suivez les instructions : 
`CTRL-B %` : on peut le faire en 2 étapes donc `CTRL-B` puis `%`. 

Rappel pour le script : 

- Téléchargez le fichiers avec `wget` ! 
- Ajoutez les droits d'exécution avec `chmod +x` ! 
- Lancez le script avec `./nom_du_script` 

# DOCKER : 

```
sudo docker run -it ubuntu /bin/bash
```

`man docker-run` : manuel de docker avec l'option run

`-i` : interactif ! 
`-t` : avec un terminal
`ubuntu` : indique l'image a utiliser 
`/bin/bash` : programme a executer 

`docker ps` : comme ps permet de lister les conteneurs 
`-a` : indique qu'on veut afficher TOUS les conteneurs (même ceux éteints)

Suivre les commandes pour `start` et `attach`. 

`vim` : on se rend compte que les dockers sont indépendants. il faut réinstaller `vim`.  


## Installation de apache2 : 

`service apache2 restart` : après l'installation de apache2 ! 

On peut verifier avec `curl localhost:80` devrait retourner du HTML : 

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
...
</html>
```

## Apres installation de curl, apache2 : 

`apache2` : serveur web (donc sur le port 80) 

`localhost:80` : devrait retourner une page d'erreur 
(car nous n'avons pas connecté le port du conteneur sur le port de notre machine)


## Bind et Publish : 

` sudo docker create -it --mount type=bind,src="$(pwd)/vim",target="/root" --publish 8080:80 ubuntu /bin/bash ` 

`create` marche comme `run` ainsi, on lui ajoute `-it ubuntu /bin/bash` comme c'était pour `run`. 

`--publish 8888:80` permet de connecter le port 8888 de la VM (notre ordinateur) au port 80 du conteneur.

`--mount type=bind,src="$(pwd)/vim",target="/root"` permet de connect le dossier `vim` de notre VM au dossier `root` du conteneur. 
`type=bind` indique que le mode de connection est un attachement.

# DockerFile 

``` 
FROM ubuntu

RUN apt-get -y update
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get install -y vim curl apache2
COPY vim/.vimrc /root
WORKDIR /var/www/html
```

Avec une image ubuntu, nous lançons `apt-get update`. On indique qu'on est en non-interactif. On install vim, curl, apache2. On copie le fichier `.vimrc` dans `/root`.
Le dossier dans lequel on va travailler est `/var/www/html`.


Avec : 

```
.
└── Dockerfile
    ├── Dockerfile
    └── vim
```
Lancez `sudo docker build ./Dockerfile/` !

On peut lancer `sudo docker run -it ad7307612714 /usr/bin/vim` :D 

NOTE : Le nom du docker est donné dans la commande précédante !

Lancez le service avec `service apache2 start`. 
