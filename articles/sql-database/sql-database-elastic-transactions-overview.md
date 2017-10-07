---
title: "aaaDistributed des transactions entre bases de données de cloud"
description: "Vue d’ensemble des transactions de bases de données élastiques avec la base de données SQL Azure"
services: sql-database
documentationcenter: 
author: torsteng
manager: jhubbard
editor: torsteng
ms.assetid: e14df7a3-7788-4cfb-bcd1-7ad6433ef1f9
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: sql-database
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 9a18f2749108d337bf115b3dc21dd0c7828dd9c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a>Transactions distribuées entre bases de données cloud
Les transactions de bases de données élastique pour base de données SQL Azure (base de données SQL) permettent de toorun les transactions qui s’étendent sur plusieurs bases de données dans la base de données SQL. Transactions de base de données élastique pour base de données SQL sont disponibles pour les applications .NET à l’aide d’ADO .NET et s’intégrer à hello programmation vous est familier à l’aide de hello [System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) classes. bibliothèque de hello tooget, consultez [.NET Framework 4.6.1 (programme d’installation de Web)](https://www.microsoft.com/download/details.aspx?id=49981).

En local, un tel scénario nécessitait généralement d’exécuter Microsoft Distributed Transaction Coordinator (MSDTC). Étant donné que MSDTC n’est pas disponible pour l’application de plateforme en tant que Service dans Azure, les transactions toocoordinate distributed hello capacité a maintenant été intégré directement dans la base de données SQL. Les applications peuvent se connecter à des transactions toolaunch distribué tooany base de données SQL, et une des bases de données hello en toute transparence coordonne les transactions hello distribué, comme indiqué dans la figure suivante de hello. 

  ![Transactions distribuées avec la base de données SQL Azure utilisant les transactions de bases de données élastiques ][1]

## <a name="common-scenarios"></a>Scénarios courants
Transactions de base de données élastique pour base de données SQL activer des applications toomake modifications atomiques toodata stockée dans plusieurs bases de données SQL différent. Aperçu de Hello se concentre sur l’expérience de développement côté client en c# et .NET. Une expérience côté serveur utilisant T-SQL est prévue pour une date ultérieure.  
Hello cibles transactions par la base de données élastique est les scénarios suivants :

* Applications de bases de données multiples dans Azure : avec ce scénario, les données sont partitionnées verticalement sur plusieurs bases de données dans SQL DB, de telle sorte que différents types de données résident sur différentes bases de données. Certaines opérations requièrent toodata de modifications qui est conservée dans deux ou plusieurs bases de données. application Hello utilise des modifications de base de données élastique transactions toocoordinate hello entre bases de données et garantir l’atomicité.
* Applications de base de données partitionnée dans Azure : dans ce scénario, couche de données hello utilise hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md) ou toohorizontally de partitionnement automatique partitionner les données hello entre plusieurs bases de données dans la base de données SQL. Un cas d’utilisation importante est hello besoin tooperform atomique les modifications pour une application mutualisée partitionnée lorsque les modifications sont réparties entre les clients. Considérez par exemple un transfert à partir d’un locataire tooanother, les deux résidant sur les différentes bases de données. Un second cas est affinée partitionnement tooaccommodate besoins en capacité pour un client volumineux, ce qui à son tour généralement implique que certains toostretch de besoins d’opérations atomiques sur plusieurs bases de données utilisé pour hello même locataire. Un troisième cas est données tooreference mises à jour atomiques qui sont répliquées sur les bases de données. Les opérations atomiques, traitées, le long de ces lignes peuvent maintenant être coordonnées entre plusieurs bases de données à l’aide de la version préliminaire de hello.
  Transactions de base de données élastique utilisent atomicité de validation en deux phases tooensure transaction entre bases de données. Il est adapté aux transactions qui impliquent moins de 100 bases de données à la fois dans une même transaction. Ces limites ne sont pas appliquées, mais un doit attendre les performances et le taux de réussite pour toosuffer des transactions de base de données élastique au-delà de ces limites.

## <a name="installation-and-migration"></a>Installation et migration
fonctionnalités de Hello pour les transactions de base de données élastique dans la base de données SQL sont fournies via les bibliothèques .NET de mises à jour toohello System.Data.dll et System.Transactions.dll. Hello DLL vous assurer que la validation en deux phases est utilisée en cas de besoin tooensure atomicité. toostart développement d’applications à l’aide de transactions de base de données élastique, installez [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) ou une version ultérieure. Lors de l’exécution sur une version antérieure du .NET framework de hello, transactions échouent toopromote tooa distribué transaction et une exception sera levée.

