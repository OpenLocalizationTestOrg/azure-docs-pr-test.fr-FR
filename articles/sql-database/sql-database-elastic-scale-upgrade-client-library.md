---
title: "bibliothèque de client de base de données élastique dernière aaaUpgrade toohello | Documents Microsoft"
description: "Mettre à niveau des applications et des bibliothèques à l’aide de Nuget"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a>Mise à niveau d’une bibliothèque cliente de base de données élastique plus récente d’application toouse hello
Nouvelles versions de hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md) sont disponibles via l’interface de gestionnaire de NuGetPackage NuGetand hello dans Visual Studio. Mises à niveau contiennent des correctifs de bogues et prise en charge de nouvelles fonctionnalités de la bibliothèque cliente de hello.

**Pour la version la plus récente hello :** accédez trop[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Régénérez votre application avec la nouvelle bibliothèque de hello, ainsi que de modifier votre gestionnaire de carte de partitions les métadonnées existantes stockées dans votre toosupport nouvelles fonctionnalités de bases de données SQL Azure.

Effectuez ces étapes dans l’ordre garantit que des versions anciennes de la bibliothèque cliente de hello ne sont plus présentes dans votre environnement lorsque des objets de métadonnées sont mises à jour, ce qui signifie que les objets de métadonnées de l’ancienne version ne sont pas créées après la mise à niveau.   

## <a name="upgrade-steps"></a>Étapes de la mise à niveau
**1. Mettez à niveau vos applications.** Dans Visual Studio, de téléchargement et de référence hello client bibliothèque version la plus récente dans l’ensemble de vos projets de développement qui utilisent la bibliothèque de hello ; reconstruire, puis déployer. 

* Dans votre solution Visual Studio, sélectionnez **Outils** --> **Gestionnaire de package NuGet** -->  **Gérer les packages NuGet pour la solution**. 
* (Visual Studio 2013) Dans le volet gauche de hello, sélectionnez **mises à jour**, puis sélectionnez hello **mise à jour** bouton sur le package de hello **bibliothèque cliente élastique montée en puissance d’Azure SQL de base de données** qui s’affiche dans hello fenêtre.
* (Visual Studio 2015) Définir trop de zone de filtre hello**mise à niveau disponible**. Hello package tooupdate, puis cliquez sur hello **mise à jour** bouton.
* (Visual Studio 2017) Haut hello de boîte de dialogue hello, sélectionnez **mises à jour**. Hello package tooupdate, puis cliquez sur hello **mise à jour** bouton.
* Générez et déployez les applications. 

**2. Mettez à niveau vos scripts.** Si vous utilisez **PowerShell** toomanage de partitions, les scripts [télécharger la version de la nouvelle bibliothèque hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) et copiez-le dans le répertoire hello à partir de laquelle vous exécutez des scripts. 

**3. Mettez à niveau votre service de fractionnement/fusion.** Si vous utilisez hello élastique de base de données outil de fusion et fractionnement tooreorganize données partitionné, [télécharger et déployer la version la plus récente de l’outil de hello hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/). Mise à niveau une procédure détaillée pour hello Service peut être trouvé [ici](sql-database-elastic-scale-overview-split-and-merge.md). 

**4. Mettez à niveau vos bases de données du Gestionnaire de cartes de partitions**. Mettre à niveau les métadonnées hello prise en charge de vos cartes de partitions dans la base de données SQL Azure.  Vous pouvez effectuer cette opération avec PowerShell ou C#. Ces deux options sont expliquées ci-dessous.

***Option 1 : mise à niveau des métadonnées à l’aide de PowerShell***

1. Téléchargement hello dernière version de ligne de commande pour NuGet à partir de [ici](http://nuget.org/nuget.exe) et enregistrer tooa dossier. 
2. Ouvrez une invite de commandes, accédez toohello même dossier et problème hello commande :`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`
3. Recherchez le sous-dossier toohello contenant hello nouvelle DLL version du client que vous avez simplement téléchargé, par exemple :`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`
4. Télécharger scriptlet mise à niveau du client de base de données élastique hello de hello [centre de scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), et enregistrez-le dans hello même dossier contenant hello DLL.
5. À partir de ce dossier, exécutez « PowerShell.\upgrade.ps1 » à partir de l’invite de commandes hello et suivez les invites de hello.

***Option 2 : mise à niveau des métadonnées à l’aide de C#***

Vous pouvez également créer une application Visual Studio qui ouvre votre ShardMapManager, effectue une itération sur toutes les partitions et effectue la mise à jour des métadonnées hello en appelant des méthodes de hello [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) et [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) comme dans cet exemple : 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

Ces méthodes de mise à niveau des métadonnées peuvent être appliquées plusieurs fois sans risque. Par exemple, si une version antérieure du client crée par inadvertance une partition une fois que vous avez déjà mis à jour, vous pouvez réexécuter mise à niveau sur toutes les partitions tooensure que hello dernière version de métadonnées est présente dans l’ensemble de votre infrastructure. 

**Remarque :** à-date de publication de nouvelles versions de la bibliothèque cliente de hello continuer toowork avec les versions antérieures de métadonnées du Gestionnaire de carte de partitions hello sur la base de données SQL Azure et vice versa.   Toutefois, parti tootake de certaines des nouvelles fonctionnalités de hello dans hello dernière version du client, métadonnées doit toobe mis à niveau.   Notez que les mises à niveau de métadonnées n’affectera pas les données utilisateur ou les données spécifiques à l’application, seuls les objets créés et utilisés par hello Gestionnaire de carte de partitions.  Et applications continuent toooperate via la séquence de mise à niveau hello décrite ci-dessus. 

## <a name="elastic-database-client-version-history"></a>Historique des versions du client des bases de données élastiques
Pour l’historique de version, accédez trop[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

