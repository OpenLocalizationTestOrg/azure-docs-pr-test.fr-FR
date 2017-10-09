---
title: "Portail Azure : Créer une base de données Azure pour PostgreSQL | Microsoft Docs"
description: "Rapide toocreate du guide de démarrage et gérer la base de données Azure pour le serveur de PostgreSQL à l’aide d’interface utilisateur du portail Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: quickstart
ms.date: 08/10/2017
ms.openlocfilehash: 61753268147d6ea283d1aa5d6baf269d2756d25a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-in-hello-azure-portal"></a>Créer une base de données Azure PostgreSQL Bonjour portail Azure

Base de données Azure pour PostgreSQL est un service géré qui vous permet de toorun, gérer et mettre à l’échelle des bases de données PostgreSQL hautement disponibles dans le cloud de hello. Ce démarrage rapide vous montre comment toocreate Azure de base de données pour le serveur PostgreSQL à l’aide de hello portail Azure en cinq minutes environ.

Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="log-in-toohello-azure-portal"></a>Ouvrez une session dans toohello portail Azure
Ouvrez votre navigateur web et accédez toohello [portail Microsoft Azure](https://portal.azure.com/). Entrez vos informations d’identification toosign dans toohello portal. affichage par défaut de Hello est votre tableau de bord de service.

## <a name="create-an-azure-database-for-postgresql"></a>Créer une base de données Azure pour PostgreSQL

Un serveur de base de données Azure pour PostgreSQL est créé. Il contient un ensemble défini de [ressources de calcul et de stockage](./concepts-compute-unit-and-storage.md). serveur de Hello est créé dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md).

Suivez ces étapes de toocreate PostgreSQL server dans une base de données Azure :
1.  Cliquez sur hello **nouveau** bouton (+) sur le coin supérieur gauche hello Hello portail Azure.
2.  Sélectionnez **bases de données** de hello **nouveau** page, puis sélectionnez **base de données Azure pour PostgreSQL** de hello **bases de données** page.
 ![Base de données Azure pour PostgreSQL - créer la base de données hello](./media/quickstart-create-database-portal/1-create-database.png)

3.  Rempliront hello nouveau serveur détails avec hello suivant d’informations, comme indiqué dans le hello précédant l’image :

    Paramètre|Valeur suggérée|Description
    ---|---|---
    Nom du serveur |*mypgserver-20170401*|Choisissez un nom unique qui identifie votre serveur de base de données Azure pour PostgreSQL. nom de domaine Hello *postgres.database.azure.com* est ajouté toohello nom de serveur vous fournissez pour tooconnect d’applications pour. nom du serveur Hello peut contenir uniquement des lettres minuscules, des chiffres et des caractères de trait d’union (-) hello, et il doit contenir entre 3 et 63 caractères.
    Abonnement|*Votre abonnement*|Hello abonnement Azure que vous souhaitez toouse pour votre serveur. Si vous avez plusieurs abonnements, choisissez abonnement approprié de hello dans lequel les ressources hello sont facturé pour.
    Groupe de ressources|*myresourcegroup*| Vous pouvez définir un nouveau nom de groupe de ressources ou utiliser un nom de groupe existant dans votre abonnement.
    Connexion d’administrateur serveur |*mylogin*| Vérifiez votre propre toouse de compte de connexion lors de la connexion toohello server. nom de connexion Hello admin ne peut pas être 'azure_superuser', « azure_pg_admin », « admin », « administrateur », « root », 'invité' ou 'public' et ne peut pas commencer par 'pg_'.
    Mot de passe |*Votre choix* | Créer un nouveau mot de passe pour le compte d’administrateur serveur hello. Doit contenir entre 8 caractères too128. Votre mot de passe doit contenir des caractères appartenant à trois des hello suivant catégories : majuscules des lettres, des lettres minuscules, des chiffres (0-9) et des caractères non alphanumériques ( !, $, #, %, etc..).
    Lieu|*utilisateurs tooyour le plus proche Hello région*| Choisissez un emplacement hello qui est le plus proche tooyour utilisateurs.
    Version de PostgreSQL.|*Choisissez la version la plus récente hello*| Choisissez la version la plus récente hello, sauf si vous avez des exigences spécifiques.
    Niveau de tarification | **De base**, **50 unités de calcul****50 Go** | Cliquez sur **niveau tarifaire** toospecify hello performances et la couche de niveau de service pour votre nouvelle base de données. Choisissez le niveau de base dans l’onglet hello haut hello. Cliquez sur fin gauche hello hello unités de calcul curseur tooadjust hello valeur toohello minimum disponible pour ce démarrage rapide. Cliquez sur **Ok** hello toosave sélection de niveau de tarification. Consultez hello suivant capture d’écran.
    | Code confidentiel toodashboard | Vérification | Vérifiez hello **toodashboard du code confidentiel** option tooallow simplifier le suivi de votre serveur sur la page de tableau de bord avant hello de votre portail Azure.

  > [!IMPORTANT]
  > connexion administrateur de serveur Hello et un mot de passe que vous spécifiez ici sont requis toolog dans toohello server et ses bases de données plus loin dans ce guide de démarrage rapide. Retenez ou enregistrez ces informations pour une utilisation ultérieure.

    ![Base de données Azure pour PostgreSQL - hello choix niveau tarifaire](./media/quickstart-create-database-portal/2-service-tier.png)

4.  Cliquez sur **créer** serveur hello de tooprovision. Configuration prend quelques minutes, des too20 minutes maximum.

5.  Dans la barre d’outils de hello, cliquez sur **Notifications** processus de déploiement toomonitor hello.
 ![Base de données Azure pour PostgreSQL - Consulter les notifications](./media/quickstart-create-database-portal/3-notifications.png)
   
  Par défaut, la création de la base de données **postgres** intervient sous votre serveur. Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) base de données est une base de données par défaut destinée à une utilisation par les utilisateurs, les utilitaires et les applications tierces. 

