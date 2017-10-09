---
title: "aaaMoving des données entre bases de données à grande échelle cloud | Documents Microsoft"
description: "Explique comment les partitions toomanipulate et déplacement des données via un service auto-hébergé à l’aide d’élastique de base de données API."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 204fd902-0397-4185-985a-dea3ed7c7d9f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 629dee06e22609e9b61edf93ba5c38d997132d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-between-scaled-out-cloud-databases"></a>Déplacement de données entre des bases de données cloud mises à l’échelle
Si vous êtes un logiciel en tant qu’un développeur de Service, et soudainement votre application subit extraordinaire, vous avez besoin d’une croissance tooaccommodate hello. Vous pouvez donc ajouter d’autres bases de données (partitions). Comment vous redistribuez hello données toohello nouvelles bases de données sans interrompre l’intégrité des données hello ? Hello d’utilisation **outil de fusion et fractionnement** toomove des données à partir de contrainte toohello nouvelles bases de données des bases de données.  

outil de fusion et fractionnement Hello s’exécute comme un service web Azure. Un administrateur ou un développeur utilise hello outil toomove shardlets (à partir d’une partition de données) entre les différentes bases de données (partitions). outil de Hello utilise des partitions carte gestion toomaintain hello service métadonnées de base de données et vérifiez les mappages cohérents.

