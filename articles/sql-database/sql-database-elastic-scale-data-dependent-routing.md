---
title: "aaaData dépendant de routage avec la base de données SQL Azure | Documents Microsoft"
description: "Comment toouse hello classe ShardMapManager dans les applications .NET pour une fonctionnalité de bases de données partitionnées dans base de données SQL Azure, le routage dépendant des données"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a>Routage dépendant des données
**Routage dépendant des données** hello capacité toouse hello données dans une requête tooroute hello demande tooan base de données appropriée. Il s’agit d’un modèle fondamental quand vous travaillez avec des bases de données partitionnées. contexte de requête Hello peut-être également être utilisés tooroute demande de hello, surtout si la clé de partitionnement hello n’est pas partie de la requête de hello. Chaque requête spécifique ou une transaction dans une application à l’aide de routage dépendant des données est limitée tooaccessing une base de données par requête. Pour les outils élastique de base de données de SQL Azure hello, cet acheminement s’effectue par hello  **[ShardMapManager classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  dans les applications ADO.NET.

application Hello n’a pas besoin tootrack différentes chaînes de connexion ou les emplacements de base de données associés à différentes tranches de données dans un environnement de partitionnée hello. Au lieu de cela, hello [Gestionnaire de carte de partitions](sql-database-elastic-scale-shard-map-management.md) ouvre les connexions toohello correct bases de données si nécessaire, en fonction des données de hello dans la carte de partitions hello et valeur hello de clé de partitionnement hello qui est la cible de hello de demande de l’application hello. Hello clé est généralement hello *customer_id*, *tenant_id*, *date_key*, ou tout autre identificateur spécifique qui est un paramètre fondamentaux de la demande de base de données hello). 