## <a name="configure-a-server-level-firewall-rule"></a>Configurer une règle de pare-feu au niveau du serveur

Bonjour Azure de base de données PostgreSQL service crée un pare-feu au niveau serveur hello. Ce pare-feu empêche des applications externes et des outils de connexion toohello serveur et les bases de données sur le serveur de hello, sauf si une règle de pare-feu est créée le pare-feu tooopen hello pour des adresses IP spécifiques. 

1.  Localisez votre serveur une fois hello déploiement terminé. Si nécessaire, vous pouvez le rechercher. Par exemple, cliquez sur **toutes les ressources** de menu à gauche hello et tapez nom du serveur hello (exemple hello *mypgserver-20170401*) toosearch pour votre serveur nouvellement créé. Cliquez sur le nom de votre serveur répertorié dans les résultats de recherche hello. Hello **vue d’ensemble** pour votre serveur s’ouvre et fournit des options pour poursuivre la configuration de la page.
 
    ![Base de données Azure pour PostgreSQL - Rechercher le nom du serveur](./media/quickstart-create-database-portal/4-locate.png)

2.  Sur la page hello du serveur, sélectionnez **sécurité de connexion**. 
    ![Base de données Azure pour PostgreSQL - Créer une règle de pare-feu](./media/quickstart-create-database-portal/5-firewall-2.png)

3.  Sous hello **des règles de pare-feu** en-tête, cliquez dans la zone de texte vide hello Bonjour **nom de la règle** toobegin colonne création de règle de pare-feu hello. 

    Pour ce guide de démarrage rapide, nous allons autoriser toutes les adresses IP dans le serveur de hello en remplissant la zone de texte hello dans chaque colonne avec hello valeurs suivantes :

    Nom de la règle | Adresse IP de début | Adresse IP de fin 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Barre d’outils hello supérieur de la page de sécurité de connexion hello, cliquez sur **enregistrer**. Attendez quelques instants et message hello notification indiquant que la mise à jour de sécurité de connexion s’est correctement terminé avant de continuer.

    > [!NOTE]
    > Connexions tooyour Azure de base de données PostgreSQL serveur communiquent via le port 5432. Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 5432 ne peut pas être autorisé par le pare-feu de votre réseau. Dans ce cas, vous ne serez pas en mesure de tooconnect tooyour serveur, sauf si votre service informatique ouvre le port 5432.
    >

## <a name="get-hello-connection-information"></a>Obtenir des informations de connexion hello