Après l’installation, vous pouvez utiliser des transactions de hello distribué API dans System.Transactions avec connexions tooSQL DB. Si vous avez des applications MSDTC existantes à l’aide de ces API, simplement de reconstruire vos applications existantes de .NET 4.6 après l’installation de hello 4.6.1 Framework. Si vos projets ciblent .NET 4.6, ils utilisent automatiquement DLL hello mis à jour à partir de la nouvelle version de Framework hello et les appels d’API de transaction distribuée en association avec tooSQL connexions que DB va réussir.

N’oubliez pas que les transactions de bases de données élastiques ne nécessitent pas d’installer MSDTC. Elles sont en fait gérées directement par et depuis la base de données SQL. Cela simplifie considérablement les scénarios de cloud, car un déploiement de MSDTC n’est pas nécessaire toouse distribué des transactions avec la base de données SQL. Dans la section 4 explique plus en détail comment hello et transactions de base de données élastique toodeploy requis .NET framework avec votre tooAzure d’applications cloud.

## <a name="development-experience"></a>Expérience de développement
### <a name="multi-database-applications"></a>Applications de bases de données multiples
Hello exemple de code suivant utilise hello programmation vous est familier avec .NET System.Transactions. Hello classe TransactionScope établit une transaction ambiante dans .NET. (Une « transaction ambiante » est une qui réside dans le thread en cours de hello.) Toutes les connexions ouvertes dans hello TransactionScope participent à des transactions de hello. Si différentes bases de données participe à, hello transaction est automatiquement avec élévation de privilèges tooa distribué. résultat de Hello de transaction de hello est contrôlé en définissant hello étendue toocomplete tooindicate une validation.

    using (var scope = new TransactionScope())
    {
        using (var conn1 = new SqlConnection(connStrDb1))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = new SqlConnection(connStrDb2))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T2 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }

### <a name="sharded-database-applications"></a>Applications de bases de données partitionnées
Transactions de base de données élastique pour base de données SQL prennent également en charge la coordination de transactions distribuées où vous utilisez hello OpenConnectionForKey méthode connexions tooopen à la bibliothèque client hello élastique de base de données pour une montée en puissance parallèle de données couche. Envisagez le cas où vous devez tooguarantee la cohérence transactionnelle des modifications sur plusieurs valeurs de clé de partitionnement différente. Les partitions de toohello connexions hébergeant les valeurs de clé de partitionnement différente hello sont réparties à l’aide de OpenConnectionForKey. Dans des cas de hello, les connexions de hello peuvent être des partitions de toodifferent telles que vous être assuré de garanties transactionnelles nécessite une transaction distribuée. Hello suivant l’exemple de code illustre cette approche. Il part du principe qu’une variable appelée shardmap est toorepresent utilisé une partition mapper à partir de la bibliothèque cliente de base de données élastique hello :

    using (var scope = new TransactionScope())
    {
        using (var conn1 = shardmap.OpenConnectionForKey(tenantId1, credentialsStr))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = shardmap.OpenConnectionForKey(tenantId2, credentialsStr))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T1 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }


## <a name="net-installation-for-azure-cloud-services"></a>Installation de .NET pour Azure Cloud Services
Azure fournit plusieurs offres toohost les applications .NET. Une comparaison des offres hello est disponible dans [comparaison d’Azure App Service, les Services de cloud computing et Machines virtuelles](../app-service-web/choose-web-site-cloud-service-vm.md). Si hello système d’exploitation invité de l’offre de hello est inférieure à .NET 4.6.1 requis pour les transactions élastiques, vous devez too4.6.1 de système d’exploitation invité tooupgrade hello. 

Pour les Services d’application Azure met à niveau invité toohello que système d’exploitation n’est actuellement pas pris en charge. Pour les Machines virtuelles Azure, connectez-vous dans hello machine virtuelle et exécuter le programme d’installation de hello pour la dernière version de framework .NET hello. Pour les Services de Cloud Azure, vous devez installation hello de tooinclude d’une version plus récente de .NET dans les tâches de démarrage hello de votre déploiement. Hello concepts et les étapes sont documentées dans [installer le .NET sur un rôle de Service Cloud](../cloud-services/cloud-services-dotnet-install-dotnet.md).  

Notez que hello le programme d’installation de .NET 4.6.1 peut nécessiter plus de stockage temporaire pendant hello amorçage processus sur les services de cloud computing Azure que hello du programme d’installation de .NET 4.6. tooensure une installation réussie, vous devez tooincrease un stockage temporaire pour votre service cloud Azure dans votre fichier ServiceDefinition.csdef dans la section de LocalResources hello et paramètres d’environnement hello de votre tâche de démarrage, comme indiqué dans les éléments suivants de hello exemple :

    <LocalResources>
    ...
        <LocalStorage name="TEMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
        <LocalStorage name="TMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
        <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
            <Environment>
        ...
                <Variable name="TEMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TEMP']/@path" />
                </Variable>
                <Variable name="TMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TMP']/@path" />
                </Variable>
            </Environment>
        </Task>
    </Startup>