![Vue d'ensemble][1]

## <a name="download"></a>Télécharger
[Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)

## <a name="documentation"></a>Documentation
1. [Didacticiel d’outil de fusion et de fractionnement de bases de données élastiques](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
2. [Configuration de la sécurité de la fusion et du fractionnement](sql-database-elastic-scale-split-merge-security-configuration.md)
3. [Configuration de la sécurité de la fusion et du fractionnement](sql-database-elastic-scale-split-merge-security-configuration.md)
4. [Gestion des cartes de partitions](sql-database-elastic-scale-shard-map-management.md)
5. [Migrer tooscale-out de bases de données existant](sql-database-elastic-convert-to-use-elastic-tools.md)
6. [Outils de base de données élastique](sql-database-elastic-scale-introduction.md)
7. [Glossaire des outils de base de données élastique](sql-database-elastic-scale-glossary.md)

## <a name="why-use-hello-split-merge-tool"></a>Pourquoi utiliser outil de fusion et fractionnement hello ?
**Flexibilité**

Les applications doivent toostretch avec souplesse au-delà des limites de hello d’une seule base de données de la base de données SQL Azure. Utilisez toomove données de l’outil hello en tant que bases de données toonew nécessaires tout en conservant l’intégrité.

**Fractionnement toogrow** 

Vous devez tooincrease globale croissance toohandle de capacité. toodo, créez une capacité supplémentaire par les données de salutation partitionnement et en distribuant entre bases de données incrémentielle plus jusqu'à ce que les besoins en capacité sont remplies. Il s’agit d’un exemple de fonctionnalité de « split » hello. 

**Fusion tooshrink**

La capacité doit réduire en raison du caractère saisonnier de toohello d’une entreprise. Hello outil vous permet de que développer vers le bas des unités d’échelle toofewer lors de l’activité ralentit. fonctionnalité de fusion » et » Hello Bonjour élastique fusion et fractionnement Service traite cette exigence. 

**Gérer les zones réactives par déplacement des shardlets**

Avec plusieurs locataires par base de données, l’allocation de shardlets tooshards hello peut entraîner des goulots d’étranglement toocapacity sur certaines partitions. Cela nécessite de réaffectation des shardlets ou le déplacement des shardlets occupé toonew ou moins partitions utilisées. 

## <a name="concepts--key-features"></a>Concepts et fonctionnalités clés
**Services hébergés par le client**

fusion et fractionnement Hello est fournie sous la forme d’un service hébergé sur le client. Vous devez déployer et héberger le service de hello dans votre abonnement Microsoft Azure. Hello que vous téléchargez à partir de NuGet contient un toocomplete de modèle de configuration avec les informations de hello pour votre déploiement spécifique. Consultez hello [didacticiel de fusion et fractionnement](sql-database-elastic-scale-configure-deploy-split-and-merge.md) pour plus d’informations. Étant donné que le service de hello s’exécute dans votre abonnement Azure, vous pouvez contrôler et configurer la plupart des aspects de sécurité du service de hello. modèle par défaut de Hello inclut hello options tooconfigure SSL, l’authentification du client de certificat, le chiffrement pour les informations d’identification stockées, protégeant un déni de service et les restrictions IP. Vous trouverez plus d’informations sur hello aspects de sécurité Bonjour suivant document [configuration de la sécurité de la fusion et fractionnement](sql-database-elastic-scale-split-merge-security-configuration.md).

valeur par défaut Hello déployé le service s’exécute avec un seul worker et un rôle web. Chacune utilise la taille de machine virtuelle A1 hello dans Azure Cloud Services. Pendant que vous ne pouvez pas modifier ces paramètres lors du déploiement de package de hello, vous pouvez les modifier après un déploiement réussi dans hello service cloud, en cours d’exécution (via hello portail Azure). Notez que ce rôle de travail hello ne doit pas être configuré pour plus d’informations d’une instance unique pour des raisons techniques. 

**Intégration des cartes de partitions**

service de fusion et fractionnement de Hello interagit avec la carte de partitions hello de l’application hello. Lorsque vous utilisez toosplit de fusion et fractionnement service hello ou plages de fusion ou toomove shardlets entre les partitions, le service de hello maintient automatiquement carte de partitions hello des toodate. toodo par conséquent, le service de hello se connecte toohello partition manager base de données de l’application hello et gère des plages et des mappages en tant que la progression des demandes de fractionnement/fusion/déplacement. Ainsi, cette carte de partitions hello toujours présente une vue à jour lorsque des opérations de fusion et fractionnement se déroulent. Opérations de déplacement de fusion et de shardlet fractionné, sont implémentées en déplaçant un lot de shardlets à partir de la partition cible de hello source partition toohello. Au cours de hello shardlet mouvement opération hello shardlets sujet toohello lot actuel sont marqués comme étant hors connexion dans la carte de partitions hello et ne sont pas disponibles pour les connexions de routage dépendant des données à l’aide de hello **OpenConnectionForKey** API. 

**Connexions cohérentes des shardlets**

Lorsque le déplacement des données démarre un nouveau lot de shardlets, n’importe quel fournie par carte de partitions dépendant des données routage connexions toohello partition stockage hello shardlet sont supprimées et ultérieures des connexions à partir de la carte de partitions hello toohello API ces shardlets sont bloquées pendant le déplacement des données de Hello sont en cours dans des incohérences tooavoid de commande. Connexions des shardlets tooother sur hello même ID de partition est également obtenir arrêtée, mais réussit à nouveau immédiatement lors de la tentative. Une fois le traitement par lots hello est déplacé, hello shardlets sont marqués en ligne pour la partition cible de hello et source de données hello est supprimé de la partition source de hello. service de Hello passe par ces étapes pour chaque lot jusqu'à ce que tous les shardlets ont été déplacés. Cette tentative génère les opérations de suppression de connexion tooseveral pendant l’opération de fractionnement/fusion/déplacement terminée hello hello.  

**Gestion de la disponibilité des shardlets**

Limitation de connexion hello tuer toohello le lot en cours de shardlets, comme expliqué ci-dessus limite l’étendue hello du lot de tooone d’indisponibilité de shardlets à la fois. Cela est préférable à une approche où les partitions complète hello reste hors connexion pour tous les shardlets son hello pendant une opération de fractionnement ou de fusion. taille de Hello d’un lot, défini comme nombre de hello de shardlets distinctes toomove à la fois, est un paramètre de configuration. Elle peut être définie pour chaque opération de fractionnement et de fusion en fonction des besoins de disponibilité et les performances de l’application hello. Notez que la plage de hello est verrouillé dans la carte de partitions hello peut être supérieure à la taille de lot hello. Il s’agit, car le service de hello récupère la taille de la plage hello telles que le nombre réel de hello de valeurs de clé de partitionnement dans les données de salutation correspond approximativement à taille de lot hello. Il s’agit en particulier tooremember important pour les clés de partitionnement peuplées. 

**Stockage des métadonnées**

service de fusion et fractionnement Hello utilise un toomaintain de base de données son état et son tookeep se connecte lors du traitement de la demande. utilisateur de Hello crée cette base de données dans leur abonnement et fournit la chaîne de connexion hello de dans le fichier de configuration hello pour le déploiement du service hello. Les administrateurs à partir de l’organisation de l’utilisateur hello peuvent également connecter toothis cours de demande de base de données tooreview et tooinvestigate des informations détaillées sur les erreurs potentielles.

**Détection de partitionnements**

service de fusion et fractionnement Hello établit la distinction entre les tables (1) partitionnées, les tables de référence (2) et les tables (3) normales. la sémantique d’une opération de fractionnement/fusion/déplacement Hello dépendre de type hello de table hello utilisée et est définie comme suit : 

* **Tables partitionnées**: Split, merge et opérations de déplacement de déplacent les shardlets à partir de la partition de tootarget source. Après l’achèvement réussi de hello demande générale, les shardlets ne sont plus présentes sur la source de hello. Notez que les tables cible hello doivent tooexist sur la partition cible de hello et qu’il ne doivent pas contenir de données dans hello cible plage tooprocessing préalable de l’opération de hello. 
* **Tables de référence**: pour les tables de référence, hello division, fusionner et déplacer des opérations de copier les données de hello à partir de la partition de hello source toohello cible. Toutefois, notez qu’aucune modification se produire sur la partition cible de hello pour une table donnée si n’importe quelle ligne est déjà présente dans le tableau de cibles de hello. table de Hello a toobe vide pour n’importe quel tableau de référence copie tooget opération traitée.
* **Autres Tables**: autres tables peuvent être présents sur hello source ou cible hello d’une opération de fractionnement et de fusion. service de fusion et fractionnement Hello ne tient pas compte de ces tables pour toutes les opérations de copie ou de déplacement des données. Notez, toutefois, qu’ils peuvent interférer avec ces opérations en cas de contraintes.

Hello plus d’informations sur la référence par rapport aux tables partitionnées sont fournies par hello **SchemaInfo** API sur la carte de partitions hello. Hello l’exemple suivant illustre les utiliser hello de ces API sur un smm objet de partition donné carte manager : 

    // Create hello schema annotations 
    SchemaInfo schemaInfo = new SchemaInfo(); 

    // Reference tables 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "region")); 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "nation")); 

    // Sharded tables 
    schemaInfo.Add(new ShardedTableInfo("dbo", "customer", "C_CUSTKEY")); 
    schemaInfo.Add(new ShardedTableInfo("dbo", "orders", "O_CUSTKEY")); 

    // Publish 
    smm.GetSchemaInfoCollection().Add(Configuration.ShardMapName, schemaInfo); 

Hello tables « région » et « pays » sont définies en tant que tables de référence et seront copiés avec les opérations de fractionnement/fusion/déplacement. Les « clients » et les « commandes » sont à leur tour définis comme tables partitionnées. C_CUSTKEY et O_CUSTKEY servent de clé de partitionnement hello. 

**Intégrité référentielle**

service de fusion et fractionnement Hello analyse les dépendances entre les tables et utilise des relations de clé primaire-clé étrangère toostage hello opérations pour déplacer des tables de référence et les shardlets. En général, les tables de référence sont d'abord copiées dans l'ordre de dépendance, puis les shardlets sont copiés dans l'ordre de leurs dépendances au sein de chaque lot. Cela est nécessaire afin que les contraintes sur la partition cible de hello PK-FK sont respectés comme hello nouvelles données arrivent. 

**Cohérence des cartes de partitions et achèvement éventuel**

En présence de hello d’échecs, le service de fusion et fractionnement de hello reprend les opérations après toute coupure de courant et vise toocomplete les demandes de progression. Toutefois, il peut arriver irrécupérable, par exemple, lors de la partition cible de hello est perdue ou compromise au-delà de réparation. Dans ces circonstances, certaines shardlets devait toobe déplacé peut continuer tooreside sur les partitions de source de hello. service de Hello garantit que les mappages de shardlet sont uniquement mis à jour après que les données nécessaires hello a été correctement copiés toohello cible. Shardlets sont supprimés uniquement sur la source de hello une fois que toutes les données ont été copiées toohello cible et les mappages correspondants hello ont été mis à jour avec succès. opération de suppression Hello se produit en arrière-plan de hello lors de la plage de hello est déjà en ligne sur la partition cible de hello. service de fusion et fractionnement Hello garantit toujours l’exactitude des mappages hello stockées dans la carte de partitions hello.

## <a name="hello-split-merge-user-interface"></a>interface utilisateur de la fusion et fractionnement de Hello
package de service de fractionnement-fusion Hello inclut un rôle de travail et un rôle web. rôle web de Hello est demandes de fusion et fractionnement toosubmit utilisé de manière interactive. Hello principaux composants d’interface utilisateur de hello sont les suivantes :

* Type d’opération : le type d’opération hello est une case d’option qui contrôle le type de hello d’opération effectuée par service hello pour cette demande. Vous pouvez choisir entre hello split, merge et déplacez des scénarios. Vous pouvez également annuler une opération précédemment soumise. Vous pouvez utiliser les demandes de fractionnement, de fusionnement et de déplacement pour les cartes de partition de plage. La liste de cartes de partition prend uniquement en charge les opérations de déplacement.
* Carte de partitions : hello section suivante de demander des informations de couverture de paramètres sur carte de partitions hello et hébergement de votre carte de partitions de la base de données hello. En particulier, vous avez besoin de nom de hello tooprovide de serveur de base de données SQL Azure hello et de la base de données d’hébergement hello shardmap, partition de toohello informations d’identification tooconnect mapper la base de données et enfin hello nom de la carte de partitions hello. Actuellement, opération de hello n’accepte qu’un seul jeu d’informations d’identification. Ces informations d’identification ont besoin d’autorisations suffisantes de toohave tooperform modifie la carte de partitions toohello ainsi que les données d’utilisateur toohello sur les partitions hello.
* Plage source (fractionnement et fusion) : une opération de fractionnement et de fusion traite une plage à l’aide de sa clé basse et haute. toospecify une opération avec une valeur clée haute unbounded, cocher hello case à cocher « clé haute est max » et laissez le champ de clé haute hello vide. valeurs clés Hello plage que vous spécifiez ne correspondent pas besoin de tooprecisely à un mappage et ses limites dans votre carte de partitions. Si vous ne spécifiez pas les limites de plage à tout service de hello déduira plage la plus proche hello pour vous automatiquement. Vous pouvez utiliser les mappages actuels hello du tooretrieve script hello GetMappings.ps1 PowerShell dans une carte de partitions donné.
* Comportement de la Source fractionnement (split) : pour les opérations de division, définir la plage source de hello point toosplit hello. Pour cela, en fournissant la clé de partitionnement hello où vous souhaitez hello fractionner toooccur. Bouton d’option utiliser hello spécifier si vous souhaitez que la partie inférieure de hello de hello plage (à l’exclusion de diviser la clé de hello) toomove, ou si vous souhaitez toomove partie supérieure de hello (y compris la clé de fractionnement hello).
* Source de Shardlet (déplacer) : déplacer les opérations sont différentes de fractionner ou fusionner les opérations qu’ils ne nécessitent pas une source de hello toodescribe plage. Une source de déplacement est simplement identifiée par la valeur de clé de partitionnement hello que vous envisagez de toomove.
* Cibler la partition (split) : une fois que vous avez fourni les informations de hello sur la source de hello de votre opération de fractionnement, vous devez toodefine où vous souhaitez hello données toobe copié le serveur de base de données SQL Azure tooby fournissant hello et nom de la base de données pour la cible de hello.
* Plage de la cible (fusion sans base) : les opérations de fusion déplacement des partitions existantes de shardlets tooan. Vous identifiez les partitions existantes hello en fournissant des limites de plage hello de plage existante hello toomerge avec souhaitées.
* Taille du lot : contrôles de taille de lot hello hello nombre de shardlets passera en mode hors connexion à la fois pendant le déplacement des données de hello. Il s’agit d’une valeur entière dans laquelle vous pouvez utiliser plus petites valeurs lorsque vous êtes toolong sensibles des périodes de temps d’arrêt pour les shardlets. Plus grandes valeurs augmentera le temps de hello un shardlet donné est hors connexion mais peut améliorer les performances.
* Id d’opération (Annuler) : Si vous avez une opération en cours n’est plus nécessaire, vous pouvez annuler hello en fournissant son ID d’opération dans ce champ. Vous pouvez récupérer l’ID d’opération hello à partir de la table d’état de demande de hello (voir la Section 8.1) ou de sortie hello dans le navigateur web de hello où vous avez envoyé la demande de hello.

## <a name="requirements-and-limitations"></a>Spécifications et limitations
mise en œuvre actuelle Hello du service de fusion et fractionnement hello est sujet toohello suivant les spécifications et limitations : 

* les partitions Hello doivent tooexist et être inscrits dans la carte de partitions hello avant de pouvoir effectuer une opération de fusion et fractionnement sur ces partitions. 
* service de Hello ne crée pas de tables ou autres objets de base de données automatiquement dans le cadre de ses opérations. Cela signifie que hello de schéma pour les tables partitionnées tout et tables de référence doivent tooexist sur l’opération de fractionnement/fusion/déplacement hello cible partition tooany préalable. En particulier, les tables partitionnées sont requis toobe vide dans la plage hello où les nouveaux shardlets sont toobe ajoutée par une opération de fractionnement/fusion/déplacement. Dans le cas contraire, hello échoue hello de cohérence initiale de la partition cible de hello. Notez que les données de référence sont copiées uniquement si la table de référence hello est vide et qu’il n’y a aucune cohérence garantit également avec les opérations d’écriture simultanées tenu tooother sur les tables de référence hello. Nous vous recommandons ce : lors de l’exécution des opérations de fractionnement/fusion, aucune autre opération d’écriture n’apporter des modifications des tables de référence toohello.
* service de Hello s’appuie sur l’identité de ligne établie par un index unique ou une clé qui inclut des performances de tooimprove clé de partitionnement hello et la fiabilité pour les shardlets de grande taille. Données de toomove de service hello ainsi une granularité encore plus que simplement hello partitionnement par valeur de clé. Cela permet de tooreduce hello maximum d’espace du journal et les verrous sont requises pendant l’opération de hello. Envisagez de créer un index unique ou une clé primaire, y compris la clé de partitionnement hello sur une table donnée si vous souhaitez que toouse que la table avec les demandes de fractionnement/fusion/déplacement. Pour des raisons de performances, clé de partitionnement hello doit être au début colonne clé de hello ou un index de hello hello.
* Au cours de hello de traitement des demandes, certaines données shardlet pouvant être présentes sur la source de hello et la partition cible de hello. Cela est nécessaire tooprotect contre les défaillances pendant le déplacement des shardlets de hello. Hello intégration de fusion et fractionnement avec la carte de partitions hello garantit que les connexions via hello données dépendant routage API à l’aide de hello **OpenConnectionForKey** méthode sur la carte de partitions hello ne voyez pas les états intermédiaires incohérents. Toutefois, quand connexion toohello source ou hello ciblez partitions sans utiliser de hello **OpenConnectionForKey** (méthode), les états intermédiaires incohérents peuvent être visibles lorsque vous allez les demandes de fractionnement/fusion/déplacement. Ces connexions peuvent afficher les résultats de partielles ou en doublons en fonction de minutage de hello ou connexion hello sous-jacente de hello partitions. Cette limitation comprend actuellement les connexions de hello effectuées par les multiples-Shard-requêtes élastique.
* base de données de métadonnées Hello pour le service de fusion et fractionnement hello ne doit pas être partagé entre les différents rôles. Par exemple, un rôle de service de fusion et fractionnement hello en transit nécessaires toopoint tooa des métadonnées différentes base de données au rôle de production hello.

## <a name="billing"></a>Facturation
service de fusion et fractionnement Hello s’exécute comme un service cloud dans votre abonnement Microsoft Azure. Par conséquent, les frais pour les services cloud s’appliquent à instance tooyour du service de hello. Sauf si vous effectuez fréquemment des opérations de fractionnement, de fusion et de déplacement, nous vous recommandons de supprimer votre service cloud de fractionnement et de fusion. Vous économiserez ainsi en coûts d'exécution ou de déploiement d'instances de service cloud. Vous pouvez redéployer et démarrer la configuration de votre exécutable facilement à votre convenance tooperform fractionner ou fusionner les opérations. 

## <a name="monitoring"></a>Surveillance
### <a name="status-tables"></a>Tables d'états
Service de fractionnement-fusion Hello fournit hello **RequestStatus** table dans la base de données du magasin de métadonnées hello pour l’analyse des demandes terminées et en cours. Hello répertorie une ligne pour chaque demande de fusion et fractionnement a été instance toothis envoyé du service de fusion et fractionnement hello. Il donne hello informations pour chaque demande suivantes :

* **Horodatage**: hello heure et date de début de la demande de hello.
* **OperationId**: un GUID qui identifie de façon unique la demande de hello. Cette demande peut également être utilisé toocancel hello opération alors qu’il est encore en cours.
* **État**: hello l’état actuel de la demande de hello. Pour les demandes en cours, il répertorie également hello phase dans le hello demande est en cours.
* **CancelRequest**: un indicateur qui indique si la demande de hello a été annulée.
* **Progression**: une estimation du pourcentage d’achèvement de l’opération de hello. Une valeur de 50 indique que les opération hello sont achevée à 50 % environ.
* **Details**: valeur XML qui fournit un rapport de progression plus détaillé. rapport de progression Hello est régulièrement mis à jour les ensembles de lignes sont copiées à partir de la source tootarget. En cas d’erreurs ou exceptions, cette colonne inclut également des informations plus détaillées sur les échecs de hello.

### <a name="azure-diagnostics"></a>Azure Diagnostics
service de fusion et fractionnement Hello utilise des Diagnostics Windows Azure basé sur Azure SDK 2.5 pour la surveillance et de diagnostics. Vous contrôlez la configuration des diagnostics hello comme expliqué ici : [activation des Diagnostics dans Azure Cloud Services et Machines virtuelles](../cloud-services/cloud-services-dotnet-diagnostics.md). package de téléchargement Hello inclut deux configurations de diagnostics - un pour le rôle web de hello et un pour le rôle de travail hello. Ces configurations de diagnostics pour le service de hello suivent les instructions de hello de [Cloud Service Fundamentals dans Microsoft Azure](https://code.msdn.microsoft.com/windowsazure/Cloud-Service-Fundamentals-4ca72649). Il inclut hello définitions toolog les compteurs de Performance, les journaux IIS, les journaux des événements Windows et les journaux des événements application de fusion et fractionnement. 

## <a name="deploy-diagnostics"></a>Déployer des diagnostics
tooenable d’analyse et de diagnostics à l’aide de la configuration de diagnostic hello pour les rôles web et worker hello fournis par le package NuGet de hello, exécutez hello suivant de commandes à l’aide d’Azure PowerShell : 

    $storage_name = "<YourAzureStorageAccount>" 

    $key = "<YourAzureStorageAccountKey" 

    $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key  


    $config_path = "<YourFilePath>\SplitMergeWebContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWeb" 


    $config_path = "<YourFilePath>\SplitMergeWorkerContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWorker" 

Vous trouverez plus d’informations sur la façon de tooconfigure et déployer des paramètres de diagnostics ici : [activation des Diagnostics dans Azure Cloud Services et Machines virtuelles](../cloud-services/cloud-services-dotnet-diagnostics.md). 

## <a name="retrieve-diagnostics"></a>Récupérer les diagnostics
Vous pouvez accéder facilement vos tests de diagnostic à partir de l’Explorateur de serveurs Visual Studio de hello Bonjour Azure-partie de l’arborescence de l’Explorateur de serveurs hello. Ouvrez une instance de Visual Studio, puis dans la barre de menus hello sur vue et l’Explorateur de serveurs. Cliquez sur hello icône Azure tooconnect tooyour abonnement Azure. Puis accédez tooAzure -> stockage -> <your storage account> -> Tables -> WADLogsTable. Pour plus d’informations, consultez la page [Consultation des ressources de stockage avec l’Explorateur de serveurs](http://msdn.microsoft.com/library/azure/ff683677.aspx). 

![WADLogsTable][2]

Hello WADLogsTable mis en surbrillance dans la figure hello ci-dessus contient hello détaillée des événements du journal des applications du service de fusion et fractionnement hello. Notez que de hello téléchargé de la configuration par défaut hello package est orienté vers un déploiement de production. Par conséquent, intervalle de salutation auquel journaux et les compteurs sont extraites à partir d’instances de service hello est volumineux (5 minutes). Pour le développement et de test, intervalle de salutation inférieure en ajustant des paramètres de diagnostics hello de web de hello ou tooyour de rôle de travail hello a besoin. Avec le bouton droit sur le rôle hello Bonjour Explorateur de serveurs Visual Studio (voir ci-dessus), puis ajustez hello période de transfert dans la boîte de dialogue de hello pour les paramètres de configuration de Diagnostics hello : 

![Configuration][3]

## <a name="performance"></a>Performances
En général, les meilleures performances sont toobe attendu de hello supérieur, niveaux de service plus performant dans la base de données SQL Azure. Les allocations e/s, processeur et mémoire plus élevées pour les niveaux de service supérieurs hello bénéficient de copie en bloc hello et supprimer des opérations hello fusion et fractionnement service utilise. Pour cette raison, augmentez le niveau de service hello pour ces bases de données pour une période limitée, définie.

service de Hello effectue également les requêtes de validation dans le cadre de ses opérations normales. Ces requêtes validation vérifier présence inattendue des données dans la plage de cible hello et assurez-vous que toute opération de fractionnement/fusion/déplacement démarre à partir d’un état cohérent. Ces requêtes toutes les fonctionnent sur les plages de clés de partitionnement définis par l’étendue de hello d’opération de hello et taille de lot hello fourni dans le cadre de la définition de requête hello. Ces requêtes fonctionnent de manière optimale lorsqu’un index est présent qui possède la clé de partitionnement hello comme hello colonne principale. 

En outre, une propriété de l’unicité avec la clé de partitionnement hello en tant que colonne de début hello permettra hello service toouse une approche optimisée qui limite la consommation des ressources en termes d’espace du journal et de la mémoire. Cette propriété de l’unicité est toomove requis des tailles de données de grande taille (au-dessus de 1 Go). 

## <a name="how-tooupgrade"></a>Comment tooupgrade
1. Suivez les étapes de hello dans [déployer un service de fusion et fractionnement](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
2. Modifier votre fichier de configuration de service cloud pour votre déploiement de fusion et fractionnement tooreflect hello nouveaux paramètres de configuration. Un nouveau paramètre obligatoire est hello plus d’informations sur les certificats hello utilisé pour le chiffrement. Un moyen simple de toodo Voici toocompare hello nouveau modèle fichier de configuration à partir de téléchargement hello par rapport à votre configuration existante. Assurez-vous que vous ajoutez des paramètres hello pour « DataEncryptionPrimaryCertificateThumbprint » et « DataEncryptionPrimary » pour les hello et rôle de travail hello.
3. Avant de déployer hello mise à jour tooAzure, assurez-vous que toutes les opérations de fusion en cours d’exécution de fractionnement ont terminé. Facilement faire cela en interrogeant les tables RequestStatus et PendingWorkflows hello d’une base de données de métadonnées de fusion et fractionnement hello pour les demandes en cours.
4. Mettre à jour votre déploiement de service cloud existant pour la fusion et fractionnement dans votre abonnement Azure avec le nouveau package de hello et votre fichier de configuration de service mis à jour.

Vous n’avez pas besoin de tooprovision une nouvelle base de données de métadonnées pour tooupgrade de fusion et fractionnement. nouvelle version de Hello met automatiquement à niveau les vos métadonnées de base de données toohello nouvelle version existante. 

## <a name="best-practices--troubleshooting"></a>Meilleures pratiques et dépannage :
* Définir un locataire de test et tester vos opérations de fractionnement/fusion/déplacement plus importantes avec le client de test hello sur plusieurs partitions. Assurez-vous que toutes les métadonnées sont correctement défini dans votre carte de partitions et que les opérations de hello ne violent pas les contraintes ou les clés étrangères.
* Taille des données client conserver hello test ci-dessus hello taille maximum de données de votre client plus grande problèmes liés à tooensure vous ne rencontrez pas taille des données. Cela vous permet d’évaluer une limite supérieure sur hello temps toomove un seul client autour. 
* Assurez-vous que votre schéma autorise les suppressions. service de fusion et fractionnement Hello requiert des données de tooremove de capacité hello à partir de la partition source de hello une fois que les données de salutation a été correctement copiés toohello cible. Par exemple, **déclencheurs delete** peut empêcher le service de hello à partir de la suppression de données source de hello hello et peut entraîner des opérations toofail.
* clé de partitionnement Hello doit être la colonne de début hello dans votre clé primaire ou la définition de l’index unique. Qui garantit des performances optimales hello pour hello requêtes de validation de fractionnement ou de fusion et pour les opérations de déplacement et la suppression de données réelles hello qui fonctionnent toujours sur les plages de clés de partitionnement.
* Colocaliser votre service de fusion et fractionnement dans hello région et centre de données où se trouvent vos bases de données. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-overview-split-and-merge/split-merge-overview.png
[2]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics.png
[3]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics-config.png