Lorsque nous avons créé notre serveur de base de données Azure pour PostgreSQL, une base de données par défaut nommée **postgres** a été créée. serveur de base de données tooconnect tooyour, vous devez tooremember hello serveur complet administration et le nom d’identification. Il pouvez que vous avez noté ces valeurs plus haut dans l’article de démarrage rapide de hello. Dans le cas où vous n’avez pas, vous pouvez facilement trouver des informations de nom et de connexion de serveur à partir de la page Vue d’ensemble du serveur hello hello Bonjour portail Azure.

1. Ouvrez la page **Vue d’ensemble** de votre serveur. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.
    Placez votre curseur dans chaque champ et icône de copie hello s’affiche à droite de toohello de texte hello. Cliquez sur icône de copie hello en tant que valeurs de hello toocopy nécessaires.

 ![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/quickstart-create-database-portal/6-server-name.png)

## <a name="connect-toopostgresql-database-using-psql-in-cloud-shell"></a>Se connecter à l’aide de psql dans un environnement de Cloud de la base de données tooPostgreSQL

Il existe un certain nombre d’applications, vous pouvez utiliser tooconnect tooyour Azure de base de données PostgreSQL serveur. Nous allons d’abord utiliser hello psql utilitaire de ligne de commande tooillustrate comment tooconnect toohello server.  Vous pouvez utiliser un navigateur web et hello Azure Cloud Shell comme décrit ici sans hello doivent tooinstall des logiciels supplémentaires. Si vous avez hello psql utilitaire est installé localement sur votre propre ordinateur, vous pouvez vous connecter à partir de là également.

1. Lancez hello Azure Cloud Shell via l’icône de terminal hello sur le volet de navigation supérieure hello.

   ![Base de données Azure pour PostgreSQL - Icône de la console Azure Cloud Shell](./media/quickstart-create-database-portal/7-cloud-console.png)

2. Bonjour Azure Cloud Shell s’ouvre dans votre navigateur, l’activation de commandes d’environnement tootype bash.

   ![Base de données Azure pour PostgreSQL - Invite bash Azure Shell](./media/quickstart-create-database-portal/8-bash.png)

3. Invite hello Cloud, se connecter tooa de base de données dans votre base de données Azure pour PostgreSQL serveur en tapant la ligne de commande hello psql invite hello vert.

    Bonjour format suivant est utilisé tooconnect tooan base de données Azure pour serveur PostgreSQL avec hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilitaire :
    ```bash
    psql --host=<yourserver> --port=<port> --username=<server admin login> --dbname=<database name>
    ```

    Par exemple, hello commande suivante établit une connexion tooan exemple de serveur :

    ```bash
    psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
    ```

    Paramètre psql |Valeur suggérée|Description
    ---|---|---
    --host | *nom du serveur* | Spécifiez la valeur de nom de serveur hello utilisé lorsque vous avez créé précédemment des hello de base de données Azure pour PostgreSQL. L’exemple de serveur que nous utilisons ici est mypgserver-20170401.postgres.database.azure.com. Utilisez le nom de domaine complet hello (\*. postgres.database.azure.com) comme indiqué dans l’exemple de hello. Suivez les étapes de hello dans les informations de connexion du hello tooget de la section précédente hello si vous ne vous souvenez pas de nom de votre serveur. 
    --port | **5432** | Utilisez toujours le port 5432 lors de la connexion de base de données de tooAzure pour PostgreSQL. 
    --username | *nom de connexion d’administrateur du serveur* |Tapez hello server connexion nom d’utilisateur administrateur fourni lorsque vous avez créé précédemment des hello de base de données Azure pour PostgreSQL. Suivez les étapes de hello dans les informations de connexion du hello tooget de la section précédente hello si vous ne vous souvenez pas de nom d’utilisateur hello.  format de Hello est  *username@servername* .
    --dbname | **postgres** | Nom de base de données utilisez hello par défaut générée par le système *postgres* pour la première connexion de hello. Par la suite, vous créerez votre propre base de données.

    Après la commande de psql hello en cours d’exécution, avec vos propres valeurs de paramètre, vous êtes tootype demandées par invite de mot de passe hello server admin. Ce mot de passe est hello même que vous avez fourni lors de la création du serveur de hello. 

    Paramètre psql |Valeur suggérée|Description
    ---|---|---
    password | *votre mot de passe d’administrateur* | Notez, hello typé caractères ne figurent pas dans un interpréteur de commandes hello invite de mot de passe. Appuyez sur entrée une fois que vous avez tapé tous les tooauthenticate de caractères hello et vous connecter.

    Une fois connecté, utilitaire de psql hello affiche une invite de postgres où vous tapez des commandes sql. Dans la sortie de la connexion initiale hello, un avertissement peut être affiché comme psql hello Bonjour Azure Cloud Shell peut être différente de celle hello Azure de base de données pour la version du serveur PostgreSQL. 
    
    Exemple de sortie psql :
    ```bash
    psql (9.5.7, server 9.6.2)
    WARNING: psql major version 9.5, server major version 9.6.
        Some psql features might not work.
    SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
    Type "help" for help.
   
    postgres=> 
    ```

    > [!TIP]
    > Si le pare-feu hello n’est pas configuré les adresse IP tooallow hello hello Azure Cloud Shell, hello erreur suivante se produit :
    > 
    > "psql: FATAL:  aucune entrée pg_hba.conf pour l’hôte "138.91.195.82", utilisateur "mylogin", base de données "postgres", SSL sur FATAL :  Connexion SSL nécessaire. Veuillez spécifier les options SSL puis réessayez.
    > 
    > Erreur de hello tooresolve, vérifiez que hello server configuration correspondances hello étapes Bonjour *configurer une règle de pare-feu de niveau serveur* section de l’article de hello.

