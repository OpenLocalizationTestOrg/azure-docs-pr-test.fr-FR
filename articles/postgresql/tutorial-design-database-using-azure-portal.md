---
title: "Concevoir votre première base de données Azure pour PostgreSQL avec le portail Azure | Microsoft Docs"
description: "Ce didacticiel montre comment tooDesign votre première Azure de base de données PostgreSQL à l’aide de hello portail Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: fde7e9d1ae2bad4291d18bebd3356f4f8a2ac86a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-hello-azure-portal"></a>Concevoir votre première base de données Azure pour PostgreSQL à l’aide de hello portail Azure

Base de données Azure pour PostgreSQL est un service géré qui vous permet de toorun, gérer et mettre à l’échelle des bases de données PostgreSQL hautement disponibles dans le cloud de hello. À l’aide de hello portail Azure, vous pouvez facilement gérer votre serveur et concevoir une base de données.

Dans ce didacticiel, vous utilisez comment hello toolearn portail Azure pour :
> [!div class="checklist"]
> * Créer une base de données Azure pour PostgreSQL
> * Configurer le pare-feu du serveur hello
> * Utilisez [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilitaire toocreate une base de données
> * Charger les exemples de données
> * Données de requête
> * Mettre à jour des données
> * Restaurer des données

## <a name="prerequisites"></a>Composants requis
Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="log-in-toohello-azure-portal"></a>Ouvrez une session dans toohello portail Azure
Connectez-vous à toohello [portail Azure](https://portal.azure.com).

## <a name="create-an-azure-database-for-postgresql"></a>Créer une base de données Azure pour PostgreSQL

Un serveur de base de données Azure pour PostgreSQL est créé. Il contient un ensemble défini de [ressources de calcul et de stockage](./concepts-compute-unit-and-storage.md). serveur de Hello est créé dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md).

Suivez ces étapes de toocreate PostgreSQL server dans une base de données Azure :
1.  Cliquez sur hello **+ nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.
2.  Sélectionnez **bases de données** de hello **nouveau** page, puis sélectionnez **base de données Azure pour PostgreSQL** de hello **bases de données** page.
 ![Base de données Azure pour PostgreSQL - créer la base de données hello](./media/tutorial-design-database-using-azure-portal/1-create-database.png)

3.  Rempliront hello nouveau serveur détails avec hello suivant d’informations, comme indiqué dans le hello précédant l’image :
    - Nom du serveur : **mypgserver-20170401** (nom d’un serveur mappe le nom de tooDNS et est donc requis toobe global unique) 
    - L’abonnement : Si vous avez plusieurs abonnements, choisissez abonnement approprié de hello dans lequel les ressources hello existent ou sont facturé pour.
    - Groupe de ressources : **myresourcegroup**.
    - Connexion d’administrateur du serveur et mot de passe de votre choix.
    - Lieu
    - Version de PostgreSQL.

  > [!IMPORTANT]
  > connexion administrateur de serveur Hello et un mot de passe que vous spécifiez ici sont requis toolog dans toohello server et ses bases de données plus loin dans ce guide de démarrage rapide. Retenez ou enregistrez ces informations pour une utilisation ultérieure.

4.  Cliquez sur **niveau tarifaire** toospecify hello performances et la couche de niveau de service pour votre nouvelle base de données. Pour ce guide de démarrage rapide, choisissez le niveau **De base**, **50 unités de calcul** et **50 Go** de stockage inclus.
 ![Base de données Azure pour PostgreSQL - niveau de service hello choix](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)
5.  Cliquez sur **OK**.
6.  Cliquez sur **créer** serveur hello de tooprovision. L’approvisionnement prend quelques minutes.

  > [!TIP]
  > Vérifiez hello **toodashboard du code confidentiel** option tooallow simplifier le suivi de vos déploiements.

7.  Dans la barre d’outils de hello, cliquez sur **Notifications** processus de déploiement toomonitor hello.
 ![Base de données Azure pour PostgreSQL - Consulter les notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)
   
  Par défaut, la création de la base de données **postgres** intervient sous votre serveur. Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) base de données est une base de données par défaut destinée à une utilisation par les utilisateurs, les utilitaires et les applications tierces. 

