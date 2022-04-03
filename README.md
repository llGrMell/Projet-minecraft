# Projet-Minecraft

# Documentation d'installation des serveurs Minecraft

## Sommaire

- [Prérequis](#p0)
- [Création et lancement du serveur](#p1)
- [Backup](#p2)
     - [Manuel](#p2.1)
     - [Automatique](#p2.2)


## Prérequis<a name="p0"></a>

Machines : Raspberry Pi 4 Modèle B 4Go

Go de RAM : 3GB (minimum) pour un serveur Minecraft

OS : Rasbian OS

Backup : Clé USB

## Création et lancement du serveur <a name="p1"></a>

Notre problème sur ce projet est de créer plusieurs serveur Minecraft. Pour répondre à ce problème, on a eu comme idée de créer UN serveur Minecraft pour le copier-coller.

<br></br>

Pour commencer, nous avons créé les dossiers ```/srv/mc/serveur_parent``` pour installer à l'intérieur tous les dossiers et fichiers permettant de créer le premier serveur Minecraft. En entrant dans ```serveur_parent``` on peut voir que l'installation à été bien fait.
```
/srv/mc/serveur_parent
eula.txt  libraries  logs  server.jar  server.properties  start.sh  versions
```

<br></br>

Une fois l'installation fait, nous allons rentrer dans ```server.properties``` pour modifier le server-port en mettant PORT au lieu de 25564. On fait cela pour faciliter ... (je c plus) 
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

Maintenant que le serveur Minecraft a été installé et bien configuré, nous devons le copier le coller. Pour cela, on a créé un script .sh dans un nouveau dossier que nous l'avons nommé ```new_server```. C'est ici que nous allons créer tous nos server Minecraft.
```
/srv/mc/new_server
/srv/mc/new_server# nano new_server.sh
```
```
#!/bin/sh
cp -r /srv/mc/server_parent /srv/mc/server4 && sed -i 's/PORT/25561/' /srv/mc/server4/server.properties
```
Quand nous allons lancer la commande ./new_server.sh celle-ci va copier le ```server_parent``` puis le coller dans le dossier ```/mc``` avec les modifications que nous lui avons apporté dans le ```server.properties```.
```cp -r``` permet de copier le chemin du dossier en question dont le ```server_parent``` avec tous ses fichiers et dossiers.
Puis il sera collé sous le nom de server4 et son ```server-port=PORT``` sera remplacer par ```server-port=25561```.

<br></br>

En retournant dans le dossier mc, nous retrouvons notre server4.
```
/srv/mc/
......... Server4 ......
```

<br></br>

Maintenant que le serveur a été installer, il faut le lancer. Pour faire cela, il faut rentrer dans le server4 puis le lancer avec la commande ```./start.sh```.

(Alex montre ce qui se trouve dans le start.sh)
```
/srv/mc/server4
```
```
/srv/mc/server4# ./start.sh
```

## Backup <a name="p2"></a>
### Manuel  <a name="p2.1"></a>


Une fois que tout est fait, nous allons faire un backup pour sauvegarder tous nos fichiers et dossiers sur une clé USB. Pour cela nous avons fait un dossier dans la quel se trouve un script.  
```
/srv/mc/backup
/srv/mc/backup# nano backup.sh
```

```
#!/bin/bash
rsync -a /srv/mc /media/pi/CLEF_BACKUP/backup
```
Se script va copier les dossiers ```/srv/mc``` avec les modifications qu'on lui a apportées et le sauvegarder sur le chemin qu'on lui a donné. Dans notre cas on lui donné comme destination une clé USB

<br></br>

Pour lancer le script, suffit juste de lancer le ```./backup.sh```.
```
/srv/mc/backup# ./backup.sh
```

### Automatique  <a name="p2.2"></a>

Pour faire une sauvegarde automatique il suffits d'éditer la table cron, en exécuter la commande:
``` 
crontab -e
```

Cette commande a pour effet de lancer l'éditeur présentant la table actuelle. Chaque entrée de la table (chaque ligne) correspond à une tâche à exécuter et est notée de la façon suivante:
mm hh jj MMM JJJ

Dans cette syntaxe:

mm représente les minutes (de 0 à 59)

hh représente l'heure (de 0 à 23)

jj représente le numéro du jour du mois (de 1 à 31)

MMM représente le numéro du mois (de 1 à 12) ou l'abréviation du nom du mois (jan, feb, mar, apr, ...)

JJJ représente l'abréviation du nom du jour ou le chiffre correspondant au jour de la semaine (0 représente le dimanche, 1 représente le lundi, ...)

En faisant cette commande: 
``` 
11 * * * * /srv/mc/backup/backup.sh
```
Cela veut dire que chaque heure passée de 11 minutes il va lancer le script ```backup.sh``` permettant de sauvegarder dans la clé USB. 

<br></br>

Quelques autres exemples :

Tous les lundis à 22h28:
``` 
 30 23 1 * * /srv/mc/backup/backup.sh
```

Tous les premiers du mois à 23h30:
``` 
11 * * * * /srv/mc/backup/backup.sh
```