4.  Créer une base de données vide à hello invite de commandes en tapant hello de commande suivante :
    ```bash
    CREATE DATABASE mypgsqldb;
    ```
    commande Hello peut prendre quelques instants toocomplete. 

5.  À l’invite de hello, exécutez hello suivant de base de données de commande tooswitch connexion toohello nouvellement créé **mypgsqldb**.
    ```bash
    \c mypgsqldb
    ```

6.  Tapez \q et appuyez sur entrée tooquit psql. Vous pouvez fermer hello Azure Cloud Shell une fois que vous avez terminé.

Vous avez maintenant connecté toohello base de données Azure pour PostgreSQL et créé une base de données utilisateur vide. Continuer toohello tooconnect de section suivante à l’aide d’un autre outil commun, pgAdmin.

## <a name="connect-toopostgresql-database-using-pgadmin"></a>Se connecter à l’aide de pgAdmin de la base de données tooPostgreSQL

tooconnect tooAzure PostgreSQL serveur à l’aide d’outil d’interface utilisateur graphique de hello _pgAdmin_
1.  Lancez hello _pgAdmin_ application sur votre ordinateur client. Vous pouvez installer _pgAdmin_ à partir de http://www.pgadmin.org/.
2.  Cliquez sur hello **ajouter un nouveau serveur** icône de hello **liens rapides** section dans le centre de hello de page du tableau de bord hello.
3.  Bonjour **Create - Server** boîte de dialogue **général** , entrez un nom convivial unique pour le serveur de hello, tel que **Azure PostgreSQL Server**.
![Outil pgAdmin - Créer - Serveur](./media/quickstart-create-database-portal/9-pgadmin-create-server.png)
4.  Bonjour **Create - Server** boîte de dialogue, **connexion** onglet, utilisez les paramètres hello spécifié et cliquez sur **enregistrer**.
   ![pgAdmin - Créer - Serveur](./media/quickstart-create-database-portal/10-pgadmin-create-server.png)

    Paramètre pgAdmin |Valeur suggérée|Description
    ---|---|---
    Nom/adresse de l’hôte | *nom du serveur* | Spécifiez la valeur de nom de serveur hello utilisé lorsque vous avez créé précédemment des hello de base de données Azure pour PostgreSQL. L’exemple de serveur que nous utilisons ici est mypgserver-20170401.postgres.database.azure.com. Utilisez le nom de domaine complet hello (\*. postgres.database.azure.com) comme indiqué dans l’exemple de hello. Suivez les étapes de hello dans les informations de connexion du hello tooget de la section précédente hello si vous ne vous souvenez pas de nom de votre serveur. 
    Port | **5432** | Utilisez toujours le port 5432 lors de la connexion de base de données de tooAzure pour PostgreSQL.  
    Base de données de maintenance | **postgres** | Nom de base de données utilisez hello par défaut générée par le système *postgres*.
    User Name | *nom de connexion d’administrateur du serveur* | Tapez hello server connexion nom d’utilisateur administrateur fourni lorsque vous avez créé précédemment des hello de base de données Azure pour PostgreSQL. Suivez les étapes de hello dans les informations de connexion du hello tooget de la section précédente hello si vous ne vous souvenez pas de nom d’utilisateur hello. format de Hello est  *username@servername* .
    Mot de passe | *votre mot de passe d’administrateur* |  mot de passe Hello vous avez choisi lorsque vous avez créé le serveur de hello plus haut dans ce démarrage rapide.
    Rôle | *Laisser vide* | Ne doivent tooprovide un rôle de nom à ce stade. Renseignez le champ de hello.
    Mode SSL | Require | Par défaut, tous les serveurs Azure PostgreSQL sont créés avec l’application du SSL activée. tooturn hors tension de l’application de SSL, consultez les détails dans [SSL de l’application](./concepts-ssl-connection-security.md).
    
