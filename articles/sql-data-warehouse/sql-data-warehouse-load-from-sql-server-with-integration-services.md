---
title: "données aaaLoad à partir de SQL Server dans Azure SQL données entrepôt (SSIS) | Documents Microsoft"
description: "Montre comment toocreate un SQL Server Integration Services (SSIS) package toomove des données d’une grande variété de données sources tooSQL l’entrepôt de données."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (SSIS)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Créer des données de tooload de package SQL Server Integration Services (SSIS) à partir de SQL Server dans Azure SQL Data Warehouse. Vous pouvez éventuellement restructurer, transformer et nettoyer les données de hello lorsqu’il transite par le flux de données SSIS hello.

Ce didacticiel présente les procédures suivantes :

* créer un nouveau projet Integration Services dans Visual Studio ;
* Connecter des sources de toodata, y compris SQL Server (en tant que source) et SQL Data Warehouse (en tant que destination).
* Concevoir un package SSIS qui charge des données à partir de la source de hello dans la destination de hello.
* Exécuter des données hello tooload hello SSIS package.

Ce didacticiel utilise SQL Server en tant que source de données hello. SQL Server peut être exécuté en local ou dans une machine virtuelle Azure.

## <a name="basic-concepts"></a>Concepts de base
package de Hello est l’unité hello de travail dans SSIS. Les packages associés sont regroupés dans des projets. Les projets et packages de conception sont créés dans Visual Studio à l’aide de SQL Server Data Tools. conception Hello processus est un processus visual dans laquelle vous faites glisser et déposez des composants à partir de l’aire de conception toohello hello boîte à outils, les connecter et définir leurs propriétés. Une fois que vous avez terminé votre package, vous pouvez éventuellement déployer tooSQL serveur pour la gestion complète, de surveillance et de sécurité.

## <a name="options-for-loading-data-with-ssis"></a>Options de chargement des données avec SSIS
SQL Server Integration Services (SSIS) est un ensemble d’outils flexible qui fournit diverses options permettant de connecter et charger les données dans SQL Data Warehouse.