## <a name="configure-a-server-level-firewall-rule"></a>Configurer une règle de pare-feu au niveau du serveur

Bonjour Azure de base de données PostgreSQL service crée un pare-feu au niveau serveur hello. Ce pare-feu empêche des applications externes et des outils de se connecter toutes les bases de données sur le serveur de hello et toohello, sauf si une règle de pare-feu est créée le pare-feu tooopen hello pour des adresses IP spécifiques. 

1.  Une fois le déploiement de hello terminé, cliquez sur **toutes les ressources** de menu à gauche hello et tapez le nom de hello **mypgserver-20170401** toosearch pour votre serveur nouvellement créé. Cliquez sur le nom du serveur hello répertorié dans les résultats de recherche hello. Hello **vue d’ensemble** pour votre serveur s’ouvre et fournit des options pour poursuivre la configuration de la page.
 
 ![Base de données Azure pour PostgreSQL - Rechercher le serveur ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  Dans le panneau de serveur hello, sélectionnez **sécurité de connexion**. 
3.  Cliquez dans la zone de texte hello sous **nom de la règle,** et ajoutez une nouvelle pare-feu règle toowhitelist hello plages IP pour la connectivité. Pour ce didacticiel, nous allons autoriser toutes les adresses IP. Pour cela, tapez **Nom de la règle = AllowAllIps** ,  **= 0.0.0.0** et **= 255.255.255.255** , puis cliquez sur **Enregistrer**. Vous pouvez définir une règle de pare-feu qui couvre une tooconnect IP plage toobe en mesure de votre réseau.
 
 ![Base de données Azure pour PostgreSQL - Créer une règle de pare-feu](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  Cliquez sur **enregistrer** puis cliquez sur hello **X** tooclose hello **sécurité des connexions** page.

  > [!NOTE]
  > Le serveur Azure PostgreSQL communique sur le port 5432. Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 5432 ne peut pas être autorisé par le pare-feu de votre réseau. Dans ce cas, vous ne serez pas de serveur de base de données SQL Azure en mesure de tooconnect tooyour, sauf si votre service informatique ouvre le port 5432.
  >


## <a name="get-hello-connection-information"></a>Obtenir des informations de connexion hello

Lorsque nous avons créé notre base de données Azure pour le serveur de PostgreSQL, hello par défaut **postgres** base de données est également créé. serveur de base de données tooconnect tooyour, vous devez tooprovide hôte accéder aux informations et informations d’identification.

1. Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous venez de créer **mypgserver-20170401**.

  ![Base de données Azure pour PostgreSQL - Rechercher le serveur ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. Cliquez sur le nom du serveur hello **mypgserver-20170401**.
4. Serveur hello sélectionnez **vue d’ensemble** page. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.

 ![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-toopostgresql-database-using-psql-in-cloud-shell"></a>Se connecter à l’aide de psql dans un environnement de Cloud de la base de données tooPostgreSQL

Nous allons maintenant utiliser hello psql utilitaire de ligne de commande tooconnect toohello Azure de base de données PostgreSQL serveur. 
1. Lancez hello Azure Cloud Shell via l’icône de terminal hello sur le volet de navigation supérieure hello.

   ![Base de données Azure pour PostgreSQL - Icône de la console Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. Bonjour Azure Cloud Shell s’ouvre dans votre navigateur, ce qui vous tootype bash commandes.

   ![Base de données Azure pour PostgreSQL - Invite bash Azure Shell](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. Invite hello Cloud, se connecter tooyour base de données Azure pour le serveur PostgreSQL à l’aide des commandes de psql hello. Bonjour format suivant est utilisé tooconnect tooan base de données Azure pour serveur PostgreSQL avec hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilitaire :
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   Par exemple, hello commande suivante connecte à base de données de la valeur par défaut toohello appelée **postgres** sur votre serveur PostgreSQL **mypgserver-20170401.postgres.database.azure.com** à l’aide des informations d’identification d’accès. À l’invite, entrez votre mot de passe d’administrateur du serveur.

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a>Créer une base de données
Une fois que vous êtes connecté toohello server, créez une base de données vide à l’invite de hello.
```bash
CREATE DATABASE mypgsqldb;
```

À l’invite de hello, exécutez hello suivant de base de données de commande tooswitch connexion toohello nouvellement créé **mypgsqldb**.
```bash
\c mypgsqldb
```
## <a name="create-tables-in-hello-database"></a>Créer des tables dans la base de données hello
Maintenant que vous savez comment tooconnect toohello base de données Azure pour PostgreSQL, nous pouvons sur la façon toocomplete certaines tâches de base.

Tout d’abord, nous pouvons créer une table et y charger des données. Nous allons créer une table qui assure le suivi des informations d’inventaire.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

Vous pouvez voir hello nouvellement créé table dans la liste hello de tabvles maintenant en tapant :
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Charger des données dans les tables de hello
Maintenant que nous disposons d’une table, nous pouvons y insérer des données. Au niveau de la fenêtre d’invite de commandes ouverte hello, exécutez hello suivant requête tooinsert certaines lignes de données
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Vous avez maintenant deux lignes d’exemples de données dans la table hello que vous avez créé précédemment.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Interroger et mettre à jour les données hello dans les tables de hello
Exécutez hello suivant tooretrieve les informations de requête à partir de la table de base de données hello. 
```sql
SELECT * FROM inventory;
```

Vous pouvez également mettre à jour les données hello dans les tables de hello
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

ligne de Hello est mise à jour en conséquence lorsque vous récupérez des données.
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-tooa-previous-point-in-time"></a>Restaurer le point de données tooa précédent dans le temps
Imaginez que vous avez supprimé cette table par erreur. La récupération dans ce cas n’est pas simple. Base de données Azure pour PostgreSQL vous permet de toogo tooany arrière dans le temps (en hello dernière too7 jours (Basic) et de 35 jours (Standard)) et de restauration ce point-à-temps tooa nouveau serveur. Les données supprimées, vous pouvez utiliser cette nouvelle toorecover de serveur. Hello suivant étapes restauration hello exemple server tooa point avant hello table a été ajoutée.

1.  Dans hello Azure de base de données pour la page PostgreSQL pour votre serveur, cliquez sur **restaurer** sur la barre d’outils hello. Hello **restaurer** ouvrir la page.
  ![Portail Azure - Options du formulaire de restauration](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)
2.  Remplir hello **restaurer** formulaire avec les informations de hello requis :

  ![Portail Azure - Options du formulaire de restauration](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - **Point de restauration**: sélectionnez un point dans le temps qui se produit avant que le serveur de hello a été modifié
  - **Serveur cible**: fournir un nouveau nom du serveur toorestore à
  - **Emplacement**: vous ne pouvez pas sélectionner la région de hello, par défaut, il est identique au serveur de source de hello
  - **Niveau tarifaire** : vous ne pouvez pas modifier cette valeur lors de la restauration d’un serveur. Il est identique au serveur de source de hello. 
3.  Cliquez sur **OK** toorestore hello server trop[tooa point-à-temps de restauration](./howto-restore-server-portal.md) avant la suppression de tables de hello. Restauration d’un point différent de tooa de serveur dans le temps crée un nouveau serveur en double en tant que serveur d’origine de hello en tant que point hello dans le temps, vous spécifiez, autant qu’il soit dans la période de rétention hello pour votre [niveau de service](./concepts-service-tiers.md).

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toouse hello portail Azure et autres utilitaires pour :
> [!div class="checklist"]
> * Créer une base de données Azure pour PostgreSQL
> * Configurer le pare-feu du serveur hello
> * Utilisez [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilitaire toocreate une base de données
> * Charger les exemples de données
> * Données de requête
> * Mettre à jour des données
> * Restaurer des données

Ensuite, découvrez comment toouse CLI d’Azure toodo des tâches similaires, passez en revue ce didacticiel : [concevoir votre première base de données Azure pour PostgreSQL à l’aide de CLI d’Azure](tutorial-design-database-using-azure-cli.md)
