---
title: "aaaMigrate tooAzure de base de données SQL Server de la base de données SQL | Documents Microsoft"
description: "En savoir plus toomigrate votre tooAzure de base de données SQL Server de la base de données SQL."
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a>Migrer votre tooAzure de base de données SQL Server de la base de données SQL

Déplacement de votre serveur SQL Server tooAzure de base de données de la base de données SQL est un processus en trois parties : vous tout d’abord préparez, puis exportez et d’importerez de la base de données hello. Ce didacticiel vous apprend à effectuer les opérations suivantes :

> [!div class="checklist"]
> * Préparer une base de données dans SQL Server tooAzure de migration de base de données SQL à l’aide de hello [l’Assistant Migration de données](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)
> * Fichier BACPAC tooa exportation hello de base de données
> * Importer un fichier BACPAC hello dans une base de données SQL Azure

Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, assurez-vous que hello est suivant des conditions préalables requises sont effectuées :

- Version la plus récente installée hello de [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). L’installation de SSMS installe également la version la plus récente hello de SQLPackage, un utilitaire de ligne de commande qui peut être utilisé tooautomate un éventail de tâches de développement de base de données. 
- Hello installé [l’Assistant Migration de données](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- Vous avez identifié et que vous avez accès tooa de base de données toomigrate. Ce didacticiel utilise hello [SQL Server 2008 R2 base de données AdventureWorks OLTP](https://msftdbprodsamples.codeplex.com/releases/view/59211) sur une instance de SQL Server 2008 R2 ou versions ultérieures, mais vous pouvez utiliser une base de données de votre choix. problèmes de compatibilité toofix, utilisez [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>Préparation de la migration

Vous êtes prêt tooprepare pour la migration. Suivez ces hello de toouse étapes  **[l’Assistant Migration de données](https://www.microsoft.com/download/details.aspx?id=53595)**  tooassess hello préparation de votre base de données tooAzure de migration de base de données SQL.

1. Ouvrez hello **l’Assistant Migration de données**. Vous pouvez exécuter DMA sur n’importe quel ordinateur avec connectivité toohello SQL Server instance contenant hello de base de données que vous envisagez de toomigrate, vous n’avez pas besoin de tooinstall sur l’ordinateur hébergeant de hello hello l’instance de SQL Server.

     ![ouvrir data migration assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. Dans le menu de gauche hello, cliquez sur **+ nouveau** toocreate un **évaluation** projet. Renseignez le formulaire hello avec un **nom du projet** (toutes les autres valeurs doivent rester à leurs valeurs par défaut) et cliquez sur **créer**. Hello **Options** ouvrir la page.

     ![nouveau projet de data migration assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. Sur hello **Options** , cliquez sur **suivant**. Hello **sélectionnez sources** ouvrir la page.

     ![nouvelles options de migration de données](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. Sur hello **sélectionnez sources** , entrez le nom hello d’instance de SQL Server contenant le serveur hello vous envisagez de toomigrate. Modification hello autres valeurs de cette page si nécessaire. Cliquez sur **Connecter**.

     ![nouvelle migration de données, select sources (sélectionner des sources)](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. Bonjour **ajouter des sources de** partie Hello **sélectionnez sources** , sélectionnez les cases à cocher hello pour toobe de bases de données hello testée pour leur compatibilité. Cliquez sur **Add**.

     ![nouvelle migration de données, select sources (sélectionner des sources)](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. Cliquez sur **Start Assessment** (Démarrer l’évaluation).

     ![nouvelle migration de données, start assessment (démarrer l’évaluation)](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. Lors de l’évaluation de hello est terminée, recherchez tout d’abord toosee si base de données hello toomigrate suffisamment compatible. Recherchez la coche hello dans un cercle vert.

     ![nouvelle migration de données, résultats de l’évaluation de compatibilité](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Passez en revue les résultats hello. Hello **parité de fonctionnalités SQL Server** résultats affichés sont tooreview de résultats par défaut hello. Passez en revue spécifiquement hello plus d’informations sur les fonctionnalités non prises en charge et partiellement prises en charge et hello fourni plus d’informations sur les actions recommandées. 

     ![nouvelle migration de données, évaluation de la parité](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. Hello de révision **des problèmes de compatibilité** en cliquant sur cette option dans le coin supérieur gauche de hello. Révision spécifiquement hello plus d’informations sur les bloqueurs de migration, les changements de comportement et fonctionnalités déconseillées de chaque niveau de compatibilité. Pour la base de données hello AdventureWorks2008R2, examiner les modifications de hello recherche de texte tooFull depuis SQL Server 2008 et hello change tooSERVERPROPERTY('LCID') depuis SQL Server 2000. Pour plus de détails sur ces modifications, des liens vers d’autres d’informations sont fournis. Un grand nombre d’options de recherche et de paramètres de recherche en texte intégral ont changé 

   > [!IMPORTANT] 
   > Après avoir migré votre tooAzure de base de données de la base de données SQL, vous pouvez choisir la base de données toooperate hello à son niveau de compatibilité actuel (niveau 100 pour la base de données AdventureWorks2008R2 hello) ou à un niveau supérieur. Pour plus d’informations sur les implications en matière de hello et les options pour l’exploitation d’une base de données à un niveau de compatibilité spécifiques, consultez [niveau de compatibilité ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Voir aussi [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) pour plus d’informations sur les paramètres de niveau de base de données supplémentaires liées toocompatibility niveaux.
   >

10. Si vous le souhaitez, cliquez sur **exporter le rapport** rapport de hello toosave sous la forme d’un fichier JSON.
11. Hello fermer l’Assistant Migration de données.

## <a name="export-toobacpac-file"></a>Fichier d’exportation tooBACPAC 

Un fichier BACPAC est un fichier ZIP avec une extension de fichier BACPAC qui contient les métadonnées de hello et les données à partir d’une base de données SQL Server. Un fichier BACPAC peut être stocké dans le stockage blob Azure ou dans le stockage local pour l’archivage ou pour la migration - par exemple à partir de SQL Server tooAzure de la base de données SQL. Pour une exportation toobe cohérente, vous ne devez vous assurer qu’aucune écriture activité se produit lors de l’exportation de hello.

Suivez ces étapes toouse hello SQLPackage utilitaire de ligne de commande tooexport hello AdventureWorks2008R2 base de données toolocal stockage.

1. Ouvrez une invite de commandes Windows et de changer de répertoire tooa dossier dans lequel vous avez hello **130** version de SQLPackage, telles que **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**.

2. Exécutez hello commande SQLPackage à hello de tooexport hello invite de commandes suivante **AdventureWorks2008R2** à partir de la base de données **localhost** trop**AdventureWorks2008R2.bacpac**. Modifiez ces valeurs comme environnement de tooyour appropriée.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage, exportation](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Une fois terminée l’exécution de hello hello généré BACPAC fichier est stocké dans le répertoire hello où sqlpackage hello exécutable se trouve. Dans cet exemple, C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin. 

## <a name="log-in-toohello-azure-portal"></a>Ouvrez une session dans toohello portail Azure

Connectez-vous à toohello [portail Azure](https://portal.azure.com/). Ouverture de session à partir de l’ordinateur hello à partir duquel vous exécutez l’utilitaire de ligne de commande de SQLPackage hello facilite la création de hello hello de règle de pare-feu à l’étape 5.

## <a name="create-a-sql-server-logical-server"></a>Créer un serveur logique SQL Server

Un [serveur logique SQL Server](sql-database-features.md) fait office de point d’administration central pour plusieurs bases de données. Suivez ces étapes toocreate un Bonjour de toocontain serveur logique SQL server migrées de la base de données Adventure Works OLTP SQL Server. 

1. Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.

2. Type **sql server** dans la fenêtre de recherche hello sur hello **nouveau** page, puis sélectionnez **base de données SQL (serveur logique)** de hello liste filtrée.

    ![sélectionner un serveur logique](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. Sur hello **tout** , cliquez sur **SQL server (serveur logique)** puis cliquez sur **créer** sur hello **SQL Server (serveur logique)** page .

    ![créer un serveur logique](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. Rempliront hello SQL server (serveur logique) avec hello suivant d’informations, comme indiqué dans le hello précédant l’image :     

   | Paramètre       | Valeur suggérée | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nom du serveur** | Entrez un nom globalement unique | Pour les noms de serveur valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom). | 
   | **Connexion d’administrateur du serveur** | Entrez un nom valide | Pour les noms de connexion valides, consultez [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données). |
   | **Mot de passe** | Entrez un mot de passe valide | Votre mot de passe doit comporter au moins 8 caractères et contenir des caractères appartenant à trois des hello suivant catégories : les caractères majuscules, caractères en minuscules, des chiffres et des caractères non alphanumériques. |
   | **Abonnement** | Sélectionner un abonnement | Pour plus d’informations sur vos abonnements, consultez [Abonnements](https://account.windowsazure.com/Subscriptions). |
   | **Groupe de ressources** | Choisissez ou créez un groupe de ressources, tel que **myResourceGroup** |  Pour les noms de groupe de ressources valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom). |
   | **Emplacement** | Entrez n’importe quel emplacement valide pour le nouveau serveur de hello | Pour plus d’informations sur les régions, consultez [Régions Azure](https://azure.microsoft.com/regions/). |

   ![formulaire de création de serveur logique rempli](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. Cliquez sur **créer** serveur logique de tooprovision hello. L’approvisionnement prend quelques minutes. 

> [!IMPORTANT]
> Mémorisez le nom du serveur, le nom de connexion de l’administrateur du serveur et le mot de passe. Vous aurez besoin de ces valeurs plus loin dans ce didacticiel.
>

## <a name="create-a-server-level-firewall-rule"></a>créer une règle de pare-feu au niveau du serveur ;

Hello service de base de données SQL crée un [pare-feu au niveau serveur hello](sql-database-firewall-configure.md) qui empêche des applications externes et des outils de se connecter toohello server ou des bases de données sur le serveur de hello, sauf si une règle de pare-feu est créée tooopen hello pare-feu pour des adresses IP spécifiques. Suivez ces étapes de toocreate une règle de pare-feu de niveau serveur de base de données SQL pour hello adresseIP de hello ordinateur à partir duquel vous exécutez l’utilitaire de ligne de commande de SQLPackage hello. Cela permet de SQLPackage tooconnect toohello SQL serverDatabase serveur logique via le pare-feu de base de données SQL Azure hello. 

1. Cliquez sur **toutes les ressources** hello menu de gauche et cliquez sur le nouveau serveur sur hello **toutes les ressources** page. page Vue d’ensemble de Hello pour votre serveur s’ouvre et fournit des options pour poursuivre la configuration.

     ![présentation du serveur logique](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Cliquez sur **pare-feu** dans le menu de gauche hello sous **paramètres** sur la page de vue d’ensemble de hello. Hello **des paramètres de pare-feu** page serveur de base de données SQL hello s’ouvre. 

3. Cliquez sur **ajouter l’adresse IP du client** sur hello barre d’outils tooadd hello adresse IP de hello ordinateur, vous utilisez actuellement, puis sur **enregistrer**. Une règle de pare-feu au niveau du serveur est créée pour cette adresse IP.

     ![définir la règle de pare-feu de serveur](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. Cliquez sur **OK**.

Vous pouvez désormais connecter tooall de bases de données sur ce serveur à l’aide de SQL Server Management Studio ou un autre outil de votre choix à partir de cette adresse IP à l’aide du compte d’administrateur de serveur hello créé précédemment.

> [!NOTE]
> SQL Database communique par le biais du port 1433. Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 ne peut pas être autorisé par le pare-feu de votre réseau. Dans ce cas, serveur de base de données SQL Azure tooyour ne peut pas se connecter à moins que votre service informatique s’ouvre le port 1433.
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a>Importer un tooAzure de fichier BACPAC de base de données SQL 

Hello dernières versions des hello SQLPackage utilitaire prennent en charge pour la création d’une base de données SQL Azure à un [au niveau de performances et de la couche de service](sql-database-service-tiers.md). Pour de meilleures performances lors de l’importation, sélectionnez un niveau élevé de service de couche et les performances et réduire après l’importation si le niveau de performances et de la couche de service hello est supérieur à ce qui vous devez immédiatement.

Suivez ces étapes utilisez hello SQLPackage utilitaire de ligne de commande tooimport hello AdventureWorks2008R2 de base de données tooAzure base de données SQL. Vous pouvez utiliser SQL Server Management Studio pour cette tâche, SQLPackage est méthode hello préféré pour la plupart des environnements de production pour une flexibilité maximale et les performances. Consultez [migration à partir de SQL Server tooAzure de la base de données SQL à l’aide des fichiers BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

- Exécutez hello commande SQLPackage à hello de tooimport hello invite de commandes suivante **AdventureWorks2008R2** de base de données à partir du serveur logique de stockage local toohello SQL server que vous créé précédemment tooa nouvelle base de données, un service niveau de **Premium**et un objectif de Service de **P6**. Remplacer les valeurs de hello figurant entre crochets par les valeurs appropriées pour votre serveur logique SQL server et spécifiez un nom pour hello nouvelle base de données (également remplacer hello chevrons). Vous pouvez également choisir les valeurs hello toochange pour l’édition de base de données et le service objectgive comme environnement de tooyour appropriée. Pour les besoins de hello de ce didacticiel, base de données migrée hello est appelée **myMigratedDatabase**.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![importer sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Un serveur logique SQL Server écoute le port 1433. Si vous essayez de tooconnect tooa serveur SQL server logique à partir d’un pare-feu d’entreprise, ce port doit être ouvert dans le pare-feu d’entreprise hello pour toosuccessfully de vous connecter.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>Se connecter avec SSMS (SQL Server Management Studio)

Utilisez SQL Server Management Studio tooestablish un serveur de base de données SQL Azure de tooyour de connexion et base de données qui vient d’être migrée, appelé **myMigratedDatabase** dans ce didacticiel. Si vous exécutez SQL Server Management Studio sur un autre ordinateur à partir duquel vous avez exécuté SQLPackage, créez une règle de pare-feu pour cet ordinateur à l’aide des étapes de hello dans la procédure précédente de hello.

1. Ouvrez SQL Server Management Studio.

2. Bonjour **connecter tooServer** boîte de dialogue, entrez hello informations suivantes :
   - **Type de serveur** : spécifiez le moteur de base de données
   - **Nom du serveur** : entrez votre nom de serveur complet, par exemple **mynewserver20170403.database.windows.net**
   - **Authentification** : spécifiez l’authentification SQL Server
   - **Connexion** : entrez votre compte d’administrateur de serveur
   - **Mot de passe**: entrez le mot de passe de hello pour votre compte d’administrateur de serveur
 
    ![se connecter avec ssms](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. Cliquez sur **Connecter**. fenêtre de l’Explorateur d’objets Hello s’ouvre. 

4. Dans l’Explorateur d’objets, développez **bases de données** , puis **myMigratedDatabase** tooview des objets de hello dans la base de données exemple hello.

## <a name="change-database-properties"></a>Modifier les propriétés de base de données

Vous pouvez modifier le niveau de service hello, niveau de performance et le niveau de compatibilité à l’aide de SQL Server Management Studio. Pendant la phase d’importation hello, nous recommandons que vous importez tooa supérieur performances couche base de données pour de meilleures performances, mais que vous l’échelle après importation de hello toosave money jusqu'à ce que vous êtes prêt tooactively utilisation hello base de données importée. La modification du niveau de compatibilité hello maîtrise des meilleures performances et des fonctionnalités les plus récents d’accès toohello Hello service de base de données SQL Azure. Lorsque vous migrez une ancienne base de données, son niveau de compatibilité de base de données est maintenue au niveau de hello plus bas pris en charge qui est compatible avec la base de données hello en cours d’importation. Pour plus d’informations, voir [Amélioration des performances des requêtes avec le niveau de compatibilité 130 dans Azure SQL Database](sql-database-compatibility-level-query-performance-130.md).

1. Dans l’Explorateur d’objets, cliquez avec le bouton droit sur **myMigratedDatabase**, puis cliquez sur **Nouvelle requête**. Une fenêtre de requête s’ouvre tooyour connecté de base de données.

2. Exécutez hello suivant le niveau de service de commande tooset hello trop**Standard** et hello le niveau de performance trop**S1**.

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![changer le niveau de service](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. Exécutez hello suivant le niveau de compatibilité de base de données de commande toochange hello trop**130**.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![modifier le niveau de compatibilité](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>Étapes suivantes 
Dans ce didacticiel, vous avez préparé votre base de données, vous l’avez exportée et importée. Vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]
> * Préparer une base de données dans SQL Server tooAzure de migration de base de données SQL
> * Fichier BACPAC tooa exportation hello de base de données
> * Importer un fichier BACPAC hello dans une base de données SQL Azure

Avancer toolearn de didacticiel suivant toohello comment toosecure votre base de données.

> [!div class="nextstepaction"]
> [Sécuriser votre base de données SQL Azure](sql-database-security-tutorial.md).