1. Utilisez un tooSQL de tooconnect entrepôt de données de Destination ADO NET. Ce didacticiel utilise une Destination ADO NET, car il comporte des options de configuration avec un minimum de hello.
2. Utilisez un tooSQL de tooconnect entrepôt de données de Destination OLE DB. Cette option peut fournir des performances légèrement meilleures que hello Destination ADO NET.
3. Utiliser les données de salutation toostage hello tâche de téléchargement Blob Azure dans le stockage d’objets Blob Azure. Utilisez ensuite hello SSIS Execute SQL tâche toolaunch un script de Polybase qui charge les données de hello dans l’entrepôt de données SQL. Cette option fournit des performances optimales hello hello trois options répertoriées ici. tooget hello tâche de téléchargement d’objet Blob Azure, téléchargez hello [Microsoft SQL Server 2016 Integration Services Feature Pack pour Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. toolearn en savoir plus sur Polybase, consultez [Guide de PolyBase][PolyBase Guide].

## <a name="before-you-start"></a>Avant de commencer
toostep dans ce didacticiel, vous devez :

1. **SQL Server Integration Services (SSIS)**. SSIS est un composant de SQL Server qui nécessite une version d’évaluation ou une version sous licence de SQL Server. tooget version d’évaluation de SQL Server 2016 Preview, consultez [SQL Server évaluations][SQL Server Evaluations].
2. **Visual Studio**. tooget hello libre Visual Studio Community Edition, consultez [Visual Studio Community][Visual Studio Community].
3. **SQL Server Data Tools pour Visual Studio (SSDT)**. tooget SQL Server Data Tools pour Visual Studio, consultez [télécharger SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Exemples de données**. Ce didacticiel utilise des exemples de données stockées dans SQL Server dans la base de données AdventureWorks hello comme hello toobe de données source chargé dans l’entrepôt de données SQL. tooget hello base de données AdventureWorks, consultez [bases de données AdventureWorks 2014][AdventureWorks 2014 Sample Databases].
5. **Une base de données SQL Data Warehouse avec les autorisations requises**. Ce didacticiel connecte d’instance de SQL Data Warehouse tooa et charge les données. Vous avez toohave autorisations toocreate une table et tooload des données.
6. **Une règle de pare-feu**. Vous avez toocreate une règle de pare-feu sur SQL Data Warehouse avec l’adresse IP de hello de votre ordinateur local avant de pouvoir télécharger toohello de données SQL Data Warehouse.

## <a name="step-1-create-a-new-integration-services-project"></a>Étape 1 : créer un nouveau projet Integration Services
1. Lancez Visual Studio.
2. Sur hello **fichier** menu, sélectionnez **New | Projet**.
3. Accédez toohello **installé | Modèles | Business Intelligence | Services d’intégration** types de projet.
4. Sélectionnez **Projet Integration Services**. Renseignez les champs **Nom** et **Emplacement**, puis cliquez sur **OK**.

Visual Studio s’ouvre et crée un nouveau projet Integration Services (SSIS). Puis Visual Studio ouvre le concepteur hello pour hello unique nouveau package SSIS (Package.dtsx) dans le projet de hello. Vous consultez hello suivant des zones d’écran :

* Sur la gauche de hello, hello **boîte à outils** de composants SSIS.
* Dans le milieu de hello, hello aire de conception, avec plusieurs onglets. Vous utilisez généralement au moins hello **flux de contrôle** et hello **de flux de données** onglets.
* Sur la droite de hello, hello **l’Explorateur de solutions** et hello **propriétés** volets.
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a>Étape 2 : Créer des flux de données de base hello
1. Faites glisser une tâche de flux de données à partir du centre de toohello hello boîte à outils de l’aire de conception hello (sur hello **flux de contrôle** onglet).
   
    ![][02]
2. Double-cliquez sur hello Data Flow Task tooswitch toohello onglet flux de données.
3. À partir de la liste d’autres Sources hello hello boîte à outils, faites glisser une aire de conception toohello Source ADO.NET. Avec l’adaptateur de source de hello étant toujours sélectionnée, modifier son nom trop**source SQL Server** Bonjour **propriétés** volet.
4. À partir de la liste d’autres Destinations hello Bonjour boîte à outils, faites glisser une aire de conception de Destination ADO.NET toohello sous hello Source ADO.NET. Avec l’adaptateur de destination hello étant toujours sélectionnée, modifier son nom trop**destination de l’entrepôt de données SQL** Bonjour **propriétés** volet.
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a>Étape 3 : Configurer l’adaptateur de source de hello
1. Double-cliquez sur Bonjour source adaptateur tooopen Bonjour **éditeur de Source ADO.NET**.
   
    ![][03]
2. Sur hello **Gestionnaire de connexions** onglet Hello **éditeur de Source ADO.NET**, cliquez sur hello **nouveau** toohello suivant du bouton **Gestionnaire de connexions ADO.NET**hello tooopen de liste **configurer un gestionnaire de connexions ADO.NET** boîte de dialogue zone et créer des paramètres de connexion de base de données SQL Server hello charge les données à partir de laquelle ce didacticiel.
   
    ![][04]
3. Bonjour **configurer un gestionnaire de connexions ADO.NET** boîte de dialogue, cliquez sur hello **nouveau** hello tooopen de bouton **Gestionnaire de connexions** boîte de dialogue zone et créer une connexion de données.
   
    ![][05]
4. Bonjour **Gestionnaire de connexions** boîte de dialogue zone, hello après les choses.
   
   1. Pour **fournisseur**, sélectionnez hello SqlClient Data Provider.
   2. Pour **nom du serveur**, entrez le nom du serveur SQL hello.
   3. Bonjour **ouvrir une session sur le serveur de toohello** section, sélectionnez ou entrez les informations d’authentification.
   4. Bonjour **base de données de se connecter tooa** , sélectionnez la base de données AdventureWorks hello.
   5. Cliquez sur **Tester la connexion**.
      
       ![][06]
   6. Dans la boîte de dialogue hello qui signale les résultats de hello de test de connexion hello, cliquez sur **OK** tooreturn toohello **Gestionnaire de connexions** boîte de dialogue.
   7. Bonjour **Gestionnaire de connexions** boîte de dialogue, cliquez sur **OK** tooreturn toohello **configurer un gestionnaire de connexions ADO.NET** boîte de dialogue.
5. Bonjour **configurer un gestionnaire de connexions ADO.NET** boîte de dialogue, cliquez sur **OK** tooreturn toohello **éditeur de Source ADO.NET**.
6. Bonjour **éditeur de Source ADO.NET**, Bonjour **nom de table de hello ou de vue de hello** liste, sélectionnez hello **Sales.SalesOrderDetail** table.
   
    ![][07]
7. Cliquez sur **aperçu** toosee hello 200 premières lignes de données dans la table de source de hello Bonjour **aperçu des résultats de requête** boîte de dialogue.
   
    ![][08]
8. Bonjour **aperçu des résultats de requête** boîte de dialogue, cliquez sur **fermer** tooreturn toohello **éditeur de Source ADO.NET**.
9. Bonjour **éditeur de Source ADO.NET**, cliquez sur **OK** toofinish configuration de la source de données hello.

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a>Étape 4 : Connecter l’adaptateur de destination hello toohello de l’adaptateur source
1. Sélectionnez l’adaptateur de source de hello sur l’aire de conception hello.
2. Sélectionnez la flèche hello bleu qui s’étend de l’adaptateur de source hello et faites-le éditeur de destination toohello jusqu'à ce qu’il s’enclenche.
   
    ![][10]
   
    Dans un package SSIS classique, vous utilisez un nombre d’autres composants à partir de la boîte à outils SSIS de hello entre la source de hello et hello destination toorestructure, transformation et nettoyez vos données qui traversent le flux de données SSIS hello. tookeep cet exemple aussi simple que possible, nous avons connecté hello source directement toohello destination.

## <a name="step-5-configure-hello-destination-adapter"></a>Étape 5 : Configurer l’adaptateur de destination hello
1. Double-cliquez sur Bonjour destination adaptateur tooopen Bonjour **éditeur de Destination ADO.NET**.
   
    ![][11]
2. Sur hello **Gestionnaire de connexions** onglet Hello **éditeur de Destination ADO.NET**, cliquez sur hello **nouveau** toohello suivant du bouton **Gestionnaire de connexions**hello tooopen de liste **configurer un gestionnaire de connexions ADO.NET** boîte de dialogue zone et créer des paramètres de connexion de base de données de l’entrepôt de données SQL Azure hello charge des données dans laquelle ce didacticiel.
3. Bonjour **configurer un gestionnaire de connexions ADO.NET** boîte de dialogue, cliquez sur hello **nouveau** hello tooopen de bouton **Gestionnaire de connexions** boîte de dialogue zone et créer une connexion de données.
4. Bonjour **Gestionnaire de connexions** boîte de dialogue zone, hello après les choses.
   1. Pour **fournisseur**, sélectionnez hello SqlClient Data Provider.
   2. Pour **nom du serveur**, entrez le nom de l’entrepôt de données SQL hello.
   3. Bonjour **ouvrir une session sur le serveur de toohello** section, sélectionnez **l’authentification d’utilisation SQL Server** et entrez les informations d’authentification.
   4. Bonjour **base de données de se connecter tooa** , sélectionnez une base de données SQL Data Warehouse existante.
   5. Cliquez sur **Tester la connexion**.
   6. Dans la boîte de dialogue hello qui signale les résultats de hello de test de connexion hello, cliquez sur **OK** tooreturn toohello **Gestionnaire de connexions** boîte de dialogue.
   7. Bonjour **Gestionnaire de connexions** boîte de dialogue, cliquez sur **OK** tooreturn toohello **configurer un gestionnaire de connexions ADO.NET** boîte de dialogue.
5. Bonjour **configurer un gestionnaire de connexions ADO.NET** boîte de dialogue, cliquez sur **OK** tooreturn toohello **éditeur de Destination ADO.NET**.
6. Bonjour **éditeur de Destination ADO.NET**, cliquez sur **nouveau** toohello suivant **utiliser une table ou vue** hello tooopen de liste **Create Table** boîte de dialogue toocreate une nouvelle table de destination avec une liste de colonnes qui correspond à la table de source de hello.
   
    ![][12a]
7. Bonjour **Create Table** boîte de dialogue zone, hello après les choses.
   
   1. Modifier le nom hello de table de destination hello trop**SalesOrderDetail**.
   2. Supprimer hello **rowguid** colonne. Hello **uniqueidentifier** type de données n’est pas pris en charge dans l’entrepôt de données SQL.
   3. Modifier le type de données hello Hello **LineTotal** colonne trop**money**. Hello **décimal** type de données n’est pas pris en charge dans l’entrepôt de données SQL. Pour plus d’informations sur les types de données pris en charge, consultez la page [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Cliquez sur **OK** toocreate hello table et retour toohello **éditeur de Destination ADO.NET**.
8. Bonjour **éditeur de Destination ADO.NET**, sélectionnez hello **mappages** onglet toosee comment les colonnes de la source de hello sont mappés toocolumns dans la destination de hello.
   
    ![][13]
9. Cliquez sur **OK** toofinish configuration de la source de données hello.

## <a name="step-6-run-hello-package-tooload-hello-data"></a>Étape 6 : Exécuter les données de salutation hello package tooload
Package d’exécution hello en cliquant sur hello **Démarrer** bouton de barre d’outils hello ou en sélectionnant une de hello **exécuter** options sur hello **déboguer** menu.

Comme package de hello commence toorun, vous voyez jaune tournant roues tooindicate activité ainsi qu’aux nombre hello de lignes traitées jusqu'à présent.

![][14]

Lors de l’exécution de package de hello est terminée, vous consultez coches verte tooindicate réussite ainsi hello nombre total de lignes de données chargées à partir de la destination de toohello hello source.

![][15]

Félicitations ! Vous avez utilisé avec succès des données tooload de SQL Server Integration Services dans Azure SQL Data Warehouse.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur le flux de données SSIS hello. Article de référence : [Flux de données][Data Flow].
* Découvrez comment toodebug et résoudre les problèmes de votre droit de packages dans un environnement de conception hello. Article de référence : [Outils de dépannage pour le développement des packages][Troubleshooting Tools for Package Development].
* Découvrez comment toodeploy votre SSIS les projets et les packages tooIntegration serveur des Services ou tooanother emplacement de stockage. Article de référence : [Déploiement de projets et de packages][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
