# Read-Me (EN) : go to below
CMS for weather station (Davis-Weatherlink)
# Lisez-Moi (FR) :
CMS pour station météo (Davis-Weatherlink)

Pour de plus amples détails, aller sur le wiki de Mbell : https://github.com/Networkbell/mbell/wiki/MBell-fr


# Description (FR)

MBell est un système de gestion de contenu (CMS - content management system) pour propriétaire de stations météos disposant d'une API au format json, leur permettant de diffuser leurs données météorologiques en temps réel sur leur propre hébergement internet.

Exemple de station météo utilisant mbell à cette adresse : http://www.meteobell.com/mbell/index.php


# Prérequis (FR)

- Disposer d'une station météo de la marque Davis Instruments avec datalogger IP (weatherlink v1 et v2), connexion USB (weatherlink v2) ou Weatherlink Live.
- Disposer d'un hébergement internet
- Disposer d'1 base de données sur son hébergement internet

NOTE 1 : Si vous ne disposez ni d'hébergement internet et/ou ni de base de données, vous pouvez cependant installer Mbell sur votre ordinateur en local. Suivre dans ce cas la procédure d'installation avec localhost.

NOTE 2 : Une base de donnée est nécessaire depuis la version 2.0 de mbell, mais vous pouvez toutefois télécharger la version précédente, sans base de données, à cette adresse, avec mbell 1.6 : http://www.meteobell.com/mbell.php Attention cette version, bien que parfaitement opérationnelle, ne sera plus mis à jour et ne disposera donc pas des dernières évolutions depuis la version 2.0. Contrairement à la version 2.0, cette version 1.6, plus ancienne, nécessite une inscription obligatoire sur meteobell.com.


# Installation (FR)

1. Télécharger MBell sur Github (clic sur le bouton vert "Code" -> "Download ZIP")
2. Dézipper le fichier mbell-main.zip

NOTE 1 : le dossier "mbell-main" obtenus peut être renommé comme bon vous semble.

## Installation sur Internet (FR)

3. Avec un logiciel FTP (exemple FileZilla), installer le dossier "mbell-main" sur votre site internet
4. Aller à l'adresse url de votre site à l'emplacement de mbell : http://www.votre-site.com/mbell-main/
5. La procédure d'installation se lance automatiquement en vous guidant pas à pas

NOTE 1 : vous pouvez placer le dossier "mbell-main" à n'importe quel endroit de votre site.

NOTE 2 : les informations de connexions à votre base de données vous sont fournis par votre hébergeur. Il vous sera peut-être nécessaire de créer la base de données (avec PHPMyAdmin) si elle n'existe pas encore (clic sur "Nouvelle base de données"). Dans ce cas vous n'avez qu'à donner un nom de base de donnée et choisissez l'encodage "utf8_general_ci". Enfin préférez MariaDB que MySQL si possible.

## Installation en localhost (FR)

3. Avec un logiciel de serveur virtuel (Wamp ou EasyPHP) aller à l'emplacement du dossier "mbell-main" sur votre disque dur
4. La procédure d'installation se lance automatiquement en vous guidant pas à pas

NOTE 1 : La base de données en local doit avoir comme propriétés : Adresse = localhost / Utilisateur = root / Pas besoin de mot de passe / Comme pour l'installation Internet, le nom de la base de données doit être créé au préalable avec PHPMyAdmin (même procédure)

## Mis à Jour - Version Plus Récente (nouveauté 2.3)

Si vous souhaitez mettre à jour Mbell dans une version plus récente, plus besoin de réinstaller (depuis version 2.3), il vous suffit d'écraser les nouveaux fichiers dans les anciens. Mbell détectera alors automatiquement qu'il doit être mis à jour et lancera une procédure d'installation simplifié sans toucher à votre bdd. Vos tables ne seront pas supprimés, mais seront mises à jour selon les besoins de la version que vous installez. Vous ne perdez donc aucune info.

A partir de la version 2.3 installée, vous n'aurez pour les prochaines mises à jours, quand elles seront prêtes, plus besoin de le faire manuellement comme avant via Github. Mbell détecte maintenant automatiquement s'il a besoin d'être mis à jour et vous n'avez qu'à appuyer sur le bouton de Mis à Jour alors disponible pour patcher automatiquement mbell dans la dernière version dispoinible. 

