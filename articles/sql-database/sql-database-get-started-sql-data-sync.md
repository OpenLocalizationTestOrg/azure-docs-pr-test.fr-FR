---
title: "aaaGetting main de la synchronisation des données SQL Azure (version préliminaire) | Documents Microsoft"
description: "Ce didacticiel décrit la prise en main d’Azure SQL Data Sync (version préliminaire)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a>Prise en main d’Azure SQL Data Sync (version préliminaire)
Dans ce didacticiel, vous découvrez comment tooset de synchronisation des données SQL Azure en créant un groupe de synchronisation hybride qui contient des instances de base de données SQL Azure et SQL Server. nouveau groupe de synchronisation Hello est entièrement configuré et synchronise sur Planification hello définie.

Ce didacticiel suppose que vous ayez déjà utilisé SQL Database et SQL Server. 

Pour une vue d’ensemble de SQL Data Sync, consultez la section [Synchronisation des données](sql-database-sync-data.md).

Pour obtenir des exemples PowerShell complets qui montrent comment tooconfigure synchronisation des données SQL, consultez hello suivant des articles :
-   [Utilisez toosync PowerShell entre plusieurs bases de données SQL Azure](scripts/sql-database-sync-data-between-sql-databases.md)
-   [Utilisez toosync PowerShell entre une base de données SQL Azure et une base de données locale SQL Server](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> Hello technique documentation complète pour la synchronisation des données SQL Azure, anciennement situé sur le site MSDN, est disponible en tant qu’un. Document PDF. Téléchargez-le [ici](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).

## <a name="step-1---create-sync-group"></a>Étape 1 : créer un groupe de synchronisation

### <a name="locate-hello-data-sync-settings"></a>Localiser les paramètres de synchronisation des données hello

1.  Dans votre navigateur, accédez à toohello portail Azure.

2.  Dans le portail hello, localisez vos bases de données SQL à partir de votre tableau de bord ou à partir de l’icône de bases de données SQL hello sur la barre d’outils hello.

    ![Liste des bases de données SQL Azure](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  Sur hello **bases de données SQL** panneau, sélectionnez hello base de données SQL que vous souhaitez toouse comme base de données concentrateur hello pour synchronisation de données. Panneau de base de données SQL hello s’ouvre.

4.  Dans le panneau de base de données hello SQL pour la base de données sélectionnée hello, sélectionnez **synchroniser les bases de données tooother**. Panneau de synchronisation des données Hello s’ouvre.

    ![Option de bases de données de synchronisation tooother](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a>Créer un groupe de synchronisation

1.  Dans le panneau de la synchronisation des données hello, sélectionnez **nouveau groupe de synchronisation**. Hello **nouveau groupe de synchronisation** panneau s’ouvre à l’étape 1, **créer un groupe de synchronisation**, mise en surbrillance. Hello **créer un groupe de synchronisation de données** panneau s’ouvre également.

2.  Sur hello **créer un groupe de synchronisation de données** panneau, hello suivants choses :

    1.  Bonjour **nom du groupe de synchronisation** , entrez un nom pour le nouveau groupe de synchronisation hello.

    2.  Bonjour **base de données de métadonnées de synchronisation** , choisissez si toocreate une base de données (recommandé) ou toouse une base de données existant.

        > [!NOTE]
        > Microsoft recommande de créer un toouse de base de données vide comme hello de base de données de métadonnées de synchronisation. SQL Data Sync crée les tables dans cette base de données et exécute une charge de travail fréquente. Cette base de données est automatiquement partagé en tant que hello de base de données de synchronisation des métadonnées pour tous vos groupes de synchronisation dans une région de hello sélectionnée. Vous ne pouvez pas modifier hello de base de données de synchronisation des métadonnées, son nom ou son niveau de service sans le déposer.

        Si vous avez choisi **Nouvelle base de données**, sélectionnez **Créer une nouvelle base de données.** Hello **base de données SQL** panneau s’ouvre. Sur hello **base de données SQL** panneau, nommez et configurer la nouvelle base de données hello. Sélectionnez ensuite **OK**.

        Si vous avez choisi **utiliser la base de données existante**, sélectionnez base de données hello à partir de la liste de hello.

    3.  Bonjour **Sync automatique** , sélectionnez tout d’abord **sur** ou **hors**.

        Si vous avez choisi **sur**, Bonjour **fréquence de synchronisation** section, entrez un nombre et sélectionnez secondes, Minutes, heures ou jours.

        ![Spécifier la fréquence de synchronisation](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  Bonjour **la résolution des conflits** , sélectionnez le « wins Hub » ou « Wins de membre ».

        ![Spécifier le mode de résolution des conflits](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  Sélectionnez **OK** et attendez hello nouvelle synchronisation groupe toobe créés et déployés.

## <a name="step-2---add-sync-members"></a>Étape 2 : ajouter des membres de synchronisation

Une fois le nouveau groupe de synchronisation hello est créé et déployé, l’étape 2, **ajouter des membres de la synchronisation**, est mis en surbrillance dans hello **nouveau groupe de synchronisation** panneau.

Bonjour **base de données concentrateur** section, entrez les informations d’identification existantes hello hello de base de données SQL server sur le hello hub base de données. N’entrez pas de *nouvelles* informations d’identification dans cette section.

![Base de données concentrateur a été ajouté toosync groupe](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a>Ajouter une base de données SQL Azure Database

Bonjour **base de données membre** section, vous pouvez également ajouter un groupe de synchronisation de base de données SQL Azure toohello en sélectionnant **ajouter une base de données Azure**. Hello **configurer la base de données Azure** panneau s’ouvre.

Sur hello **configurer la base de données Azure** panneau, hello suivants choses :

1.  Bonjour **nom du membre de synchronisation** champ, fournissez un nom pour le nouveau membre de synchronisation hello. Ce nom est différent de nom hello de base de données hello lui-même.

2.  Bonjour **abonnement** hello, sélectionnez associés à un abonnement Azure à des fins de facturation.

3.  Bonjour **Azure SQL Server** serveur de base de données SQL existante, sélectionnez hello.

4.  Bonjour **base de données SQL Azure** hello, sélectionnez base de données SQL.

5.  Bonjour **Directions de synchronisation** , sélectionnez la synchronisation bidirectionnelle, toohello concentrateur, ou à partir de hello Hub.

    ![Ajout d’un nouveau membre de synchronisation SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  Bonjour **nom d’utilisateur** et **mot de passe** , saisissez les informations d’identification existantes hello pour hello de base de données SQL server sur le hello membre base de données. N’entrez pas de *nouvelles* informations d’identification dans cette section.

7.  Sélectionnez **OK** et attendez hello nouvelle synchronisation membre toobe créés et déployés.

    ![Nouveau membre de synchronisation SQL Database ajouté](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a>Ajouter une base de données SQL Server locale

Bonjour **base de données membre** section éventuellement ajouter un groupe de synchronisation toohello SQL Server local en sélectionnant **ajouter une base de données local**. Hello **configurer On-Premises** panneau s’ouvre.

Sur hello **configurer On-Premises** panneau, hello suivants choses :

1.  Sélectionnez **choisir hello passerelle de l’Agent de synchronisation**. Hello **sélectionnez l’Agent de synchronisation** panneau s’ouvre.

    ![Choisissez la passerelle de l’agent de synchronisation hello](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  Sur hello **choisir hello passerelle de l’Agent de synchronisation** panneau, choisissez si toouse un agent existant ou créer un nouvel agent.

    Si vous avez choisi **les agents existants**, sélectionnez hello agent existant à partir de la liste de hello.

    Si vous avez choisi **créer un nouvel agent**, hello suivants choses :

    1.  Télécharger le logiciel de l’agent de synchronisation hello client à partir du lien hello fourni et l’installer sur l’ordinateur hello où se trouve hello SQL Server.
 
        > [!IMPORTANT]
        > Vous avez tooopen sortant le port TCP 1433 dans l’agent client hello hello pare-feu toolet de communiquer avec le serveur de hello.


    2.  Entrez un nom pour l’agent de hello.

    3.  Sélectionnez **Créer et générer une clé**.

    4.  Copiez le Presse-papiers toohello clé de l’agent hello.
        
        ![Création d’un agent de synchronisation](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  Sélectionnez **OK** tooclose hello **sélectionnez l’Agent de synchronisation** panneau.

    6.  Sur l’ordinateur SQL Server de hello, recherchez et exécuter l’application de l’Agent de synchronisation Client hello.

        ![application de l’agent client de synchronisation des données de Hello](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  Dans l’application de l’agent de synchronisation hello, sélectionnez **envoyer la clé de l’Agent**. Hello **Configuration de base de données de métadonnées de synchronisation** boîte de dialogue s’ouvre.

    8.  Bonjour **Configuration de base de données de métadonnées de synchronisation** boîte de dialogue, coller dans la clé d’agent hello copié à partir de hello portail Azure. Fournissent également des informations d’identification existantes de hello pour le serveur de base de données SQL Azure hello sur quel hello les métadonnées de base de données se trouve. (Si vous avez créé une nouvelle base de données de métadonnées, cette base de données est sur hello même serveur que la base de données concentrateur hello.) Sélectionnez **OK** et attendez hello configuration toofinish.

        ![Entrez hello des informations d’identification clé et le serveur de l’agent](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   Si vous obtenez une erreur de pare-feu à ce stade, vous devez toocreate une règle de pare-feu sur le trafic entrant à partir de l’ordinateur SQL Server de hello tooallow Azure. Vous pouvez créer des règles de hello manuellement dans le portail de hello, mais il peut s’avérer plus facile toocreate il dans SQL Server Management Studio (SSMS). Dans SSMS, essayez de base de données du concentrateur tooconnect toohello sur Azure. Entrez son nom sous la forme \<nom_base_données_hub\>.database.windows.net. Suivez les étapes de hello de règle de pare-feu Azure hello boîte de dialogue zone tooconfigure hello. Application de l’Agent de synchronisation Client toohello est renvoyé.

    9.  Dans l’application de l’Agent de synchronisation Client hello, cliquez sur **inscrire** tooregister une base de données SQL Server avec l’agent de hello. Hello **de Configuration SQL Server** boîte de dialogue s’ouvre.

        ![Ajouter et configurer une base de données SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. Bonjour **de Configuration SQL Server** boîte de dialogue, choisissez si tooconnect à l’aide de SQL Server ou l’authentification Windows. Si vous choisissez l’authentification SQL Server, entrez les informations d’identification existantes hello. Indiquez des noms de SQL Server de hello et hello de base de données hello que vous souhaitez toosync. Sélectionnez **tester la connexion** tootest vos paramètres. Ensuite, sélectionnez **Enregistrer**. base de données inscrite Hello s’affiche dans la liste de hello.

        ![La base de données SQL Server est maintenant inscrite.](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. Vous pouvez fermer une application de l’Agent de synchronisation Client hello.

    12. Dans le portail hello, sur hello **configurer On-Premises** panneau, sélectionnez **sélectionnez hello de base de données.** Hello **sélectionner une base de données** panneau s’ouvre.

    13. Sur hello **sélectionner une base de données** panneau, Bonjour **nom du membre de synchronisation** champ, fournissez un nom pour le nouveau membre de synchronisation hello. Ce nom est différent de nom hello de base de données hello lui-même. Sélectionnez la base de données de hello à partir de la liste de hello. Bonjour **Directions de synchronisation** , sélectionnez la synchronisation bidirectionnelle, toohello concentrateur, ou à partir de hello Hub.

        ![Sélectionnez hello sur la base de données de site](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. Sélectionnez **OK** tooclose hello **sélectionner une base de données** panneau. Puis sélectionnez **OK** tooclose hello **configurer On-Premises** lame et attendez hello nouveau synchroniser toobe membre créé et déployé. Enfin, cliquez sur **OK** tooclose hello **sélectionner les membres de la synchronisation** panneau.

        ![Sur la base de données local ajouté toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  tooconnect tooSQL synchronisation des données et l’agent local de hello, ajoutez votre rôle d’utilisateur nom toohello `DataSync_Executor`. Synchronisation des données crée ce rôle sur l’instance de SQL Server hello.

## <a name="step-3---configure-sync-group"></a>Étape 3 : configurer le groupe de synchronisation

Une fois les nouveaux membres de groupe de synchronisation hello sont créés et déployés, étape 3, **groupe de synchronisation configurer**, est mis en surbrillance dans hello **nouveau groupe de synchronisation** panneau.

1.  Sur hello **Tables** panneau, sélectionnez une base de données à partir de la liste de hello de synchronisation des membres du groupe, puis sélectionnez **actualisation du schéma**.

2.  Dans la liste hello des tables disponibles, sélectionnez les tables de hello que vous souhaitez toosync.

    ![Sélectionner les tables toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  Par défaut, toutes les colonnes de table de hello sont sélectionnés. Si vous ne souhaitez pas toutes les colonnes hello toosync, désactivez la case à cocher hello pour les colonnes hello que vous ne souhaitez pas toosync. N’oubliez pas sélectionné de la colonne de clé primaire tooleave hello.

    ![Sélectionner les champs toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  Enfin, sélectionnez **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
Félicitations ! Vous avez créé un groupe de synchronisation incluant une instance de base de données SQL et une base de données SQL Server.

Pour plus d’informations sur SQL Database et SQL Data Sync, consultez :

-   [Téléchargez la documentation technique hello complète synchronisation des données SQL](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [Télécharger la documentation des API REST de SQL Data Sync hello](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [Vue d’ensemble des bases de données SQL](sql-database-technical-overview.md)
-   [Gestion du cycle de vie des bases de données](https://msdn.microsoft.com/library/jj907294.aspx)