## <a name="transactions-across-multiple-servers"></a>Transactions sur plusieurs serveurs
Les transactions de bases de données élastiques sont prises en charge sur plusieurs serveurs logiques de la base de données SQL Azure. Lorsque les transactions franchissent les limites du serveur logique, les serveurs participant hello doivent toobe entré dans une relation de communication mutuelle. Une fois que la relation de communication hello a été établie, une base de données dans un des deux serveurs peuvent participer élastiques transactions avec les bases de données à partir de hello hello autre serveur. Avec plus de deux serveurs logiques de fractionnement des transactions, une relation de communication doit toobe en place pour n’importe quelle paire de serveurs logiques.

Utilisez hello suivant d’applets de commande PowerShell toomanage les relations entre serveurs communication pour les transactions de base de données élastique :

* **Nouveau-AzureRmSqlServerCommunicationLink**: utilisez cette applet de commande de toocreate une nouvelle relation de communication entre deux serveurs logiques dans la base de données SQL Azure. relation de Hello est symétrique, ce qui signifie que les deux serveurs peuvent initier des transactions avec hello autre serveur.
* **Get-AzureRmSqlServerCommunicationLink**: utilisez cette applet de commande tooretrieve les communications existantes des relations et leurs propriétés.
* **Remove-AzureRmSqlServerCommunicationLink**: utilisez cette applet de commande de tooremove une relation de communication existante. 

## <a name="monitoring-transaction-status"></a>Surveillance de l’état de transaction
Utilisez les vues de gestion dynamique (DMV) dans l’état de toomonitor de base de données SQL et la progression de vos opérations en cours de la base de données élastique. Tous les tootransactions de vues de gestion dynamique associées sont pertinentes pour les transactions distribuées dans la base de données SQL. Vous pouvez trouver hello liste correspondante de DMV ici : [fonctions (Transact-SQL) et les vues de gestion dynamique connexes Transaction](https://msdn.microsoft.com/library/ms178621.aspx).

Les vues de gestion dynamique ci-dessous sont particulièrement utiles :

* **sys.dm\_tran\_active\_transactions** : répertorie les transactions actives et leur état. Hello colonne de l’UOW (unité de travail) peut identifier les hello enfant différentes transactions appartenant toohello même transaction distribuée. Toutes les transactions de hello comportent de la même transaction distribuée hello même valeur UOW. Consultez hello [documentation de la vue de gestion dynamique](https://msdn.microsoft.com/library/ms174302.aspx) pour plus d’informations.
* **Sys.DM\_tran\_base de données\_transactions**: fournit des informations supplémentaires sur les transactions, telles que la sélection élective de transaction hello dans le journal de hello. Consultez hello [documentation de la vue de gestion dynamique](https://msdn.microsoft.com/library/ms186957.aspx) pour plus d’informations.
* **Sys.DM\_tran\_verrous**: fournit des informations sur les verrous hello actuellement maintenus par les transactions en cours. Consultez hello [documentation de la vue de gestion dynamique](https://msdn.microsoft.com/library/ms190345.aspx) pour plus d’informations.

## <a name="limitations"></a>Limites
Hello actuellement des limites suivantes s’appliquent tooelastic des transactions de base de données dans la base de données SQL :

* Seules les transactions entre les bases de données dans SQL DB sont prises en charge. Les autres fournisseurs de ressources [X/Open XA](https://en.wikipedia.org/wiki/X/Open_XA) et les bases de données résidant à l’extérieur de SQL DB ne peuvent pas participer aux transactions de bases de données élastiques. Cela signifie que les transactions de bases de données élastiques ne peuvent pas s’étendre sur des bases de données SQL Server et SQL Azure locales. Pour les transactions distribuées en local, continuer toouse MSDTC. 
* Seules les transactions coordonnées par le client à partir d’une application .NET sont prises en charge. La prise en charge côté serveur de T-SQL, comme BEGIN DISTRIBUTED TRANSACTION, est planifiée, mais pas encore disponible. 
* Les transactions entre les services WCF ne sont pas prises en charge. Par exemple, vous disposez d’une méthode de service WCF qui exécute une transaction. Englobant appel hello au sein d’une étendue de transaction échoue car un [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception).

## <a name="next-steps"></a>Étapes suivantes
Pour toute question, veuillez contacter toous sur hello [Forum sur la base de données SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) et pour les demandes de fonctionnalités, ajoutez-les toohello [forum de commentaires de la base de données SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



