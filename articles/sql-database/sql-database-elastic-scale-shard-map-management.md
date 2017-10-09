---
title: "aaaScale une base de données SQL Azure | Documents Microsoft"
description: "Comment toouse hello ShardMapManager, la bibliothèque cliente de base de données élastique"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a>Montée en charge des bases de données avec le Gestionnaire de carte de partitions hello
tooeasily montée de bases de données sur SQL Azure, utilisez un gestionnaire de carte de partitions. Gestionnaire de cartes de partitions Hello est une base de données spécial qui gère les informations de mappage global sur toutes les partitions (bases de données) dans un ensemble de partitions. Hello métadonnées permettent à une application tooconnect toohello base de données appropriée en fonction de valeur hello Hello **clé de partitionnement**. En outre, chaque partition dans l’ensemble de hello contient les cartes qui effectuent le suivi des données de partition locale hello (appelé **shardlets**). 

![Gestion des cartes de partitions](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

Comprendre comment ces mappages sont construites est la gestion de carte tooshard essentielles. Cette opération est effectuée à l’aide de hello [ShardMapManager classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), située dans hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md) toomanage partition est associée.  

## <a name="shard-maps-and-shard-mappings"></a>Cartes de partitions et mappages de partitions
Pour chaque partition, vous devez sélectionner le type hello de toocreate de carte de partitions. choix de Hello dépend de l’architecture de base de données hello : 

1. Client unique par base de données  
2. Plusieurs clients par base de données (deux types) :
   1. Mappage de liste
   2. Mappage de plage

Pour un modèle de client unique, créez une carte de partitions de **mappage de liste** . modèle de locataire unique Hello assigne une base de données par client. Il s’agit d’un modèle efficace pour les développeurs SaaS, car il simplifie la gestion.

![Mappage de liste][1]

modèle d’architecture mutualisée Hello affecte plusieurs clients tooa une seule base de données (et vous pouvez distribuer des groupes de clients sur plusieurs bases de données). Utilisez ce modèle lorsque vous attendez que chaque données de petite taille toohave client a besoin. Dans ce modèle, nous affectons une plage d’utilisation de base de données clients tooa **mappage de plage**. 

![Mappage de plage][2]

Ou vous pouvez implémenter un modèle de base de données à l’aide un *mappage de liste* tooassign plusieurs locataires tooa base de données unique. Par exemple, DB1 est toostore utilisé plus d’informations sur l’id de client 1 et 5, et DB2 stocke des données pour les locataires 7 et client 10. 

![Plusieurs clients sur une base de données unique][3] 

### <a name="supported-net-types-for-sharding-keys"></a>Types .Net pris en charge pour les clés de partitionnement
Hello de prise en charge de l’échelle élastique suivant .net Framework des types en tant que clés de partitionnement :

* integer
* long
* guid
* byte[]  
* datetime
* timespan
* datetimeoffset

### <a name="list-and-range-shard-maps"></a>Liste et cartes de partitions de plage
Vous pouvez construire des cartes de partition en utilisant des **listes de valeurs de clés de partitionnement individuelles** ou des **plages de valeurs de clés de partitionnement**. 

### <a name="list-shard-maps"></a>Cartes de partition de liste
**Partitions** contiennent **shardlets** et mappage hello de shardlets tooshards est gérée par une carte de partitions. A **carte de partitions liste** est une association entre les bases de données hello qui font Office de partitions et de hello des valeurs de clés qui identifient les shardlets hello.  **Liste des mappages** sont explicites et différentes valeurs de clé peuvent être mappé toohello même base de données. Par exemple, la clé 1 mappe tooDatabase A, et faire référence à des valeurs de clé 3 et 6 B. la base de données

| Clé | Emplacement de partition |
| --- | --- |
| 1 |Database_A |
| 3 |Database_B |
| 4 |Database_C |
| 6 |Database_B |
| ... |... |

### <a name="range-shard-maps"></a>Cartes de partitions de plage
Dans un **carte de partitions plage**, plage de clés hello est décrit par une paire **[faible valeur, la valeur élevée)** où hello *faible valeur* est hello de clé minimale dans la plage de hello et hello *Valeur élevée* est la première valeur hello plus élevé que hello plage. 

Par exemple, **[0, 100)** inclut tous les entiers égaux ou supérieurs à 0 et inférieurs à 100. Notez que plusieurs plages peut point toohello de base de données et disjoints plages sont pris en charge (par exemple, [100,200) et [400,600) à la fois C point tooDatabase dans l’exemple hello ci-dessous.)

