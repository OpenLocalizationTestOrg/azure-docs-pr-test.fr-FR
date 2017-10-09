---
title: "aaaManaging les informations d’identification de la bibliothèque cliente de base de données élastique hello | Documents Microsoft"
description: "Comment tooset hello niveau approprié d’informations d’identification, admin tooread uniquement, pour les applications de base de données élastique"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>Informations d’identification utilisées la bibliothèque cliente de tooaccess hello élastique de base de données
Hello [bibliothèque cliente de base de données élastique](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) utilise trois types différents de hello de tooaccess d’informations d’identification [Gestionnaire de carte de partitions](sql-database-elastic-scale-shard-map-management.md). En fonction de la nécessité de hello, utiliser les informations d’identification de hello avec hello plus bas niveau d’accès possible.

* **Informations d'identification d'administration**: pour créer ou manipuler un gestionnaire des cartes de partitions. (Consultez hello [glossaire](sql-database-elastic-scale-glossary.md).) 
* **Accéder aux informations d’identification**: tooaccess une partition existante mapper manager tooobtain plus d’informations sur les partitions.
* **Informations d’identification de connexion**: tooconnect tooshards. 

Consultez également la section [Gestion des bases de données et des connexions dans la base de données Azure SQL](sql-database-manage-logins.md) 

## <a name="about-management-credentials"></a>À propos des informations d'identification d'administration
Informations d’identification d’administration sont utilisé toocreate un [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) objet pour les applications qui manipulent des cartes de partitions. (Par exemple, consultez [Ajout d’une partition à l’aide des outils de base de données élastique](sql-database-elastic-scale-add-a-shard.md) et [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md)) utilisateur hello de bibliothèque cliente d’élastique hello crée des utilisateurs SQL hello et des connexions SQL et permet de s’assurer que chacun est accordé des autorisations de lecture/écriture hello sur les partitions global hello mappent de base de données et toutes les partitions bases de données. Ces informations d’identification sont la carte de partitions globales hello toomaintain utilisés et les cartes de partitions local de hello lors de la carte de partitions toohello modifications sont effectuées. Par exemple, utiliser objet de gestionnaire map toocreate hello partition hello gestion des informations d’identification (à l’aide de [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

variable de Hello **smmAdminConnectionString** est une chaîne de connexion qui contient les informations d’identification de gestion hello. Hello ID d’utilisateur et mot de passe fournit la base de données de mappage en lecture/écriture access tooboth partitions et des partitions individuelles. chaîne de connexion de gestion Hello inclut également hello serveur nom et la base de données nom tooidentify hello global partition carte de base de données. Voici une chaîne de connexion classique à cet effet :

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

N’utilisez pas les valeurs sous forme de hello de «username@server», utilisez simplement de valeur de « nom d’utilisateur » hello.  Il s’agit, car les informations d’identification doivent fonctionner par rapport à la base de données du gestionnaire carte hello partitions et des partitions individuelles, qui peuvent être sur des serveurs différents.

## <a name="access-credentials"></a>Informations d’identification d’accès
Lorsque vous créez une partition de gestionnaire de cartes dans une application qui ne pas administrer les cartes de partitions, utilisez les informations d’identification disposant des autorisations en lecture seule sur la carte de partitions globales de hello. Hello informations récupérées à partir de la carte de partitions globales de hello sous ces informations d’identification sont utilisées pour [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md) et partitions de hello toopopulate mapper le cache sur hello client. Hello informations d’identification sont fournies via hello même call modèle trop**GetSqlShardMapManager** comme indiqué ci-dessus : 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Notez que hello hello **smmReadOnlyConnectionString** tooreflect utilisation de hello de différentes informations d’identification d’accès de la part de **non-administrateur** utilisateurs : ces informations d’identification ne doivent pas fournir écriture autorisations sur la carte de partitions globales de hello. 

## <a name="connection-credentials"></a>Informations d'identification de connexion
Informations d’identification supplémentaires sont nécessaires lorsque vous utilisez hello [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) méthode tooaccess une partition associée à une clé de partitionnement. Ces informations d’identification besoin tooprovide autorisations pour les tables de correspondance des accès en lecture seule toohello partition locale résidant sur les partitions hello. Il s’agit de validation de la connexion tooperform nécessaires pour le routage dépendant des données sur les partitions hello. Cet extrait de code permet l’accès aux données dans le contexte de hello de routage dépendant des données : 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

Dans cet exemple, **smmUserConnectionString** contient des informations d’identification de l’utilisateur de chaîne de connexion hello pour hello. Pour la base de données SQL Azure, voici une chaîne de connexion classique pour les informations d'identification de l'utilisateur : 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Comme avec les informations d’identification d’administrateur hello, ne pas les valeurs sous forme de hello de «username@server». Utilisez simplement « username ».  Notez également que chaîne de connexion hello ne contient pas de nom de serveur et le nom de la base de données. C’est parce que hello **OpenConnectionForKey** appel dirigera hello toohello de connexion correct de partitions en fonction de la clé de hello. Par conséquent, nom de base de données hello et le nom du serveur ne sont pas fournies. 

## <a name="see-also"></a>Voir aussi
[Gestion des bases de données et des connexions dans Azure SQL Database](sql-database-manage-logins.md)

[Sécurisation de votre base de données SQL](sql-database-security-overview.md)

[Prise en main de Tâches de bases de données élastiques](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