5.  Cliquez sur **Enregistrer**.
6.  Dans le volet gauche du navigateur hello, développez hello **serveurs** nœud. Sélectionnez votre serveur, par exemple **Azure PostgreSQL serveur** et cliquez sur tooconnect tooit.
7. Développez le nœud du serveur hello et puis **bases de données** sous celle-ci. Hello liste doit inclure vos *postgres* base de données et n’importe quel utilisateur nouvellement créé de base de données, tel que *mypgsqldb*, que vous avez créée dans la section précédente de hello. Remarque : vous pouvez créer plusieurs bases de données par serveur avec la base de données Azure pour PostgreSQL.
8. Avec le bouton droit sur **bases de données**, choisissez hello **créer** menu, puis cliquez sur **base de données**.
9.  Tapez un nom de base de données de votre choix dans hello **base de données** champ, tels que *mypgsqldb* hello illustré. 
10. Sélectionnez hello **propriétaire** de base de données hello à partir de la zone de liste déroulante hello. Choisissez le nom de connexion d’administrateur du serveur, par exemple *mylogin*.
10. Cliquez sur **enregistrer** toocreate une base de données vide.
11. Bonjour **navigateur** volet, consultez hello de base de données vous avez créé dans la liste hello des bases de données sous le nom de votre serveur.
 ![pgAdmin - Créer - Base de données](./media/quickstart-create-database-portal/11-pgadmin-database.png)


## <a name="clean-up-resources"></a>Supprimer des ressources
Nettoyer les ressources hello vous avez créé dans démarrage rapide de hello soit en supprimant hello [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md), qui inclut toutes les ressources hello dans le groupe de ressources hello ou en supprimant des ressources d’un serveur hello si vous souhaitez tookeep hello autres ressources intacts.

> [!TIP]
> Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide. Si vous prévoyez toocontinue toowork avec ultérieures Démarrages rapides, effectuez pas nettoyer les hello ressources créées dans ce démarrage rapide. Si vous n’envisagez pas de toocontinue, utilisez hello suivant les ressources de toodelete étapes créées par ce démarrage rapide Bonjour portail Azure.

groupe de ressource entier hello toodelete y compris les serveur hello nouvellement créé :
1.  Bonjour portail Azure, recherchez votre groupe de ressources. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur le nom de votre groupe de ressources, telles que notre exemple hello du **myresourcegroup**.
2.  Sur la page de votre groupe de ressources, cliquez sur **Supprimer**. Puis hello nom du type de votre groupe de ressources, telles que notre exemple **myresourcegroup**, en hello suppression de tooconfirm de zone de texte, puis cliquez sur **supprimer**.

Ou, au lieu de cela, toodelete hello créé récemment serveur :
1.  Localisez votre serveur Bonjour portail Azure, si vous ne pas les connaissez ouvrir. Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources**, puis recherchez serveur hello vous avez créé.
2.  Sur hello **vue d’ensemble** , cliquez sur hello **supprimer** bouton dans le volet supérieur de hello.
![Base de données Azure pour PostgreSQL : Supprimer le serveur](./media/quickstart-create-database-portal/12-delete.png)
3.  Confirmez le nom du serveur hello souhaité toodelete, afficher hello bases de données dans cette section sont affectées. Tapez le nom de votre serveur dans la zone de texte hello, tels que notre exemple **mypgserver-20170401**, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./howto-migrate-using-export-and-import.md)