| Clé | Emplacement de partition |
| --- | --- |
| [1,50) |Database_A |
| [50,100) |Database_B |
| [100,200) |Database_C |
| [400,600) |Database_C |
| ... |... |

Chacune des tables hello ci-dessus est un exemple conceptuel d’un **ShardMap** objet. Chaque ligne est un exemple simplifié d’un individu **PointMapping** (pour la carte de partitions liste hello) ou **RangeMapping** (pour la carte de partitions de plage hello) objet.

## <a name="shard-map-manager"></a>Gestionnaire des cartes de partitions
Dans la bibliothèque cliente de hello, Gestionnaire de carte de partitions hello est une collection de cartes de partitions. Hello les données gérées par un **ShardMapManager** instance est conservée dans trois emplacements : 

1. **Carte de partitions globales (GSM)**: vous spécifiez une tooserve de base de données en tant que référentiel hello pour les cartes de partitions et les mappages. Tables spéciales et les procédures stockées sont créées automatiquement des informations toomanage hello. Cela est généralement une petite base de données et accéder à la légère, et ne doit pas être utilisé pour d’autres besoins de l’application hello. Hello tables se trouvent dans un schéma spécial appelé **__ShardManagement**. 
2. **Carte de partitions local (LSM)**: chaque base de données que vous spécifiez toobe une partition est modifié toocontain plusieurs petites tables et des procédures stockées spéciales qui contiennent et gérer des partitions de partitions carte informations toothat spécifique. Ces informations sont redondantes avec informations hello Bonjour GSM, et il permet des informations de mappage des partitions hello application toovalidate mis en cache sans imposer aucune charge sur hello GSM ; application Hello utilise hello LSM toodetermine si un mappage de mise en cache est toujours valide. Hello tables correspondante toohello LSM sur chaque partition sont également dans le schéma de hello **__ShardManagement**.
3. **Cache d’application** : chaque instance d’application accédant à un objet **ShardMapManager** conserve un cache local en mémoire de ses mappages. Elle stocke les informations de routage récupérées récemment. 

## <a name="constructing-a-shardmapmanager"></a>Construction d'un objet ShardMapManager
Un objet **ShardMapManager** est construit à l’aide d’un modèle [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) . Hello  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  méthode utilise les informations d’identification (y compris le nom du serveur hello et le nom de base de données contenant hello GSM) sous forme de hello d’un  **ConnectionString** et retourne une instance d’un **ShardMapManager**.  

**Remarque :** hello **ShardMapManager** doit être instancié une seule fois par domaine d’application, dans le code d’initialisation hello pour une application. La création d’instances supplémentaires de ShardMapManager Bonjour même appdomain, entraîne accrue de la mémoire et l’utilisation du processeur de l’application hello. Un **ShardMapManager** peut contenir n’importe quel nombre de cartes de partitions. Si une carte de partitions peut suffire à de nombreuses applications, il arrive que différents ensembles de bases de données soient utilisés pour différents schémas ou pour des objectifs uniques. Lorsque cela se produit, il est préférable d'employer plusieurs cartes de partitions. 

Dans ce code, une application essaie tooopen existant **ShardMapManager** avec hello [TryGetSqlShardMapManager méthode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).  Si les objets représentant un Global **ShardMapManager** (GSM) ne le faites pas encore exister à l’intérieur de la base de données hello, bibliothèque cliente de hello crée les il à l’aide de hello [CreateSqlShardMapManager méthode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

En guise d’alternative, vous pouvez utiliser Powershell toocreate un nouveau gestionnaire de carte de partitions. Un exemple est disponible [ici](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="get-a-rangeshardmap-or-listshardmap"></a>Obtenir un objet RangeShardMap ou ListShardMap
Après avoir créé une partition de gestionnaire de cartes, vous pouvez obtenir hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) ou [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) à l’aide de hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), ou hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) (méthode).

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a>Informations d'identification de l'administration de carte de partitions
Applications administrent et de manipulent des cartes de partitions sont différentes de celles qui utilisent des connexions de tooroute de cartes de partitions hello. 

mappe les partitions de tooadminister (ajouter ou modifier des partitions, les cartes de partitions, les mappages de partition, etc.), vous devez instancier hello **ShardMapManager** à l’aide de **en lecture/écriture d’informations d’identification disposant des droits sur les deux bases de données GSM de hello et sur chaque base de données qui sert d’une partition**. informations d’identification Hello doivent autoriser pour l’écriture de tables hello dans les deux hello GSM et LSM comme informations de mappage de partitions sont entrées ou modifiées, ainsi que pour la création de tables LSM sur les nouvelles partitions.  

Consultez [informations d’identification utilisées bibliothèque du client de base de données élastique tooaccess hello](sql-database-elastic-scale-manage-credentials.md).

