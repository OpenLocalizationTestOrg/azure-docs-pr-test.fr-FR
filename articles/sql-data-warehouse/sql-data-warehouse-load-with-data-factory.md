---
title: "données aaaLoad dans Azure SQL Data Warehouse – Data Factory | Documents Microsoft"
description: "Ce didacticiel charge les données dans Azure SQL Data Warehouse à l’aide d’Azure Data Factory et utilise une base de données SQL Server en tant que source de données hello."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>Chargement de données dans SQL Data Warehouse avec Data Factory

Vous pouvez utiliser les données de tooload d’Azure Data Factory dans Azure SQL Data Warehouse de n’importe quelle hello [prise en charge des magasins de données source](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats). Par exemple, vous pouvez charger des données dans un entrepôt de données SQL à partir d’une base de données SQL Azure ou d’une base de données Oracle à l’aide de Data Factory. Didacticiel dans cet article vous montre comment les données tooload à partir d’un ordinateur local SQL Server de base de données dans un entrepôt de données SQL.

**Durée estimée**: ce didacticiel prend environ 10 à 15 minutes toocomplete une fois que les conditions préalables de hello sont remplies.

## <a name="prerequisites"></a>Composants requis

- Vous avez besoin une **base de données SQL Server** avec les tables qui contiennent des données hello toobe copiée toohello entrepôt de données SQL.  

- Vous avez besoin d’un **SQL Data Warehouse** en ligne. Si vous n’avez pas déjà d’un entrepôt de données, découvrez comment trop[créer un entrepôt de données SQL Azure](sql-data-warehouse-get-started-provision.md).

- Vous avez besoin d’un **compte de stockage Azure**. Si vous n’avez pas déjà un compte de stockage, découvrez comment trop[créer un compte de stockage](../storage/common/storage-create-storage-account.md). Pour de meilleures performances, recherchez le compte de stockage hello et hello l’entrepôt de données Bonjour même région Azure.

