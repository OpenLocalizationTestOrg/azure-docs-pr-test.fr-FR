---
title: aaaIndexing stockage de Table Azure avec Azure Search | Documents Microsoft
description: "Découvrez comment les données de tooindex stockées dans le stockage Table Azure avec Azure Search"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: abb01a4d807cede310246b34775d8059fceb4456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="index-azure-table-storage-with-azure-search"></a>Indexer le stockage de tables Azure avec Azure Search
Cet article explique comment toouse données tooindex de Azure Search est stockée dans le stockage Azure Table.

## <a name="set-up-azure-table-storage-indexing"></a>Configurer l’indexation du stockage de tables Azure

Vous pouvez configurer un indexeur de stockage de tables Azure à l’aide des ressources suivantes :

* [Portail Azure](https://ms.portal.azure.com)
* [API REST](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations) de la Recherche Azure
* [Kit de développement logiciel .NET (SDK)](https://aka.ms/search-sdk) de la Recherche Azure

Ici, nous allons montrer hello flux à l’aide des API REST de hello. 

### <a name="step-1-create-a-datasource"></a>Étape 1 : Création d’une source de données

Une source de données spécifie le données tooindex, hello informations d’identification tooaccess hello obtenir les données nécessaires et stratégies hello qui permettent d’Azure Search tooefficiently identifient les modifications apportées aux données de hello.

Pour l’indexation de tableau, datasource de hello doit avoir hello propriétés suivantes :

- **nom** est hello nom de datasource de hello au sein de votre service de recherche.
- **type** doit être `azuretable`.
- **informations d’identification** paramètre contient la chaîne de connexion de compte de stockage hello. Consultez hello [spécifier les informations d’identification](#Credentials) pour plus d’informations.
- **conteneur** jeux hello nom de table et une requête facultative.
    - Spécifier le nom de la table hello à l’aide de hello `name` paramètre.
    - Si vous le souhaitez, spécifier une requête à l’aide de hello `query` paramètre. 

> [!IMPORTANT] 
> Si possible, utilisez un filtre sur PartitionKey pour de meilleures performances. Toute autre requête effectue une analyse complète, ce qui entraîne une dégradation des performances pour les grandes tables. Consultez hello [considérations relatives aux performances](#Performance) section.


toocreate une source de données :

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

Pour plus d’informations sur hello créer la source de données API, consultez [créer la source de données](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="ways-toospecify-credentials"></a>Informations d’identification de façons toospecify ####

Vous pouvez fournir des informations d’identification hello pour table hello dans une des manières suivantes : 

- **Chaîne de connexion de compte de stockage un accès complet**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` vous pouvez obtenir des chaîne de connexion hello de hello portail Azure en accédant de toohello **Panneau de compte de stockage** > **paramètres**   >  **Clés** (pour les comptes de stockage classique) ou **paramètres** > **clés d’accès** (pour les ressources Azure Comptes de stockage Manager).
- **Compte de stockage partagé la chaîne de connexion de signature accès**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=t&sp=rl` signature d’accès partagé hello doit avoir hello liste et autorisations de lecture sur les conteneurs (tables dans ce cas) et les objets (lignes de table).
-  **Signature d’accès partagé de table**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<hello signature>&se=<hello validity end time>&sp=r` signature d’accès partagé hello doit disposer d’autorisations de requête (lecture) sur la table de hello.

Pour plus d’informations sur les signatures d’accès partagé au stockage, consultez [Utilisation des signatures d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Si vous utilisez les informations d’identification de signature accès partagé, vous devez informations d’identification de la source de données tooupdate hello régulièrement avec des signatures renouvelé tooprevent leur expiration. Si l’expirent des informations d’identification de signature accès partagé, indexeur de hello échoue avec un message d’erreur similaire trop « informations d’identification fournies dans la chaîne de connexion hello ne sont pas valides ou ont expiré. »  

### <a name="step-2-create-an-index"></a>Étape 2 : Création d’un index
index de Hello spécifie les champs hello dans un document, les attributs de hello, et d’autres constructions cette expérience de recherche de forme hello.

toocreate un index :

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

Pour plus d’informations sur la création d’index, consultez [Création d’un index](https://docs.microsoft.com/rest/api/searchservice/create-index).

### <a name="step-3-create-an-indexer"></a>Étape 3 : Création d’un indexeur
Un indexeur connecte une source de données avec un index de recherche cible et fournit une actualisation planifiée des données tooautomate hello. 

Une fois la source de données et les index hello sont créés, vous êtes indexeur de hello toocreate prêt :

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Cet indexeur s’exécute toutes les deux heures. (l’intervalle de planification hello est défini trop « PT2H ».) toorun un indexeur toutes les 30 minutes, définissez intervalle de salutation trop « PT30M ». intervalle de pris en charge le plus court Hello est de cinq minutes. planification de Hello est facultative. Si omis, un indexeur s’exécute qu’une seule fois lorsqu’il est créé. Toutefois, vous pouvez à tout moment exécuter un indexeur à la demande.   

Pour plus d’informations sur hello créer indexeur API, consultez [créer un indexeur](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="deal-with-different-field-names"></a>Gérer différents noms de champs
Parfois, les noms de champs hello dans votre index existant sont différents des noms de propriété hello dans votre table de. Vous pouvez utiliser des noms de propriété champ mappages toomap hello hello table toohello noms de champs dans votre index de recherche. toolearn en savoir plus sur les mappages de champs, consultez [pont les mappages de champs d’indexeur Azure Search différences hello entre les index de recherche et de sources de données](search-indexer-field-mappings.md).

## <a name="handle-document-keys"></a>Gérer les clés de document
Dans Azure Search, clé de document hello identifie de façon unique un document. Chaque index de recherche doit comporter exactement un champ de clé de type `Edm.String`. champ de clé Hello est requis pour chaque document toohello index est ajouté. (En fait, il hello uniquement champ obligatoire.)

Puisque les lignes d’une table ont une clé composée, Azure Search génère un champ synthétique appelé `Key` qui est une concaténation des valeurs de la clé de partition et de la clé de ligne. Par exemple, si une ligne de PartitionKey est `PK1` et RowKey `RK1`, puis hello `Key` valeur du champ est `PK1RK1`.

> [!NOTE]
> Hello `Key` valeur peut contenir des caractères qui ne sont pas valides dans les clés de document, tels que des tirets. Vous pouvez traiter des caractères non valides à l’aide de hello `base64Encode` [fonction de mappage de champ](search-indexer-field-mappings.md#base64EncodeFunction). Si vous faites cela, n’oubliez pas de tooalso utilisation Base64 sécurisé URL codage lors de la passe des clés de document dans l’API appelle tels que de la recherche.
>
>

## <a name="incremental-indexing-and-deletion-detection"></a>Indexation incrémentielle et détection des suppressions
Lorsque vous configurez un toorun d’indexeur de tableau selon une planification, il répertorie à nouveau les lignes nouvelles ou mises à jour uniquement, comme déterminé par d’une ligne `Timestamp` valeur. Vous n’avez toospecify une stratégie de détection de modification. L’indexation incrémentielle est automatiquement activée pour vous.

tooindicate que certain documents doivent être supprimés à partir de l’index de hello, vous pouvez utiliser une stratégie de suppression réversible. Au lieu de supprimer une ligne, ajoutez un tooindicate propriété qu’elle est supprimée et définir une stratégie de détection de suppression réversible sur datasource de hello. Par exemple, hello suivant stratégie considère qu’une ligne est supprimée si la ligne de hello possède une propriété `IsDeleted` avec la valeur de hello `"true"`:

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a>Considérations relatives aux performances

Par défaut, Azure Search utilise hello suivant filtre de requête : `Timestamp >= HighWaterMarkValue`. Parce que les tables Azure ne sont pas un index secondaire sur hello `Timestamp` champ, ce type de requête nécessite une analyse complète de la table et est par conséquent lent pour les tables volumineuses.


Voici deux approches possibles pour améliorer les performances d’indexation de table. Ces deux approches s’appuient sur l’utilisation de partitions de table : 

- Si vos données peuvent être partitionnées naturellement en plusieurs plages de partition, créez une source de données et un indexeur correspondant pour chaque plage. Chaque indexeur a maintenant tooprocess qu’une plage de partition spécifique, ce qui entraîne de meilleures performances de requête. Si les données hello toobe indexée contient un petit nombre de partitions fixes, meilleures : chaque indexeur procède uniquement à une analyse de la partition. Par exemple, toocreate une source de données pour le traitement d’une plage de partition avec des clés de `000` trop`100`, utilisez une requête comme suit : 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- Si vos données sont partitionnées par heure (par exemple, si vous créez une nouvelle partition, chaque jour ou par semaine), envisagez de hello approche : 
    - Utiliser une requête sous forme de hello : `(PartitionKey ge <TimeStamp>) and (other filters)`. 
    - Surveiller la progression de l’indexeur à l’aide de [obtenir les API d’indexeur état](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status)et mettre à jour régulièrement hello `<TimeStamp>` condition de requête hello en fonction de hello dernière réussite borne-valeur. 
    - Avec cette approche, si vous avez besoin de tootrigger une réindexation complète, vous devez tooreset requête de source de données hello dans l’indexeur de hello tooresetting Ajout. 


## <a name="help-us-make-azure-search-better"></a>Aidez-nous à améliorer Azure Search
Si vous souhaitez nous soumettre des demandes d’ajout de fonctionnalités ou des idées d’amélioration, n’hésitez pas les proposer sur notre [site UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
