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


## Apres installation de curl, apache2 : 

`apache2` : serveur web (donc sur le port 80) 

`localhost:80` : devrait retourner une page d'erreur 
(car nous n'avons pas connecté le port du conteneur sur le port de notre machine)


