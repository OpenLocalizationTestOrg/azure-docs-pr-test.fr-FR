---
title: aaaSet des PostgreSQL sur un VM Linux | Documents Microsoft
description: "Découvrez comment tooinstall et configurer PostgreSQL sur un ordinateur virtuel de Linux dans Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a>Installer et configurer PostgreSQL sur Microsoft Azure
PostgreSQL est tooOracle similaire d’avancée de la base de données open source et DB2. Il inclut des fonctionnalités destinées aux entreprises, comme la conformité complète à ACID, un traitement transactionnel fiable et un contrôle d’accès concurrentiel multiversion. Il prend également en charge des normes comme ANSI SQL et SQL/MED (y compris les wrappers de données externes pour Oracle, MySQL, MongoDB et beaucoup d’autres). Il est hautement extensible, avec la prise en charge de 12 langages procéduraux, les index GIN et GIST, la prise en charge des données spatiales et plusieurs fonctionnalités de type NoSQL pour les applications JSON ou basées sur les paires clé-valeur.

Dans cet article, vous allez apprendre comment tooinstall et configurer PostgreSQL sur une machine virtuelle Azure exécutant Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>Installation de PostgreSQL
> [!NOTE]
> Vous devez déjà disposer d’une machine virtuelle Azure exécutant Linux dans l’ordre toocomplete ce didacticiel. toocreate et configurer un VM Linux avant de procéder, consultez la [didacticiel de la machine virtuelle de Azure Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

Dans ce cas, utilisez le port 1999 comme hello PostgreSQL port.  

Se connecter toohello VM Linux vous avez créé via PuTTY. S’il s’agit hello première fois que vous utilisez une machine virtuelle Linux de Azure, consultez [comment tooUse SSH avec Linux sur Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn comment toouse PuTTY tooconnect tooa Linux VM.

1. Exécutez hello suivant racine de toohello commande tooswitch (admin) :
   
        # sudo su -
2. Certaines distributions ont des dépendances à installer avant d’installer PostgreSQL. Vérifiez pour votre distribution dans cette liste et exécutez la commande appropriée hello :
   
   * Red Hat Linux :
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Debian Linux :
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * SUSE Linux :
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. Télécharger PostgreSQL dans le répertoire racine de hello et puis décompressez le package de hello :
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    Hello ci-dessus est un exemple. Vous pouvez trouver hello plus détaillées téléchargement adresse Bonjour [Indexde/pub/source/](https://ftp.postgresql.org/pub/source/).
4. génération de hello toostart, exécutez ces commandes :
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. Si vous souhaitez toobuild tout ce qui peut être générée, y compris la documentation de hello (pages HTML et man) et les modules complémentaires (cotisation), exécuter la commande suivante à la place de hello :
   
        # gmake install-world
   
    Vous devez recevoir hello message de confirmation suivant :
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>Configurer PostgreSQL
1. (Facultatif) Créer un hello tooshorten de lien symbolique PostgreSQL référence toonot inclure le numéro de version hello :
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. Créez un répertoire de base de données hello :
   
        # mkdir -p /opt/pgsql_data
3. Créez un utilisateur non-root et modifiez le profil de cet utilisateur. Ensuite, basculez toothis nouvel utilisateur (appelé *postgres* dans notre exemple) :
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > Pour des raisons de sécurité, PostgreSQL utilise un tooinitialize utilisateur non racine, démarrer ou arrêter la base de données hello.
   > 
   > 
4. Modifier hello *bash_profile* fichier en entrant les commandes hello ci-dessous. Ces lignes seront ajoutées fin toohello Hello *bash_profile* fichier :
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. Exécutez hello *bash_profile* fichier :
   
        $ source .bash_profile
6. Valider votre installation à l’aide de hello de commande suivante :
   
        $ which psql
   
    Si votre installation est réussie, vous verrez hello suivant la réponse :
   
        /opt/pgsql/bin/psql
7. Vous pouvez également vérifier la version de PostgreSQL hello :
   
        $ psql -V
8. Initialiser la base de données hello :
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    Vous devez recevoir hello suivant de sortie :

![image](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>Configurer PostgreSQL
<!--    [postgres@ test ~]$ exit -->

Exécutez hello suivant de commandes :

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

Modifiez les deux variables dans le fichier de /etc/init.d/postgresql hello. Hello préfixe a la valeur chemin d’installation de toohello de PostgreSQL : **pgsql/opt/**. PGDATA est défini de chemin d’accès de stockage de données toohello de PostgreSQL : **pgsql_data/opt/**.

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![image](./media/postgresql-install/no2.png)

Modifier hello fichier toomake il exécutable :

    # chmod +x /etc/init.d/postgresql

Démarrez PostgreSQL :

    # /etc/init.d/postgresql start

Vérifiez si le point de terminaison hello de PostgreSQL se trouve sur :

    # netstat -tunlp|grep 1999

Vous devez voir hello suivant de sortie :

![image](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>Connexion de base de données Postgres toohello
Basculer de nouveau toohello postgres utilisateur :

    # su - postgres

Créez une base de données Postgres :

    $ createdb events

Se connecter toohello événements de base de données que vous venez de créer :

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>Créer et supprimer une table Postgres
Maintenant que vous êtes connecté toohello de base de données, vous pouvez créer les tables qu’il contient.

Par exemple, créer une nouvelle table de Postgres exemple à l’aide de hello de commande suivante :

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

Vous avez défini un tableau de quatre colonnes avec hello suivant des noms de colonnes et restrictions :

1. Hello « name » une colonne a été limitée par hello VARCHAR commande toobe sous 20 caractères.
2. colonne de « produits alimentaires » Hello indique aliment hello chaque personne s’affiche. VARCHAR limite ce toobe texte sous 30 caractères.
3. Hello « confirmé « enregistrements de la colonne si personne de hello a auxquels elle répondu toohello buffet. les valeurs acceptables Hello sont « Y » et « N ».
4. affiche de colonne « date » de Hello lors de leur inscription pour l’événement de hello. Postgres requiert que les dates soient écrites au format aaaa-mm-jj.

Vous devez voir s’afficher hello si votre table a été créée avec succès :

![image](./media/postgresql-install/no4.png)

Vous pouvez également vérifier la structure de la table hello à l’aide de hello de commande suivante :

![image](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>Ajouter la table de données tooa
Insérez d’abord des informations dans une ligne :

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

Cette sortie doit s’afficher :

![image](./media/postgresql-install/no6.png)

Vous pouvez ajouter quelques plusieurs personnes toohello table également. Voici quelques propositions, mais vous pouvez créer vos propres informations :

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>Afficher les tables
Hello suivant commande tooshow une table, utilisez :

    select * from potluck;

sortie de Hello est :

![image](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>Supprimer des données dans une table
Utilisez hello données toodelete de commande dans une table suivantes :

    delete from potluck where name=’John’;

Cette opération supprime toutes les informations de hello Bonjour ligne de « John ». sortie de Hello est :

![image](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>Mettre à jour des données dans une table
Utilisez hello suivant données tooupdate de commande dans une table. Dans cet exemple, Sandy a confirmé qu’elle participe, donc nous allons changer son RSVP à partir de « N » trop « Y » :

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>Obtenez davantage d’informations sur PostgreSQL
Maintenant que vous avez terminé l’installation Bonjour de PostgreSQL dans une machine virtuelle Linux de Azure, vous pouvez profiter de l’utiliser dans Azure. toolearn en savoir plus sur PostgreSQL, visitez hello [site Web de PostgreSQL](http://www.postgresql.org/).

