# Projet-minecraft

# Documentation d'instalation des serveurs minecraft

## Sommaire

- [Prérequis](#p0)
- [Création des serveurs](#p1)
    - [Serveur Parent](#p1.1)
    - [Initialisation](#p1.2)

## Prérequis <a name="p0"></a>

Machines : Raspberry Pi 4 Modèle B 4Go

Go de RAM : 3GB (minimum) pour un serveur minecraft

OS : Rasbian OS

Backup : Clé USB

## Création des serveurs <a name="p1"></a>

Notre probleme sur se projet est de créer plusieur serveur minecaft. Pour répondre à ce problemes, on a eu comme idée de creer UN serveur Minecraft pour le copier coller.

<br></br>

Pour commencer, on a créé les dossiers "/srv/mc/serveur_parent" pour installer à l'interieur le premier serveur minecraft.
```
/srv/mc/serveur_parent
```
<br></br>

Maintenant qu'une fois le serveur Minecraft a été installé, nous devons le copier et le coller. Pour cela, on a créer un script dans un nouveau dossier.
```
/srv/mc/new_server
/srv/mc/new_server # nano (oe.sh)
```
```
la commande dans le oe.sh
```
Quant on va lancer le (oe.sh) celui-ci va copier le Serveur Parent pour le coller dans le dossier /mc avec les modifications que nous avons mis. 

<br></br>















 