### <a name="only-metadata-affected"></a>Seules les métadonnées sont affectées
Méthodes utilisées pour le remplissage ou de la modification de hello **ShardMapManager** données ne modifient pas les données utilisateur hello sont stockées dans des partitions hello eux-mêmes. Par exemple, les méthodes telles que **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affectent uniquement les métadonnées de mappage partition hello. Ils ne pas suppriment, ajouter ou modifier les données utilisateur contenues dans les partitions hello. Au lieu de cela, ces méthodes sont conçue toobe utilisé conjointement avec des opérations distinctes vous effectuez toocreate ou supprimez des bases de données réelles ou déplacer les lignes à partir d’une seule partition tooanother toorebalance un environnement partitionné.  (hello **fusion et fractionnement** outil fourni avec les outils de base de données élastique se sert de ces API, ainsi que d’orchestrer le déplacement des données réelles entre les partitions.) Consultez [mise à l’échelle à l’aide d’outil de hello fractionnement de base de données élastique-fusion](sql-database-elastic-scale-overview-split-and-merge.md).

## <a name="populating-a-shard-map-example"></a>Exemple de remplissage d'une carte de partitions
Vous trouverez ci-dessous un exemple de séquence d’opérations toopopulate une carte de partitions spécifiques. code de Hello procède comme suit : 

1. Une carte de partitions est créée dans un gestionnaire des cartes de partitions. 
2. métadonnées Hello pour deux partitions différentes sont ajoutée de carte de partitions toohello. 
3. Une variété de mappages de la plage de clés sont ajoutées, et hello contenu globale de la carte de partitions hello est affichés. 

code de Hello est écrite afin que la méthode hello peut être réexécutée si une erreur se produit. Chaque requête teste si une partition ou le mappage existe déjà, avant de tenter de toocreate il. Hello code part du principe que les bases de données nommée **sample_shard_0**, **sample_shard_1** et **sample_shard_2** ont déjà été créés dans le serveur hello référencé par la chaîne **shardServer**. 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

Comme alternative, vous pouvez utiliser PowerShell scripts tooachieve hello même résultat. Certains exemples de hello exemple PowerShell sont disponibles [ici](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).     

Une fois que les cartes de partitions ont été remplies, les applications d’accès aux données peuvent être créées ou adapté toowork avec des cartes de hello. Remplissage ou de la manipulation des mappages de hello ne doit pas avoir lieu à nouveau tant que **mise en page de mappage** doit toochange.  

## <a name="data-dependent-routing"></a>Routage dépendant des données
Gestionnaire de cartes de partitions Hello est plus utilisé dans les applications qui nécessitent des opérations de données spécifiques à l’application de base de données connexions tooperform hello. Ces connexions doivent être associées avec la base de données correcte hello. Cette opération est nommée **Routage dépendant des données**. Pour ces applications, instanciez un objet de gestionnaire de mappage de partitions à partir de la fabrique de hello à l’aide des informations d’identification qui ont un accès en lecture seule sur la base de données GSM hello. Les requêtes individuelles pour les connexions ultérieures fournissent des informations d’identification nécessaires pour la connexion de base de données de la partition appropriée toohello.

Notez que ces applications (à l’aide de **ShardMapManager** ouverte avec des informations d’identification en lecture seule) ne peuvent pas apporter des modifications toohello mappages ou des mappages. Pour cela, vous devez créer des applications d'administration ou des scripts PowerShell qui fourniront des informations d'identification dotées de privilèges élevés comme indiqué précédemment. Consultez [informations d’identification utilisées bibliothèque du client de base de données élastique tooaccess hello](sql-database-elastic-scale-manage-credentials.md).

Pour plus d'informations, consultez [Routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md). 

## <a name="modifying-a-shard-map"></a>Modification d'une carte de partitions
Vous disposez de plusieurs méthodes pour modifier une carte de partitions. Toutes les méthodes suivantes de hello modifier les métadonnées de hello décrivant les partitions hello et leurs mappages, mais ils ne modifient pas physiquement les données dans les partitions hello, ni qu’ils créer ou supprimer des bases de données réelles hello.  Certaines opérations hello sur la carte de partitions hello décrite ci-dessous peut-être toobe coordonné avec des actions administratives que déplacer physiquement les données ou qui ajouter et supprimer des bases de données servant de partitions.

Ces méthodes fonctionnent ensemble comme disponible pour la modification de blocs de construction hello hello distribution globale des données dans votre environnement de base de données partitionnée.  

