---
title: "aaaConnect tooSQL de la base de données à l’aide de C et C++ | Documents Microsoft"
description: "Exemple de hello d’utilisation de code dans ce démarrage rapide de toobuild une application moderne avec C++ et soutenu par une puissante base de données relationnelle dans le cloud de hello avec la base de données SQL Azure."
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a>Se connecter tooSQL de base de données à l’aide de C et C++
Cette publication est destinée aux développeurs C et C++, la tentative de tooconnect tooAzure base de données SQL. Il est vous divisé en sections, vous pouvez passer la section toohello qui capture les mieux votre intérêt. 

## <a name="prerequisites-for-hello-cc-tutorial"></a>Configuration requise pour le didacticiel de C/C++ hello
Vérifiez que vous avez hello éléments suivants :

* Un compte Azure actif. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit des services Azure](https://azure.microsoft.com/pricing/free-trial/)dès aujourd’hui.
* [Visual Studio](https://www.visualstudio.com/downloads/). Vous devez installer hello C++ language composants toobuild et exécuter cet exemple.
* [Développement Visual Studio Linux](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e). Si vous développez sur Linux, vous devez également installer l’extension de Visual Studio Linux hello. 

## <a id="AzureSQL"></a>Azure SQL Database et SQL Server sur les machines virtuelles
SQL Azure repose sur Microsoft SQL Server et est conçue tooprovide une haute disponibilité, performant et évolutive des services. Il existe de nombreux avantages toousing SQL Azure sur votre base de données propriétaire en cours d’exécution en local. Avec SQL Azure vous ne tooinstall, configurer, gérer ou gérer votre base de données, mais uniquement hello contenu et de structure hello de votre base de données. Les capacités de base de données importantes, telles que la tolérance de panne et la redondance, sont intégrées. 

Azure propose actuellement deux options pour l’hébergement des charges de travail SQL Server : Azure SQL Database, qui fournit une base de données en tant que service, et SQL Server sur les machines virtuelles. Nous allons pas dans les détails sur les différences de hello entre ces deux sauf que la base de données SQL Azure est la meilleure solution pour parti de tootake nouvelles applications basées sur le cloud de hello réduction des coûts et fournissent des services de cloud computing optimisation des performances. Si vous envisagez de migrer ou d’étendre votre service cloud de toohello d’applications, SQL server sur une machine virtuelle Azure peut être plus appropriée pour vous. tookeep plus simple pour cet article, nous allons créer une base de données SQL Azure. 

## <a id="ODBC"></a>Technologies d’accès aux données : ODBC et OLE DB
Connexion tooAzure de base de données SQL n’est pas différent et actuellement il existe deux façons tooconnect toodatabases : ODBC (Open Database connectivity) et OLE DB (base de données de liaison et incorporation). Ces dernières années, Microsoft s’est aligné sur [ODBC pour l’accès aux données relationnelles natives](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/). ODBC est relativement simple, mais aussi beaucoup plus rapide qu’OLE DB. Hello attentif ici est que ODBC utilise une API C-style ancien. 

## <a id="Create"></a>Étape 1 : création de votre base de données SQL Azure
Consultez hello [page mise en route](sql-database-get-started-portal.md) toolearn comment toocreate une base de données exemple.  Vous pouvez également suivre ce [courte vidéo de deux minutes](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) une base de données SQL Azure à l’aide de toocreate hello portail Azure.

## <a id="ConnectionString"></a>Étape 2 : obtention de la chaîne de connexion
Après la configuration de votre base de données SQL Azure, vous devez toocarry out hello informations de connexion toodetermine étapes suivantes et ajoutez votre adresse IP du client pour l’accès de pare-feu. 

Dans [portail Azure](https://portal.azure.com/), passez la chaîne de connexion ODBC tooyour SQL Azure de base de données à l’aide de hello **afficher les chaînes de connexion de base de données** répertoriés dans le cadre de la section vue d’ensemble de hello pour votre base de données : 

![Chaîne de connexion ODBC](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![Propriétés de la chaîne de connexion ODBC](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

Copier le contenu de hello Hello **ODBC (inclut Node.js) [authentification SQL]** chaîne. Nous utilisons cette chaîne tooconnect ultérieur à partir de notre interpréteur de ligne de commande C++ ODBC. La chaîne contient des détails tels que les pilotes de hello, serveur et autres paramètres de connexion de base de données. 

## <a id="Firewall"></a>Étape 3 : Ajoutez votre pare-feu de toohello IP
Section toohello du pare-feu pour votre serveur de base de données, ajoutez votre [pare-feu toohello de client IP à l’aide de ces étapes](sql-database-configure-firewall-settings.md) toomake que nous pouvons établir une connexion réussie : 

![Fenêtre d’ajout de l’adresse IP](./media/sql-database-develop-cplusplus-simple/ip.png)

À ce stade, vous avez configuré votre base de données SQL Azure et sont tooconnect prêt à partir de votre code C++. 

## <a id="Windows"></a>Étape 4 : connexion à partir d’une application C/C++ Windows
Vous pouvez facilement connecter tooyour [base de données SQL Azure à l’aide de ODBC sur Windows à l’aide de cet exemple](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) qui génère avec Visual Studio. exemple Hello implémente un interpréteur de ligne de commande ODBC qui peut être utilisés tooconnect tooour base de données SQL Azure. Cet exemple prend soit un fichier de fichier (DSN) de nom de source de base de données comme un argument de ligne de commande ou une chaîne de connexion documentée hello que nous copiées précédemment à partir de hello portail Azure. Afficher la page de propriétés hello pour ce projet et collez la chaîne de connexion hello en tant qu’argument de commande, comme indiqué ici : 

![Fichier de propriétés DSN](./media/sql-database-develop-cplusplus-simple/props.png)

Vérifiez que vous fournissez des informations d’authentification approprié hello pour votre base de données dans le cadre de cette chaîne de connexion de base de données. 

Lancez hello application toobuild il. Vous devez voir hello suivant la fenêtre de validation d’une connexion réussie. Vous pouvez même exécuter des commandes SQL de base comme **create table** toovalidate la connectivité de base de données :

![Commandes SQL](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

Ou bien, vous pouvez créer un fichier de source de données à l’aide d’Assistant hello qui s’affiche lorsque aucun argument de commande n’est fournis. Nous vous recommandons d’essayer également cette option. Vous pouvez utiliser ce fichier DSN à des fins d’automatisation et pour protéger vos paramètres d’authentification : 

![Création d’un fichier DSN](./media/sql-database-develop-cplusplus-simple/datasource.png)

Félicitations ! Vous avez maintenant correctement connecté tooAzure SQL à l’aide de C++ et ODBC sur Windows. Vous pouvez continuer la lecture toodo même hello pour la plate-forme Linux ainsi. 

## <a id="Linux"></a>Étape 5 : connexion à partir d’une application C/C++ Linux
Dans le cas où vous n’avez pas entendu news de hello encore, Visual Studio vous permet désormais toodevelop ainsi les applications Linux C++. Vous pouvez lire sur ce nouveau scénario Bonjour [Visual C++ pour le développement Linux](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog. toobuild pour Linux, vous devez un ordinateur distant où votre distribution Linux est en cours d’exécution. Si vous n’en avez pas, vous pouvez en configurer un rapidement à l’aide de [machines virtuelles Azure Linux](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Pour ce didacticiel, nous partirons du principe que vous disposez d’une distribution Linux Ubuntu 16.04. étapes Hello ici doivent s’appliquer également tooUbuntu 15.10, Red Hat 6 et Red Hat 7. 

Hello suit installer les bibliothèques hello nécessaires pour SQL et ODBC pour votre distribution :

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

Lancez Visual Studio. Sous Outils -> Options -> multiplateforme -> Gestionnaire de connexions, ajoutez une zone de Linux tooyour connexion : 

![Outils > Options](./media/sql-database-develop-cplusplus-simple/tools.png)

Une fois la connexion via SSH établie, créez un modèle de projet vide (Linux) : 

![Nouveau modèle de projet](./media/sql-database-develop-cplusplus-simple/template.png)

Vous pouvez ensuite ajouter un [nouveau fichier source C et le remplacer par ce contenu](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c). À l’aide de hello SQLAllocHandle d’API ODBC et SQLSetConnectAttr SQLDriverConnect, vous devez être en mesure de tooinitialize et établir une connexion de données tooyour. Comme avec hello, exemple ODBC de Windows, vous devez appel de SQLDriverConnect hello tooreplace avec les détails de hello à partir de vos paramètres de chaîne de connexion de base de données copiée précédemment à partir de hello portail Azure. 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

Hello dernière chose toodo avant la compilation est tooadd **odbc** comme une dépendance de bibliothèque : 

![Ajout d’ODBC en tant que bibliothèque d’entrée](./media/sql-database-develop-cplusplus-simple/lib.png)

toolaunch votre application, afficher hello Linux Console à partir de hello **déboguer** menu : 

![Console Linux](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

Si votre connexion a réussi, vous devez maintenant voir le nom de base de données actuel hello imprimé Bonjour Linux Console : 

![Sortie de la fenêtre de la Console Linux](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

Félicitations ! Vous avez terminé avec succès le didacticiel de hello et pouvez maintenant se connecter tooyour base de données SQL Azure à partir de C++ sur les plateformes Windows et Linux.

## <a id="GetSolution"></a>Obtenir la solution didacticiel hello complète C/C++
Vous pouvez trouver des solutions GetStarted hello qui contient tous les exemples hello dans cet article dans github :

* [Exemple ODBC C++ Windows](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), télécharger hello Windows C++ ODBC Sample tooconnect tooAzure SQL
* [Exemple de ODBC C++ Linux](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), télécharger hello Linux C++ ODBC Sample tooconnect tooAzure SQL

## <a name="next-steps"></a>Étapes suivantes
* Hello de révision [vue d’ensemble du développement de base de données SQL](sql-database-develop-overview.md)
* Plus d’informations sur hello [référence de l’API ODBC](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)

## <a name="additional-resources"></a>Ressources supplémentaires
* [Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* Explorer tous les hello [fonctionnalités de base de données SQL](https://azure.microsoft.com/services/sql-database/)

