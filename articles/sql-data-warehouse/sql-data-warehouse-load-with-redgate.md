---
title: "entrepôt de données Azure aaaUse Redgate tooload données tooyour | Documents Microsoft"
description: "Découvrez comment Data Platform Studio de toouse Redgate pour les scénarios d’entreposage de données."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a>Chargement de données avec Redgate Data Platform Studio
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

Ce didacticiel vous montre comment toouse [données plateforme Studio de Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) données de toomove (STD) à partir d’un tooAzure de SQL Server locale SQL Data Warehouse. Studio de plateforme de données applique des correctifs de compatibilité plus appropriés hello et optimisations, donc il a hello plus rapidement moyen tooget en main de l’entrepôt de données SQL.

> [!NOTE]
> [Redgate](http://www.red-gate.com) est un partenaire Microsoft de longue date, et fournit divers outils SQL Server. Cette fonctionnalité de Data Platform Studio est disponible gratuitement pour un usage commercial et non commercial.
> 
> 

## <a name="before-you-begin"></a>Avant de commencer
### <a name="create-or-identify-resources"></a>Créer ou identifier des ressources
Avant de commencer ce didacticiel, vous devez toohave :

* **base de données SQL Server locale**: hello les données que vous souhaitez tooimport tooSQL l’entrepôt de données doit toocome à partir d’un ordinateur local SQL Server (version 2008R2 ou version ultérieure). Data Platform Studio ne peut pas importer les données directement à partir d’une base de données Azure SQL Database, ni à partir de fichiers texte.
* **Compte de stockage Azure**: données plateforme Studio prépare les données hello dans le stockage d’objets Blob Azure avant de les charger dans l’entrepôt de données SQL. compte de stockage Hello doit utiliser le modèle de déploiement « Gestionnaire de ressources » hello (valeur par défaut de hello) au lieu du modèle de déploiement « Classiques » hello. Si vous n’avez pas un compte de stockage, découvrez comment tooCreate un compte de stockage. 
* **SQL Data Warehouse**: ce didacticiel déplace hello données locale SQL Server tooSQL entrepôt de données, par conséquent, vous devez toohave un entrepôt de données en ligne. Si vous n’avez pas déjà d’un entrepôt de données, découvrez comment tooCreate un entrepôt de données SQL Azure.

> [!NOTE]
> Les performances sont améliorées si le compte de stockage hello et entrepôt de données hello sont créés dans hello même région.
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a>Étape 1 : Se connecter tooData plateforme Studio avec votre compte Azure
Ouvrez votre navigateur web et accédez toohello [Data Platform Studio](https://www.dataplatformstudio.com/) site Web. Connectez-vous avec hello même compte Azure que vous toocreate utilisé hello stockage compte et les données de l’entrepôt. Si votre adresse de messagerie est associée à un travail ou compte scolaire et un compte Microsoft, que compte hello toochoose a tooyour d’accéder aux ressources.

> [!NOTE]
> S’il s’agit de la première fois à l’aide de données plateforme Studio, vous êtes invité à toogrant hello application autorisation toomanage vos ressources Azure.
> 
> 

## <a name="step-2-start-hello-import-wizard"></a>Étape 2 : Démarrer l’Assistant Importation de hello
À partir de l’écran principal de hello STD, sélectionnez Assistant Importation de hello toostart lien hello importation tooAzure SQL Data Warehouse.

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a>Étape 3 : Installer hello passerelle de données plateforme Studio
tooconnect tooyour de données SQL Server locale, vous devez tooinstall hello STD passerelle. passerelle de Hello est un agent de client qui fournit l’accès tooyour environnement local, extrait des données de hello et il télécharge le compte de stockage tooyour. Vos données ne transitent jamais via les serveurs de Redgate. hello tooinstall passerelle :

1. Cliquez sur hello **créer une passerelle** lien
2. Téléchargement et installation de passerelle hello à l’aide de programme d’installation fourni hello

![][2]

> [!NOTE]
> Hello passerelle peut être installé sur n’importe quel ordinateur avec la base de données de réseau accès toohello source SQL Server. Elle accède à base de données SQL Server hello à l’aide de l’authentification Windows avec informations d’identification hello de l’utilisateur actuel hello.
> 
> 

Une fois installé, hello tooConnected de modifications de statut de passerelle et vous pouvez sélectionner suivant.

## <a name="step-4-identify-hello-source-database"></a>Étape 4 : Identifier la base de données source hello
Bonjour *entrer le nom du serveur* zone de texte, entrez le nom hello du serveur hello qui héberge votre base de données et sélectionnez **suivant**. Puis, à partir du menu déroulant de hello, sélectionnez tooimport des données à partir de la base de données hello.

![][3]

STD inspecte la base de données sélectionnée hello pour les tables tooimport. Par défaut, std importe toutes les tables hello hello de base de données. Vous pouvez sélectionner ou désélectionner des tables en développant hello lier de toutes les Tables. Sélectionnez hello suivant bouton toomove vers l’avant.

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a>Étape 5 : Choisissez une données hello compte toostage de stockage
STD vous invite à entrer un emplacement toostage hello de données. Choisissez un compte de stockage existant dans votre abonnement, puis sélectionnez **Next** (Suivant).

> [!NOTE]
> STD crée un conteneur d’objets blob Bonjour choisi le compte de stockage et utiliser un dossier distinct pour chaque importation.
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a>Étape 6 : créer un entrepôt de données
Ensuite, vous sélectionnez une ligne [Azure SQL Data Warehouse](http://aka.ms/sqldw) tooimport des données hello dans la base de données. Une fois que vous avez sélectionné votre base de données, vous devez toohello de tooconnect tooenter hello informations d’identification de base de données et sélectionnez **suivant**.

![][5]

> [!NOTE]
> STD fusionne les tables de données source hello dans l’entrepôt de données hello. STD vous avertit si le nom de table hello il requiert toooverwrite des tables existantes dans l’entrepôt de données hello. Vous pouvez supprimer les objets existants dans l’entrepôt de données hello en cochant supprimer tous les objets existants avant l’importation.
> 
> 

## <a name="step-7-import-hello-data"></a>Étape 7 : Importer des données de hello
STD confirme que vous souhaitez que les données de salutation tooimport. Cliquez simplement sur hello démarrer Importation bouton toobegin hello l’importation des données.

![][6]

STD affiche une visualisation qui affiche la progression de hello d’extraction et chargement des données de hello depuis hello local SQL Server et hello la progression de l’importation de hello dans SQL Data Warehouse.

![][7]

Une fois l’importation hello est terminée, std affiche un résumé de l’importation de données hello et un rapport des modifications des correctifs de compatibilité hello qui ont été effectuées.

![][8]

## <a name="next-steps"></a>Étapes suivantes
tooexplore vos données dans l’entrepôt de données SQL, commencez par affichage :

* [Interroger Azure SQL Data Warehouse (sqlcmd) (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]
* [Visualiser des données avec Power BI][Visualize data with Power BI]

toolearn plus en détail Data Platform Studio de Redgate :

* [Visitez la page d’accueil de hello STD](http://www.dataplatformstudio.com/)
* [Regardez une démonstration de DPS sur Channel9](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

Pour une vue d’ensemble d’autres façons toomigrate et les charge vos données dans l’entrepôt de données SQL voir :

* [Migrer votre tooSQL solution entrepôt de données][Migrate your solution tooSQL Data Warehouse]
* [Chargement de données dans Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md)

Pour plus de conseils de développement, consultez hello [vue d’ensemble du développement de SQL Data Warehouse](sql-data-warehouse-overview-develop.md).

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