## <a name="configure-a-data-factory"></a>Configurer une fabrique de données
1. Connectez-vous à toohello [portail Azure][].
2. Recherchez votre entrepôt de données et cliquez sur tooopen il.
3. Dans le panneau principal de hello, cliquez sur **charger des données** > **Azure Data Factory**.

    ![Lancer l’Assistant Charger des données](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. Si vous n’avez pas une fabrique de données dans votre abonnement Azure, vous voyez un **nouvelle fabrique de données** boîte de dialogue dans un onglet distinct du navigateur de hello. Hello, renseignez les informations demandées, puis cliquez sur **créer**. Après la création de la fabrique de données hello, hello **nouvelle fabrique de données** boîte de dialogue se ferme et vous voyez hello **sélectionnez Data Factory** boîte de dialogue.

    Si vous avez une ou plusieurs fabriques de données déjà dans hello abonnement Azure, vous voyez hello **sélectionnez Data Factory** boîte de dialogue. Dans cette boîte de dialogue, vous pouvez sélectionner une fabrique de données existante ou cliquez sur **créer une nouvelle fabrique de données** toocreate un nouveau.

    ![Configurer une fabrique de données](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. Bonjour **sélectionnez Data Factory** boîte de dialogue, hello **charger des données** option est sélectionnée par défaut. Cliquez sur **suivant** toostart création d’une tâche de chargement de données.

## <a name="configure-hello-data-factory-properties"></a>Configurer les propriétés de fabrique de données hello
Maintenant que vous avez créé une fabrique de données, étape suivante de hello donnée tooconfigure hello du chargement de planification.

1. Pour le **nom de la tâche**, entrez **DWLoadData-fromSQLServer**.
2. Utiliser la valeur par défaut hello **exécuter qu’une seule fois maintenant** , cliquez sur **suivant**.

    ![Configurer la planification](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>Configurer le magasin de données source hello et la passerelle
Vous indiquez maintenant Data Factory hello local SQL Server de base de données à partir de laquelle vous souhaitez que les données de tooload.

1. Choisissez **SQL Server** de source de données pris en charge de hello stocker le catalogue, puis cliquez sur **suivant**.

    ![Choisir la source du serveur SQL](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. A **base de données SQL Server de spécifier hello locale** boîte de dialogue s’affiche. Hello tout d’abord **nom de la connexion** champ est automatiquement renseigné. deuxième champ de Hello demande nom hello Hello **passerelle**. Si vous utilisez une fabrique de données existant qui possède déjà une passerelle, vous pouvez réutiliser la passerelle de hello en le sélectionnant dans la liste déroulante de hello. Cliquez sur hello **créer une passerelle** lien toocreate une passerelle de gestion des données.  

    > [!NOTE]
    > Si le magasin de données de source de hello est local ou dans une machine virtuelle Azure IaaS, une passerelle de gestion des données est requise. Une passerelle a une relation 1-1 avec une fabrique de données. Elle ne peut pas être utilisée à partir de la fabrique de données dans un autre, mais il peut être utilisé par plusieurs données chargement des tâches avec Bonjour même fabrique de données. Une passerelle peut être banques de données toomultiple tooconnect utilisé lors de l’exécution des tâches de chargement des données.
    >
    > Pour plus d’informations sur la passerelle de hello, consultez [passerelle de gestion des données](../data-factory/data-factory-data-management-gateway.md) l’article.

3. Une boîte de dialogue **Créer une passerelle** s’affiche. Dans le champ Nom, entrez **GatewayForDWLoading**, puis cliquez sur **Créer**.

4. Une boîte de dialogue **Configurer la passerelle** s’affiche. Cliquez sur **lancer le programme d’installation express sur cet ordinateur** tooautomatically télécharger, installer et inscrire la passerelle de gestion des données sur votre ordinateur. progression de Hello est indiquée dans une fenêtre indépendante. Si la machine de hello ne peut pas connecter le magasin de données toohello, vous pouvez manuellement [télécharger et installer la passerelle de hello](https://www.microsoft.com/download/details.aspx?id=39717) sur un ordinateur qui peut se connecter à des données de toohello stocker et ensuite utiliser tooregister de clé hello.
    > [!NOTE]
    > le programme d’installation express de Hello fonctionne en mode natif avec Microsoft Edge et Internet Explorer. Si vous utilisez Google Chrome, d’abord installer extension de ClickOnce hello web Store de Chrome.

    ![Lancer le programme d’installation express](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. Attendez que hello passerelle le programme d’installation toocomplete. Une fois que la passerelle de hello est enregistré correctement et est en ligne, fermeture de fenêtre contextuelle hello et passerelle hello s’affiche dans le champ de la passerelle hello. Puis rest de hello, renseignez les champs obligatoires comme suit, puis cliquez sur **suivant**.
    - **Nom du serveur**: nom de hello local SQL Server.
    - **Nom de la base de données** : base de données SQL Server.
    - **Chiffrement des informations d’identification**: utiliser par défaut de hello « par le navigateur web ».
    - **Type d’authentification**: choisissez de type hello d’authentification que vous utilisez.
    - **Nom d’utilisateur** et **mot de passe**: entrez le nom d’utilisateur hello et le mot de passe pour un utilisateur qui a des données d’autorisation toocopy hello.

    ![Lancer le programme d’installation express](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. étape suivante de Hello est toochoose les tables de hello depuis lequel les données hello toocopy. Vous pouvez filtrer les tables hello à l’aide de mots clés. Et vous pouvez afficher un aperçu de schéma de données et la table hello dans le panneau inférieur hello. Une fois la sélection terminée, cliquez sur **Suivant**.

    ![Sélectionner des tables](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>Configurer la destination hello, votre entrepôt de données SQL

Maintenant, vous indiquez Data Factory les informations de destination hello.

1. Vos informations de connexion SQL Data Warehouse sont renseignées automatiquement. Entrez un mot de passe hello hello nom d’utilisateur. , puis cliquez sur **Suivant**.

    ![Configurer la destination](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. Un mappage de table intelligent s’affiche qui mappe les tables sources toodestination basées sur des noms de table. Si la table de hello n’existe pas dans la destination de hello, par défaut ADF créera un par hello même nom (cela s’applique tooSQL serveur ou base de données SQL Azure en tant que source). Vous pouvez également choisir la table de toomap tooan existante. Vérifiez, puis cliquez sur **Suivant**.

    ![Mapper les tables](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. Passez en revue le mappage de schéma hello et recherchez les messages d’erreur ou avertissement. Le mappage intelligent repose sur le nom de colonne. S’il existe une conversion de type de données non pris en charge entre les colonnes source et de destination hello, vous consultez un message d’erreur en même temps que la table correspondante de hello. Si vous choisissez automatique de Data Factory toolet créer des tables de hello, conversion de type de données peut se produire si nécessaire l’incompatibilité de hello toofix entre des magasins de source et de destination.

    ![Mapper le schéma](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. Cliquez sur **Suivant**.

## <a name="configure-hello-performance-settings"></a>Configurer les paramètres de performances hello
Dans les configurations de performances hello, vous configurez un compte de stockage Azure utilisé pour le transit des données de hello avant de charger dans l’entrepôt de données SQL à l’aide d’énumérer efficacement [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly). Une fois hello copie terminée, les données intermédiaires dans le stockage de salutation seront nettoyées automatiquement.

Sélectionnez un compte de stockage Azure existant, puis cliquez sur **Suivant**.

![Configurer le blob intermédiaire](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>Passez en revue les informations de résumé et de déploiement du pipeline de hello

Passez en revue la configuration de hello et cliquez sur **Terminer** pipeline de bouton toodeploy hello.

![Déployer la fabrique de données](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>Surveiller la progression du chargement des données

Vous pouvez voir la progression du déploiement hello et résultats Bonjour **déploiement** page.

1. Une fois le déploiement de hello est terminé, cliquez sur lien hello indiquant **cliquez ici pipeline de copie toomonitor** données toomonitor progression du chargement.

    ![Surveillance d’un pipeline](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. Hello nouvellement créé **DWLoadData-fromSQLServer** pipeline de chargement de données est automatiquement sélectionné à partir de hello gauche **l’Explorateur de ressources**.

    ![Afficher le pipeline](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. Cliquez sur dans le pipeline hello au milieu de hello hello toosee de panneau état détaillé de chaque table qui mappe tooan activité.

    ![Afficher l’activité de la table](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. Plus cliquez dans une activité et vous voyez le chargement des détails dans le volet droit de hello, y compris la taille des données, les lignes, débit, etc. les données de salutation.

    ![Afficher les informations relatives à l’activité des tables](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. Cliquez sur cette analyse vue ultérieur, accédez tooyour SQL Data Warehouse, de toolaunch **charger des données > Azure Data Factory**, sélectionnez votre fabrique et choisissez **surveiller existant du chargement des tâches**.

## <a name="next-steps"></a>Étapes suivantes

reportez-vous à votre tooSQL de base de données Data Warehouse, toomigrate [présentation de la Migration](sql-data-warehouse-overview-migrate.md).

toolearn en savoir plus sur Azure Data Factory et de ses fonctionnalités de déplacement des données, consultez hello suivant des articles :

- [Introduction tooAzure Data Factory](../data-factory/data-factory-introduction.md)
- [Déplacer des données à l’aide de l’activité de copie](../data-factory/data-factory-data-movement-activities.md)
- [Déplacer les données tooand à partir de l’entrepôt de données SQL Azure à l’aide d’Azure Data Factory](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

tooexplore vos données dans l’entrepôt de données SQL, consultez hello suivants articles :

- [Se connecter tooSQL Data Warehouse avec Visual Studio et SSDT](sql-data-warehouse-query-visual-studio.md)
- [Données visuelles avec Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)

<!-- Azure references -->
[portail Azure]: https://portal.azure.com