Pour plus d’informations, consultez [Augmentation de la taille des instances SQL Server avec le routage dépendant des données](https://technet.microsoft.com/library/cc966448.aspx).

## <a name="download-hello-client-library"></a>Télécharger la bibliothèque cliente de hello
classe de hello tooget, installation hello [bibliothèque cliente de base de données élastique](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a>Utilisation d’une classe ShardMapManager dans une application de routage dépendant des données
Les applications doivent instancier hello **ShardMapManager** pendant l’initialisation, à l’aide d’appel de fabrique hello  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**. Dans cet exemple, une classe **ShardMapManager** et un objet **ShardMap** spécifique qu’elle contient sont initialisés. Cet exemple affiche hello GetSqlShardMapManager et [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) méthodes.

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a>Utilisez la plus faible privilège d’informations d’identification possibles pour l’obtention de carte de partitions hello
Si une application est la manipulation pas de carte de partitions hello lui-même, informations d’identification de hello utilisées dans la méthode de fabrique hello doivent avoir des autorisations uniquement en lecture seule sur hello **carte de partitions globales** base de données. Ces informations d’identification sont en général différentes de gestionnaire de carte de partitions informations d’identification utilisées tooopen connexions toohello. Voir aussi [informations d’identification utilisées bibliothèque du client de base de données élastique tooaccess hello](sql-database-elastic-scale-manage-credentials.md). 

## <a name="call-hello-openconnectionforkey-method"></a>Appelez la méthode de OpenConnectionForKey hello
Hello  **[ShardMap.OpenConnectionForKey méthode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  retourne une connexion ADO.Net prêt pour l’émission de commandes toohello base de données appropriée en fonction de valeur hello Hello **clé**paramètre. Les informations de partition sont mis en cache dans une application hello en hello **ShardMapManager**, de sorte que ces demandes n’impliquent généralement une recherche de base de données par rapport à hello **carte de partitions globales** base de données. 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* Hello **clé** paramètre est utilisé comme clé de recherche dans hello partition carte toodetermine hello base de données appropriée pour la demande de hello. 
* Hello **connectionString** est toopass utilisées seules informations d’identification utilisateur hello pour les connexions hello souhaité. Aucun nom de base de données ou le nom du serveur sont inclus dans ce *connectionString* étant donné que la méthode hello déterminera la base de données hello et serveur à l’aide de hello **ShardMap**. 
* Hello  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  doit être défini trop**ConnectionOptions.Validate** si un environnement où mappe les partitions peut changer et les lignes peuvent déplacer des bases de données tooother comme un résultat des opérations de fractionnement ou de fusion. Cela implique une carte de partitions local de toohello de requête brève sur hello base de données cible (pas un mappage de partitions globales toohello) avant la connexion de hello est remis toohello application. 

Si la validation par rapport à la carte de partitions local de hello hello échoue (indiquant que le cache de hello est incorrecte), hello Gestionnaire de carte de partitions interroge hello global partition carte tooobtain hello nouvelle valeur correcte pour la recherche de hello, mettre à jour le cache de hello et obtenir et de retour hello connexion de base de données appropriée. 

Utilisez **ConnectionOptions.None** uniquement quand aucune modification de mappage de carte n’est prévue pendant qu’une application est en ligne. Dans ce cas, hello mis en cache les valeurs peuvent être considérées comme tooalways soit correct, et la base de données hello validation supplémentaire aller-retour appel toohello cible peut être ignorée en toute sécurité. Cela réduit le trafic de base de données. Hello **connectionOptions** peut également être définie par une valeur dans un tooindicate de fichier de configuration, si des modifications de partitionnement sont prévues ou non pendant une période donnée.  

Cet exemple utilise la valeur hello de clé entière **CustomerID**, en utilisant un **ShardMap** objet nommé **customerShardMap**.  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

Hello **OpenConnectionForKey** méthode retourne un nouveau déjà ouvert connexion toohello base de données correcte. Les connexions utilisées de cette manière tirent pleinement parti du regroupement de connexions ADO.Net. Tant que les transactions et les demandes peuvent être satisfaites en une seule partition à la fois, ce doit être la seule modification hello nécessaire dans une application déjà à l’aide d’ADO.Net. 

Hello  **[OpenConnectionForKeyAsync méthode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  est également disponible si votre application permet d’utiliser la programmation asynchrone avec ADO.Net. Son comportement est données hello dépendantes routage équivalent de l’objet ADO. De NET  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  (méthode).

## <a name="integrating-with-transient-fault-handling"></a>Intégration de la gestion des erreurs temporaires
Une meilleure pratique du développement d’applications d’accès aux données dans le cloud de hello est tooensure que transitoires sont interceptées par application hello et que les opérations de hello sont retentées plusieurs fois avant de lever une erreur. La gestion des erreurs temporaires pour les applications cloud est traitée à la page [Gestion des erreurs temporaires](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx). 

Gestion d’erreurs transitoires peut coexister naturellement avec le modèle de routage dépendant des données hello. demande d’accès données hello tooretry notamment hello est Hello primordiale **à l’aide de** bloc qui a obtenu la connexion de routage dépendant des données hello. exemple Hello ci-dessus peut être réécrit comme suit (Notez le changement en surbrillance). 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a>Exemple : routage dépendant des données avec gestion des erreurs temporaires
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


Packages de gestion d’erreurs transitoires tooimplement nécessaires sont téléchargés automatiquement lorsque vous générez l’application d’exemple hello élastique de base de données. Les packages sont également disponibles séparément dans [Enterprise Library - Bloc des applications de gestion des erreurs temporaires](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/). Utilisez la version 6.0 ou ultérieure. 

## <a name="transactional-consistency"></a>Cohérence transactionnelle
Propriétés transactionnelles sont garanties pour toutes les partitions de tooa local d’opérations. Par exemple, les transactions soumises via le routage dépendant des données s’exécuter dans hello étendue de partition cible de hello pour la connexion de hello. À ce stade, il n'existe aucune fonctionnalité fournie pour l'inscription de plusieurs connexions dans une transaction, et par conséquent, il n'existe aucune garantie transactionnelle lors des opérations effectuées sur les partitions.

## <a name="next-steps"></a>Étapes suivantes
Voir toodetach une partition ou une partition, de tooreattach [à l’aide des problèmes du mappage de partitions hello RecoveryManager classe toofix](sql-database-elastic-database-recovery-manager.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

