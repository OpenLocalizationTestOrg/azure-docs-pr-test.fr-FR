---
title: aaaCollect des performances des applications Linux dans OMS journal Analytique | Documents Microsoft
description: "Cet article fournit des détails de configuration hello Agent OMS pour Linux toocollect des compteurs de performances pour Apache HTTP Server et MySQL."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a>Collecte des compteurs de performances pour les applications Linux dans Log Analytics 
Cet article fournit des détails de configuration hello [Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect les compteurs de performances pour des applications spécifiques.  les applications de Hello incluses dans cet article sont :  

- [MySQL](#MySQL)
- [Apache HTTP Server](#apache-http-server)

## <a name="mysql"></a>MySQL
Si MySQL Server ou MariaDB Server est détecté sur l’ordinateur de hello lorsque hello OMS agent est installé, un fournisseur pour MySQL Server d’analyse des performances seront installé automatiquement. Ce fournisseur connecte toohello local MySQL/MariaDB server tooexpose les statistiques de performances. Informations d’identification MySQL doivent être configurées afin que hello fournisseur d’accéder à hello MySQL Server.

### <a name="configure-mysql-credentials"></a>Configuration des informations d’identification de MySQL
Hello fournisseur OMI MySQL requiert un utilisateur MySQL soit préconfiguré et les bibliothèques clientes MySQL installées dans l’ordre tooquery hello informations performances et d’intégrité à partir de l’instance de MySQL hello.  Ces informations d’identification sont stockées dans un fichier d’authentification qui est stocké sur l’agent Linux de hello.  fichier d’authentification Hello Spécifie l’adresse de liaison et instance de MySQL hello port d’écoute et les informations d’identification toouse toogather métriques.  

Lors de l’installation de hello Agent OMS pour Linux hello OMI MySQL fournisseur recherchera les fichiers de configuration MySQL my.cnf (emplacements par défaut) adresse de liaison et un port et partiellement hello de jeu de fichier d’authentification OMI MySQL.

fichier d’authentification MySQL Hello est stocké à `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.


### <a name="authentication-file-format"></a>Format du fichier d’authentification
Voici le format hello pour hello fichier d’authentification OMI MySQL

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

les entrées dans le fichier d’authentification hello Hello sont décrits dans hello tableau suivant.

| Propriété | Description |
|:--|:--|
| Port | Représente les hello de port actuel hello MySQL instance écoute. Type de port 0 indique que les propriétés hello suivantes sont utilisées pour l’instance par défaut. |
| Adresse de liaison| Adresse de liaison MySQL active. |
| username| Utilisateur MySQL utilisé l’instance de serveur MySQL toouse toomonitor hello. |
| Mot de passe encodé en base 64| Mot de passe de hello utilisateur d’analyse MySQL codé en Base64. |
| AutoUpdate| Indique si toorescan pour les modifications dans le fichier my.cnf de hello et remplacer le fichier d’authentification OMI MySQL hello lorsque hello fournisseur OMI MySQL est mis à niveau. |

### <a name="default-instance"></a>Instance par défaut
Hello fichier d’authentification OMI MySQL peut définir une instance par défaut et toomake de numéro de port gérer plusieurs instances MySQL sur un hôte Linux plus facile.  instance par défaut de Hello est représentée par une instance avec le port 0. Toutes les instances supplémentaires héritent des propriétés définies à partir de l’instance par défaut de hello, sauf si elles spécifient des valeurs différentes. Par exemple, si l’instance MySQL à l’écoute sur le port « 3308 » est ajoutée, l’instance par défaut de hello adresse de liaison, nom d’utilisateur et mot de passe codé en Base64 seront être tootry utilisé d’analyser hello instance à l’écoute du port 3308. Si l’instance hello du port 3308 est lié tooanother adresse et utilise hello du même nom d’utilisateur MySQL mot de passe paire uniquement hello adresse de liaison est nécessaire et hello autres propriétés sont héritées.

Hello tableau suivant a des paramètres de l’instance exemple 

| Description | Fichier |
|:--|:--|
| Instance par défaut et instance avec le port 3308. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| Instance par défaut et instance avec le port 3308 et un autre nom d’utilisateur et un autre mot de passe. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a>Programme du fichier d’authentification OMI MySQL
Fournisseur est un programme de fichier d’authentification OMI MySQL qui peut être utilisé tooedit hello authentification OMI MySQL fichier inclus avec installation hello Hello OMI MySQL. programme de fichier d’authentification Hello sont accessibles à l’emplacement suivant de hello.

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> fichier d’informations d’identification de Hello doit être accessible en lecture hello omsagent compte. Est recommandé d’exécuter la commande mycimprovauth de hello pour omsgent.

Hello tableau suivant fournit des détails sur la syntaxe de hello pour l’utilisation de mycimprovauth.

| Opération | Exemple | Description
|:--|:--|:--|
| autoupdate *false\|true* | mycimprovauth autoupdate false | Fichier d’authentification hello ou non sera automatiquement mis à jour de jeux sur Redémarrer ou mettre à jour. |
| default *adresse_de_liaison nom_utilisateur mot_de_passe* | mycimprovauth default 127.0.0.1 root pwd | Jeux de hello instance par défaut dans le fichier d’authentification OMI MySQL de hello.<br>champ de mot de passe Hello doit être entré au format texte brut, un mot de passe hello Bonjour fichier d’authentification OMI MySQL codée en Base 64. |
| delete *valeur_par_défaut\|num_port* | mycimprovauth 3308 | Supprime l’instance spécifiée de hello par défaut ou par numéro de port. |
| help | mycimprov help | Imprime une liste de commandes toouse. |
| print | mycimprov print | Imprime un tooread facile de fichier d’authentification OMI MySQL. |
| update num_port *adresse_de_liaison nom_utilisateur mot_de_passe* | mycimprov update 3307 127.0.0.1 root pwd | Met à jour d’instance spécifiée de hello ou ajoute l’instance de hello s’il n’existe pas. |

Hello exemples de commandes suivants définissent un compte d’utilisateur par défaut pour le serveur de hello MySQL sur localhost.  champ de mot de passe Hello doit être entré au format texte brut - mot de passe de hello Bonjour fichier d’authentification OMI MySQL est codée en Base 64

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a>Autorisations de base de données requises pour les compteurs de performances MySQL
Hello utilisateur MySQL nécessite toohello accès suivant requêtes toocollect données de performances MySQL Server. 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


utilisateur de MySQL Hello requiert également toohello accès choisi par défaut tableaux suivants.

- information_schema
- mysql. 

Ces privilèges peuvent être accordés en exécutant hello suivant de commandes grant.

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> toogrant autorisations tooa analyse hello utilisateur octroi d’utilisateur MySQL doit avoir hello privilège « GRANT option », ainsi que des privilèges hello accordée.

### <a name="define-performance-counters"></a>Définition des compteurs de performances

Une fois que vous configurez hello Agent OMS pour Linux toosend données tooLog Analytique, vous devez configurer toocollect de compteurs de performances hello.  Hello, procédez dans [sources de données de performances Windows et Linux dans le journal Analytique](log-analytics-data-sources-windows-events.md) avec des compteurs de hello Bonjour tableau suivant.

| Nom d’objet | Nom de compteur |
|:--|:--|
| MySQL Database | Disk Space in Bytes |
| MySQL Database | Tables |
| MySQL Server | Aborted Connection Pct |
| MySQL Server | Connection Use Pct |
| MySQL Server | Disk Space Use in Bytes |
| MySQL Server | Full Table Scan Pct |
| MySQL Server | InnoDB Buffer Pool Hit Pct |
| MySQL Server | InnoDB Buffer Pool Use Pct |
| MySQL Server | InnoDB Buffer Pool Use Pct |
| MySQL Server | Key Cache Hit Pct |
| MySQL Server | Key Cache Use Pct |
| MySQL Server | Key Cache Write Pct |
| MySQL Server | Query Cache Hit Pct |
| MySQL Server | Query Cache Prunes Pct |
| MySQL Server | Query Cache Use Pct |
| MySQL Server | Table Cache Hit Pct |
| MySQL Server | Table Cache Use Pct |
| MySQL Server | Table Lock Contention Pct |

## <a name="apache-http-server"></a>Apache HTTP Server 
Si Apache HTTP Server est détecté sur l’ordinateur de hello lorsque hello du bundle omsagent, un fournisseur pour Apache HTTP Server d’analyse des performances seront installé automatiquement. Ce fournisseur s’appuie sur un module Apache qui doit être chargé dans hello Apache HTTP Server ordre tooaccess les données de performance. module de Hello peut être chargé par hello de commande suivante :
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello module d’analyse Apache, exécutez hello de commande suivante :
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a>Définition des compteurs de performances

Une fois que vous configurez hello Agent OMS pour Linux toosend données tooLog Analytique, vous devez configurer toocollect de compteurs de performances hello.  Hello, procédez dans [sources de données de performances Windows et Linux dans le journal Analytique](log-analytics-data-sources-windows-events.md) avec des compteurs de hello Bonjour tableau suivant.

| Nom d’objet | Nom de compteur |
|:--|:--|
| Apache HTTP Server | Busy Workers |
| Apache HTTP Server | Idle Workers |
| Apache HTTP Server | Pct Busy Workers |
| Apache HTTP Server | Total Pct CPU |
| Apache Virtual Host | Errors per Minute - Client |
| Apache Virtual Host | Errors per Minute - Server |
| Apache Virtual Host | KB per Request |
| Apache Virtual Host | Requests KB per Second |
| Apache Virtual Host | Requests per Second |



## <a name="next-steps"></a>Étapes suivantes
* [Collecter les compteurs de performances](log-analytics-data-sources-performance-counters.md) à partir d’agents Linux.
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles. 