NOTE 1 : Si un problème quelconque arrive, ou que vous rencontrez un message d'erreur suite à une mise à jour ou installation, il est parfois préférable cependant de faire une ré-installation complète (un fichier mal copié ou une écriture serveur qui s'est mal effectué pendant l'installation, ça peut arriver). Mbell détectera également si vous vous trompez en faisant une mise à jour avec une version plus ancienne, auquel cas il faudra faire une réinstallation complète.

## Re-Installation

Si vous souhaitez réinstaller Mbell dans la même version, vous pouvez soit supprimer le fichier admin.php dans le dossier config, soit changer `$installed = 'yes';` dans le fichier admin.php par 'no'. Cela relancera la procédure d'installation depuis le début. Attention, cela supprimera avant de les recréer aussi vos tables dans votre base de données (sauf mb_data). La table de vos données météos (créés avec le cronjob) n'est en revanche pas touché. La seule façon de supprimer mb_data est de le faire manuellement avec PhpMyAdmin, ceci afin de ne pas perdre vos données météos-climatos.

## Installation Avancée

La phase d'installation va créer un fichier "**admin.php**" dans le dossier config. Pour relancer la phase d'installation, il suffit alors de supprimer ce fichier "admin.php". Notez que si vous utilisez les mêmes préfixes de tables, lors de cette nouvelle installation, toute la bdd sera écrasé (détruite puis recréé pour être exact). 

**Ne supprimez ou ne modifiez jamais le fichier "admin-backup.php"**. Vous pouvez par contre installer manuellement mbell en **copiant** ce fichier "admin-backup.php" et en renommant cette nouvelle copie "admin.php" puis en remplissant manuellement les informations demandées à l'intérieur de ce nouveau fichier. Tout est expliqué à l'intérieur du fichier pour vous aider à installer manuellement mbell. 


# Plusieurs Stations Météos / Mbell

Si vous disposez de plusieurs stations météos, avecun chacune une API différente et voulez avoir un mbell pour chacun d'eux sur le même hébegerment internet c'est tout à fait possible. Vous n'avez même pas besoin d'avoir plusieurs base de données pour cela. 

Il vous suffit d'installer plusieurs mbell avec des préfixes de tables différents. Exemple :  
1. un mbell à l'adresse suivante http://www.votre-nom-de-domaine/station-1/mbell/ avec comme préfixe de table mb1_
2. un autre mbell à l'adresse suivante http://www.votre-nom-de-domaine/station-2/mbell/ avec comme préfixe de table mb2_
etc...

NOTE 1 : Vous pouvez aussi faire cela avec une seule station météo et des mbell avec plusieurs configurations, langues, design etc différentes.


# Debug

Si vous rencontrez un problème avec MBell, avant de m'en informer, allez dans le fichier "admin.php" du dossier "config" et activez la fonction de débogage en mettant "true" à la place de "false" à la ligne :
$debug = false;

 # Versions

    2.0 (-0.55) - Initial Release
    2.1 (-0.58) - Addon : Weatherlink Live
    2.2 (-0.63) - Addon : Cron Weather Backup
    2.3 (-0.65) - Addon : Auto Update System

Version actuelle = Publique 2.3 (Développement -0.65)


# Problèmes connus

 ## Général :

- le système de cronjob introduit en 2.2 est très/trop sensible aux désactivations serveurs, il se désactive donc souvent si votre hébergement est un peu trop instable et doit être relancé manuellement (réparé dans une future version)

## Avec Weatherlink Live :

- Toutes les infos de stations ne sont pas proposés, je recherche des personnes possédant ce type de sondes auxiliaires, afin de réaliser des tests et les ajouter à Mbell :

1. Station Météo Auxiliaire de Température Air-Eau-Sol (6372)
2. Station Météo Auxiliaire de Température & Humidité de l'Air (6382)
3. Station Météo Auxiliaire Humectation du Feuillage / Température & Humidité du Sol (6345)

- L'API Weatherlink Live en gratuite est très basique et possède beaucoup moins d'informations proposées qu'auparavant, je ne peux donc afficher toutes les informations que Mbell propose avec les API précédentes, le template Mbell a été donc allégé en conséquence.
