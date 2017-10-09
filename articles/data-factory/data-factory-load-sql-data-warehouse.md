---
title: "aaaLoad des téraoctets de données dans l’entrepôt de données SQL | Documents Microsoft"
description: "Montre comment 1 To de données peut être chargé dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a>Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory
[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) est une base de données de mise à l’échelle basée sur le cloud qui prend en charge le traitement de grands volumes de données relationnelles et non relationnelles.  Reposant sur une architecture MPP (massively parallel processing), SQL Data Warehouse est optimisée pour les charges de travail d’entrepôt de données d’entreprise.  Il offre cloud élasticité avec un stockage tooscale hello flexibilité et de calcul indépendamment.

La prise en main d’Azure SQL Data Warehouse est désormais plus facile à l’aide **d’Azure Data Factory**.  Azure Data Factory est un service d’intégration des données cloud entièrement géré, ce qui peut être utilisé toopopulate un entrepôt de données SQL avec des données de hello de votre système existant et l’enregistrement d’un temps précieux lors de l’évaluation SQL Data Warehouse et votre analytique solutions. Voici hello principaux avantages du chargement de données dans l’entrepôt de données SQL Azure à l’aide de la fabrique de données Azure :

* **Tooset facile des**: 5-étape intuitif Assistant pas de script.
* **Prise en charge étendue du magasin de données** : prise en charge intégrée d’un ensemble complet de magasins de données locaux et sur le cloud.
* **Sécurisés et conformes**: données sont transférées sur HTTPS ou ExpressRoute et la présence du service global garantit que vos données ne quittent jamais les limites géographiques hello
* **Performances uniques à l’aide de PolyBase** – à l’aide de Polybase est hello plus efficace des toomove données dans Azure SQL Data Warehouse. À l’aide de hello mise en lots de la fonctionnalité de l’objet blob, vous pouvez obtenir vitesses de charge élevée de tous les types de banques de données en plus de stockage d’objets Blob Azure, qui hello Polybase prend par défaut.

Cet article vous montre comment toouse Assistant Copier les données fabrique tooload 1 To de données à partir du stockage d’objets Blob Azure dans Azure SQL Data Warehouse sous des 15 dernières minutes, à un débit plus 1,2 Gbits/s.

Cet article fournit des instructions détaillées pour le déplacement des données dans Azure SQL Data Warehouse à l’aide de hello Assistant copie de.

