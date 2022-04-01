# Projet-minecraft

# Documentation d'instalation des serveurs minecraft

## Sommaire

- [Prérequis](#p0)
- [Création et lancement du serveur](#p1)
- [Backup](#p1)


## Prérequis <a name="p0"></a>

Machines : Raspberry Pi 4 Modèle B 4Go

Go de RAM : 3GB (minimum) pour un serveur minecraft

OS : Rasbian OS

Backup : Clé USB

## Création et lancement du serveur <a name="p1"></a>

Notre probleme sur se projet est de créer plusieur serveur minecaft. Pour répondre à ce problemes, on a eu comme idée de creer UN serveur Minecraft pour le copier coller.

<br></br>

Pour commencer, nous avons créé les dossiers "/srv/mc/serveur_parent" pour installer à l'interieur tous les dossiers et fichiers permettant de creer le premier serveur Minecraft. En entrant dans serveur_parent on peut voir que l'installation à été bien fait.
```
/srv/mc/serveur_parent
eula.txt  libraries  logs  server.jar  server.properties  start.sh  versions
```
Une fois l'installation fait, nous allons rentrer dans server.properties pour modifier le server-port en mettant PORT au lieu de 25564. On fait cela pour faciliter ... (je c plus) 
```
/srv/mc/serveur_parent/ nano server.properties
```
```
.
.
.
ressource-pack-prompt=
allow-nether=true
server-port=PORT
enable-rcon=false
.
.
.

```

<br></br>

Maintenant que le serveur Minecraft a été installé et bien configuré, nous devons le copier le coller. Pour cela, on a créer un script .sh dans un nouveau dossier que nous l'avons nommé new_server. C'est ici que nous allons créé tous nos server minecraft.
```
/srv/mc/new_server
/srv/mc/new_server# nano new_server.sh
```
```
#!/bin/sh
cp -r /srv/mc/server_parent /srv/mc/server4 && sed -i 's/PORT/25561/' /srv/mc/server4/server.properties
```
Quans nous allons lancer la commande ./new_server.sh celle-ci va copier le server_parent puis le coller dans le dossier /mc avec les modifications que nous lui avons apporté dans le server.properties.
```cp -r``` permet de copier le chemin du dossier en queston dont le server_parent avec tous ses fichiers et dossiers.
Puis il sera coller sous le nom de server4 et son server-port=PORT sera remplacer par server-port=25561.

<br></br>

En retounant dans le dossier mc, nous retrouvons notre server4.
```
/srv/mc/
......... Server1 ......
```

## Backup <a name="p0"></a>

pas eu le temps dsl 


























 