* tooadd ou supprimer des partitions : utilisez  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  et  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  Hello [Shardmap classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx). 
  
    Hello serveur et base de données qui représente la partition cible de hello doivent déjà exister pour tooexecute de ces opérations. Ces méthodes n’ont pas leur impact sur hello bases de données elles-mêmes, uniquement sur les métadonnées dans la carte de partitions hello.
* toocreate ou supprimer des points ou des plages qui sont mappés toohello partitions : utilisez  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  de hello [RangeShardMapping classe](https://msdn.microsoft.com/library/azure/dn807318.aspx), et  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  Hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)
  
    Nombre des différents points ou des plages peuvent être mappé toohello même ID de partition. Ces méthodes affectent uniquement les métadonnées. Elles n’affectent pas les données qui peuvent déjà être présentes dans les partitions. Si les données doivent toobe supprimé de la base de données de hello dans toobe ordre cohérent avec **DeleteMapping** opérations, vous devez tooperform ces opérations séparément mais conjointement à l’aide de ces méthodes.  
* toosplit des plages existantes en deux ou fusionner les plages adjacentes en une seule : utilisez  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  et  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.  
  
    Notez que fractionne et fusionner les opérations **ne changent pas de clé de toowhich hello partition les valeurs sont mappées**. Un fractionnement s’arrête une plage existante en deux parties, mais laisse les deux en tant que toohello mappé même ID de partition. Une fusion fonctionne sur les deux plages adjacentes qui sont déjà mappé toohello même partition, les fusionner dans une même plage.  déplacement des points ou des plages eux-mêmes entre les partitions Hello doit toobe coordonnée à l’aide de **UpdateMapping** conjointement avec le déplacement des données réelles.  Vous pouvez utiliser hello **fractionnement/fusion** les outils de service qui fait partie de la base de données élastique toocoordinate modifications du mappage de partitions avec le déplacement des données, lorsque le déplacement est nécessaire. 
* toore-map (ou déplacement) points ou des plages toodifferent partitions : utilisez  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.  
  
    Étant donné que les données pouvant nécessiter toobe déplacé de tooanother une partition dans toobe ordre cohérent avec **UpdateMapping** opérations, vous devez tooperform mouvement séparément mais conjointement à l’aide de ces méthodes.
* mappages tootake en ligne et hors connexion : utilisez  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  et  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello état en ligne d’un mappage. 
  
    Certaines opérations des mappages de partitions sont autorisées uniquement lorsque l’état d’un mappage est « hors connexion », notamment **UpdateMapping** et **DeleteMapping**. Lorsqu'un mappage est hors connexion, une demande dépendant des données basée sur une clé incluse dans ce mappage renvoie une erreur. En outre, lorsqu’une plage est tout d’abord mises hors connexion, toutes les partitions toohello affectée de connexions sont alors supprimés automatiquement dans l’ordre tooprevent incomplète des résultats incohérents ou pour les requêtes à l’encontre de plages en cours de modification. 

Les mappages sont des objets immuables dans .Net.  Toutes les méthodes de hello ci-dessus qui modifient les mappages d’invalident également tout toothem de références dans votre code. toomake informatique des séquences de tooperform plus faciles d’opérations qui modifient l’état d’un mappage, toutes les méthodes hello qui modifient un mappage de retournent un nouveau mappage de référence, afin d’opérations peuvent être chaînées. Par exemple, toodelete un mappage dans sm shardmap qui contient la clé de hello 25 existant, vous pouvez exécuter hello suivant : 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a>Ajout d'une partition
Applications souvent besoin toosimply ajouter de nouvelles partitions toohandle données qui sont attendues de nouvelles clés ou des plages de clés pour une carte de partitions qui existe déjà. Par exemple, une application partitionnée par ID client peut-être tooprovision une nouvelle partition pour un nouveau client, ou mensuelle partitionnée de données peut-être une nouvelle partition configurée avant le début de hello de chaque nouveau mois. 

Si hello nouvelle plage de valeurs de clé n’est pas déjà partie d’un mappage existant et aucun déplacement de données est nécessaire, il est la nouvelle partition de hello tooadd très simple et associer la nouvelle clé de hello ou partition toothat de plage. Pour plus d’informations sur l’ajout de nouvelles partitions, consultez [Ajout d’une nouvelle partition](sql-database-elastic-scale-add-a-shard.md).

Toutefois, pour les scénarios qui requièrent le déplacement des données, outil de fusion et fractionnement hello est tooorchestrate nécessaires hello déplacement des données entre les partitions en association avec les mises à jour de partition nécessaire hello. Pour plus d’informations sur l’utilisation de hello yool de fusion et fractionnement, consultez [vue d’ensemble de la fusion de fractionnement](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