> [!NOTE]
>  Pour des informations générales sur les fonctionnalités de la fabrique de données lors du déplacement des données vers/à partir de l’entrepôt de données SQL Azure, consultez [déplacer tooand de données à partir de l’entrepôt de données SQL Azure à l’aide d’Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) l’article.
>
> Vous pouvez également créer des pipelines à l’aide du portail Azure, de Visual Studio, de PowerShell, etc. Consultez [didacticiel : copier des données d’objets Blob Azure tooAzure base de données SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour une présentation rapide des instructions détaillées pour l’utilisation de l’activité de copie de hello dans Azure Data Factory.  
>
>

## <a name="prerequisites"></a>Composants requis
* Stockage Blob Azure : cette expérience utilise le Stockage Blob Azure (GRS) pour stocker un jeu de données de test TPC-H.  Si vous n’avez pas de compte de stockage Azure, Découvrez [comment toocreate un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* [TPC-H](http://www.tpc.org/tpch/) données : nous allons toouse TPC-H comme hello du jeu de données de test.  toodo, vous avez besoin toouse `dbgen` à partir de la boîte à outils de TPC-H, qui vous permet de générer le jeu de données hello.  Vous pouvez soit télécharger le code source pour `dbgen` de [TPC outils](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) et compilez-le vous-même ou binaire hello compilé de téléchargement à partir de [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).  Fichier plat de toogenerate 1 To pour les commandes dbgen.exe exécution avec les éléments suivants de hello `lineitem` table réparti entre 10 fichiers :

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * …
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    Maintenant, hello de copie généré tooAzure de fichiers Blob.  Consultez trop[déplacer des données tooand à partir d’un système de fichiers local à l’aide d’Azure Data Factory](data-factory-onprem-file-system-connector.md) procédure toodo qui à l’aide de la copie de la définition d’application.    
* Azure SQL Data Warehouse : cette expérience charge des données dans Azure SQL Data Warehouse créé avec 6 000 DWU

    Consultez trop[créer un entrepôt de données SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) pour obtenir des instructions détaillées sur la façon dont toocreate une SQL l’entrepôt de données de base de données.  tooget hello charge possible des performances optimales dans l’entrepôt de données SQL à l’aide de Polybase, nous choisissons le nombre maximal d’unités de l’entrepôt de données (Dwu) autorisés dans le paramètre de Performance hello, qui est de 6 000 Dwu.

  > [!NOTE]
  > Lors du chargement d’objets Blob Azure, données hello performances de chargement sont directement proportionnelle toohello différents Dwu vous configurez sur hello SQL Data Warehouse :
  >
  > Le chargement de 1 To dans 1 000 DWU SQL Data Warehouse prend 87 minutes (débit d’environ 200 Mo/s). Le chargement de 1 To dans 2000 DWU SQL Data Warehouse prend 46 minutes (débit d’environ 380 Mo/s). Le chargement de 1 To dans 6 000 DWU SQL Data Warehouse prend 14 minutes (débit d’environ 1,2 Go/s).
  >
  >

    toocreate un entrepôt de données SQL avec 6 000 Dwu, déplacez hello performances curseur tous les toohello de façon hello droite :

    ![Curseur Performance](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    Pour une base de données existante qui n’est pas configurée avec 6 000 DWU, vous pouvez la mettre à l’échelle à l’aide du portail Azure.  Accédez toohello de base de données dans le portail Azure et il est un **échelle** bouton Bonjour **vue d’ensemble** Panneau de configuration illustré hello suivant image :

    ![Bouton Mise à l’échelle](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    Cliquez sur hello **échelle** suivant de bouton tooopen hello du panneau, déplacez la valeur maximale de hello curseur toohello, puis cliquez sur **enregistrer** bouton.

    ![Boîte de dialogue de mise à l’échelle](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    Cette expérience charge des données dans Azure SQL Data Warehouse à l’aide de la classe de ressources `xlargerc`.

    tooachieve meilleurs résultats possibles, la copie doit toobe effectuée à l’aide d’un utilisateur de l’entrepôt de données SQL appartenant trop`xlargerc` classe de ressource.  Découvrez comment toodo qui en suivant [modifier un exemple de classe de ressource utilisateur](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).  
* Créer le schéma de table de destination dans la base de données de l’entrepôt de données SQL Azure, en exécutant hello suivant l’instruction DDL :

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
Étapes hello terminées, nous sommes maintenant à l’aide de hello Assistant copie de l’activité de copie tooconfigure prêt hello.

## <a name="launch-copy-wizard"></a>Lancer l’Assistant Copie
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **+ nouveau** à partir de l’angle supérieur gauche de hello, cliquez sur **Intelligence + analytique**, puis cliquez sur **Data Factory**.
3. Bonjour **nouvelle fabrique de données** panneau :

   1. Entrez **LoadIntoSQLDWDataFactory** pour hello **nom**.
       nom de Hello de fabrique de données Azure hello doit être globalement unique. Si vous recevez une erreur de hello : **nom de fabrique de données « LoadIntoSQLDWDataFactory » n’est pas disponible**, de modifier le nom hello hello fabrique de données (par exemple, yournameLoadIntoSQLDWDataFactory) et essayez à nouveau de créer. Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.  
   2. Sélectionnez votre **abonnement**Azure.
   3. Pour le groupe de ressources, effectuez l’une des hello comme suit :
      1. Sélectionnez **utiliser l’existante** tooselect un groupe de ressources existant.
      2. Sélectionnez **nouvel** tooenter un nom pour un groupe de ressources.
   4. Sélectionnez un **emplacement** de fabrique de données hello.
   5. Sélectionnez **toodashboard du code confidentiel** bas hello du Panneau de hello de case à cocher.  
   6. Cliquez sur **Créer**.
4. Après la création de hello est terminée, vous voyez hello **Data Factory** panneau comme indiqué dans hello suivant image :

   ![Page d'accueil Data Factory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. Sur la page d’accueil de Data Factory hello, cliquez sur hello **copier les données** vignette toolaunch **Assistant copie de**.

   > [!NOTE]
   > Si vous voyez ce navigateur hello est bloqué au niveau de « Autorisation... », désactiver/Décochez **bloquer les cookies tiers et les données de site** définition (ou) qu’il soit activé et créer une exception pour **login.microsoftonline.com**, puis essayez de lancer les Assistant hello à nouveau.
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a>Étape 1 : Configurer la planification du chargement de données
première étape de Hello donnée tooconfigure hello du chargement de planification.  

Bonjour **propriétés** page :

1. Entrez **CopyFromBlobToAzureSqlDataWarehouse** comme **Nom de la tâche**
2. Sélectionnez l’option **Exécuter une fois**.   
3. Cliquez sur **Suivant**.  

    ![Assistant Copie - Page Propriétés](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a>Étape 2 : Configurer la source
Cette indique la section hello de source de hello étapes tooconfigure : contenant des objets Blob Azure hello 1 to TPC-fichiers de ligne H.

1. Sélectionnez hello **stockage d’objets Blob Azure** comme données de salutation stocker, puis cliquez sur **suivant**.

    ![Assistant Copie - Page Sélectionner la source](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. Renseignez les informations de connexion hello pour hello compte de stockage d’objets Blob Azure, puis cliquez sur **suivant**.

    ![Assistant Copie - Informations de connexion à la source](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. Choisissez hello **dossier** contenant hello TPC-H ligne fichiers d’élément et cliquez sur **suivant**.

    ![Assistant Copie - Sélectionner le dossier d’entrée](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. Lorsque vous cliquez sur **suivant**, paramètres de format de fichier hello sont détectés automatiquement.  Vérifiez toomake que ce séparateur de colonnes est ' | 'au lieu de virgules par défaut hello','.  Cliquez sur **suivant** une fois que vous avez affiché un aperçu des données de salutation.

    ![Assistant Copie - Paramètres de format de fichier](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a>Étape 3 : Configurer la destination
Cette section vous montre comment tooconfigure hello destination : `lineitem` table dans la base de données Azure SQL Data Warehouse hello.

1. Choisissez **Azure SQL Data Warehouse** en tant que destination de hello stocker, cliquez sur **suivant**.

    ![Assistant Copie - Sélectionner le magasin de données de destination](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. Renseignez les informations de connexion hello pour Azure SQL Data Warehouse.  Assurez-vous que vous spécifiez utilisateur hello qui est membre du rôle de hello `xlargerc` (voir hello **conditions préalables** section pour obtenir des instructions détaillées), puis cliquez sur **suivant**.

    ![Assistant Copie - Informations de connexion à la destination](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. Choisissez la table de destination hello et cliquez sur **suivant**.

    ![Assistant Copie - Page Mappage de table](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. Dans la page Mappage de schéma, laissez l’option « Appliquer le mappage de colonnes » décochée et cliquez sur **Suivant**.

## <a name="step-4-performance-settings"></a>Étape 4 : Paramètres de performance

La case **Autoriser Polybase** est cochée par défaut.  Cliquez sur **Suivant**.

![Assistant Copie - Page Mappage de schéma](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a>Étape 5 : Déployer et surveiller les résultats du chargement
1. Cliquez sur **Terminer** toodeploy du bouton.

    ![Assistant Copie - Page Résumé](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. Une fois le déploiement de hello est terminé, cliquez sur `Click here toomonitor copy pipeline` copie de hello toomonitor statut d’exécution. Pipeline de copie hello sélectionnez vous avez créé dans hello **Windows de l’activité** liste.

    ![Assistant Copie - Page Résumé](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    Vous pouvez consulter copie hello détails de l’exécution dans hello **activité fenêtre Explorateur** dans le panneau droit hello, y compris le volume de données hello lire à partir de la source et écrites dans la destination, la durée et le débit moyen de hello pour hello exécuter,.

    Comme vous pouvez le constater hello suivant capture d’écran, la copie de 1 To de stockage d’objets Blob Azure dans SQL Data Warehouse a duré 14 minutes, efficacement productivité 1,22 Gbits/s !

    ![Assistant Copie - Boîte de dialogue Succès](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a>Meilleures pratiques
Voici quelques meilleures pratiques pour l’exécution de votre base de données Azure SQL Data Warehouse :

* Utilisez une classe de ressources supérieure lors du chargement dans un INDEX COLUMNSTORE EN CLUSTER.
* Pour des jonctions plus efficaces, envisagez d’utiliser la distribution par hachage en fonction d’une colonne sélectionnée au lieu de la distribution par tourniquet (round robin) par défaut.
* Pour des vitesses de chargement plus rapides, envisagez d’utiliser des tas pour les données temporaires.
* Créez des statistiques une fois le chargement Azure SQL Data Warehouse terminé.

Pour plus d’informations, consultez [Meilleures pratiques pour Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

## <a name="next-steps"></a>Étapes suivantes
* [Assistant copie de fabrique de données](data-factory-copy-wizard.md) -cet article fournit des détails sur l’Assistant copie de hello.
* [Copier l’activité guide des performances et paramétrage](data-factory-copy-activity-performance.md) -cet article contient des mesures de performances de référence hello et guide d’optimisation.
