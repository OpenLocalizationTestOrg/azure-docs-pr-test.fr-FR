---
title: "Opérations de l’indexeur (API REST du service Recherche Azure : 2015-02-28-Preview) | Microsoft Docs"
description: "Opérations de l'indexeur (API REST du service Azure Search : 2015-02-28-Preview)"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>Opérations de l'indexeur (API REST du service Azure Search : 2015-02-28-Preview)
> [!NOTE]
> Cet article décrit les indexeurs Bonjour [2015-02-28-Preview REST API](search-api-2015-02-28-preview.md). Cette version de l'API ajoute des versions préliminaires d’un indexeur de stockage d’objets blob Azure avec extraction des documents et un indexeur de stockage de tables Azure, ainsi que d’autres améliorations. Hello API prend également en charge les indexeurs (GA) généralement disponibles, y compris les indexeurs pour la base de données SQL Azure, SQL Server sur des machines virtuelles Azure et base de données Azure Cosmos.
> 
> 

## <a name="overview"></a>Vue d'ensemble
Azure Search peut s’intégrer directement avec des sources de données courantes, suppression hello besoin toowrite code tooindex vos données. tooset de cela, vous pouvez appeler toocreate des API Azure Search hello et gérer **indexeurs** et **des sources de données**. 

Un **indexeur** est une ressource qui connecte des sources de données à des index de recherche cibles. Un indexeur est utilisé dans hello suivant façons : 

* Effectuer une copie ponctuelle des données de hello toopopulate un index.
* Un index avec des modifications dans la source de données hello selon un calendrier de synchronisation. planification de Hello fait partie de la définition d’indexeur hello.
* Appeler à la demande tooupdate un index en fonction des besoins. 

Un **indexeur** est utile lorsque vous souhaitez index tooan de mises à jour régulières. Vous pouvez configurer une planification incluse dans le cadre d'une définition d'indexeur, ou l'exécuter à la demande à l'aide de la commande [Exécuter l'indexeur](#RunIndexer) 

A **source de données** spécifie les données toobe indexée, informations d’identification tooaccess hello des données et stratégies tooenable Azure Search tooefficiently identifier les modifications apportées aux données hello (tel que modifié ou supprimé des lignes dans une table de base de données). Elle est définie comme une ressource indépendante utilisable par plusieurs indexeurs.

Hello les sources de données suivantes est actuellement prises en charge :

* **Base de données Azure SQL** et **SQL Server sur les machines virtuelles Azure**. Pour obtenir une procédure pas à pas ciblée, consultez [cet article](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 
* **Azure Cosmos DB**. Pour obtenir une procédure pas à pas ciblée, consultez [cet article](search-howto-index-documentdb.md). 
* **Stockage d’objets Blob Azure**, y compris formats de document suivants de hello : PDF, Microsoft Office (DOCX/DOC, XSLX/XLS, PPTX/PPT, MSG), HTML, XML, ZIP et texte brut des fichiers (y compris le JSON). Pour obtenir une procédure pas à pas ciblée, consultez [cet article](search-howto-indexing-azure-blob-storage.md).
* **Stockage Table Azure**. Pour obtenir une procédure pas à pas ciblée, consultez [cet article](search-howto-indexing-azure-tables.md).

Nous envisageons d’ajouter la prise en charge pour les sources de données supplémentaires dans hello futures. toohelp nous hiérarchiser ces décisions, veuillez fournir vos commentaires sur hello [forum de commentaires d’Azure Search](http://feedback.azure.com/forums/263029-azure-search).

Consultez [limites de Service](search-limits-quotas-capacity.md) pour maximum limite les ressources de source tooindexer et les données associées.

## <a name="typical-usage-flow"></a>Flux d'utilisation typique
Vous pouvez créer et gérer des index dans le service Azure Search par le biais de simples requêtes HTTP (POST, GET, PUT, DELETE) sur une ressource `data source` ou `indexer` spécifique.

La configuration de l'indexation automatique est généralement un processus en quatre étapes :

1. Identifier la source de données de hello qui contient les données hello doit toobe indexé. Gardez à l’esprit que Azure Search ne peut-être pas en charge tous les types de données hello présents dans votre source de données. Consultez [prise en charge des types de données](https://msdn.microsoft.com/library/azure/dn798938.aspx) pour la liste hello.
2. Créez un index Azure Search dont le schéma est compatible avec votre source de données.
3. Créez une source de données Azure Search comme décrit dans [Création d'une source de données](#CreateDataSource).
4. Créez un indexeur Azure Search comme décrit dans [Création d'indexeur](#CreateIndexer).

Vous devez prévoir de créer un indexeur pour chaque association source de données/index cible. Vous pouvez avoir plusieurs indexeurs écrivant dans hello même index et que vous pouvez réutiliser hello même source de données pour plusieurs indexeurs. Toutefois, un indexeur peut uniquement utiliser une source de données à la fois et ne peut écrire tooa seul index. 

Après avoir créé un indexeur, vous pouvez récupérer son état d’exécution à l’aide de hello [obtenir le statut indexeur](#GetIndexerStatus) opération. Vous pouvez également exécuter un indexeur à tout moment (au lieu d’ou ajout toorunning il périodiquement selon une planification) à l’aide de hello [exécuter l’indexeur](#RunIndexer) opération.

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>Création d'une source de données
Dans Azure Search, une source de données est utilisée avec les indexeurs, qui fournit des informations de connexion hello pour l’actualisation des données ad hoc ou planifiée d’un index de la cible. Vous pouvez créer une source de données au sein d'un service Azure Search à l'aide d'une requête HTTP POST.

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Vous pouvez également utiliser une requête PUT et spécifiez le nom de source de données hello sur hello URI. Si la source de données hello n’existe pas, il sera créé.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> nombre maximal de Hello de sources de données autorisé varie en fonction du niveau de tarification. service gratuit de Hello permet à des sources de données too3. Le service standard autorise 50 sources de données. Pour plus d’informations, consultez [Limites de service](search-limits-quotas-capacity.md) .
> 
> 

**Requête**

Le protocole HTTPS est requis pour toutes les requêtes de service. Hello **créer une Source de données** demande peut être construite à l’aide d’une méthode POST ou PUT. Lors de l’utilisation de POST, vous devez fournir un nom de source de données dans le corps de la demande, ainsi que la définition de source de données hello hello. Avec PUT, nom de hello fait partie de l’URL de hello. Si la source de données hello n’existe pas, il est créé. S’il existe déjà, il est mis à jour toohello nouvelle définition. 

nom de source de données Hello doit être en minuscules, commencer par une lettre ou un chiffre, contenir sans barres obliques ni points et être inférieure à 128 caractères. Après avoir démarré le nom de source de données hello par une lettre ou un chiffre, reste hello du nom de hello peut inclure toute lettre, le numéro et des tirets, tant que les tirets hello ne soient pas contigus. Pour en savoir plus, consultez [Règles d'affectation des noms](https://msdn.microsoft.com/library/azure/dn857353.aspx) .

Hello `api-version` est requis. version actuelle de Hello est `2015-02-28`.

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif. 

* `Content-Type`: requis. Définissez cette propriété trop`application/json`
* `api-key`: obligatoire. Hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il s’agit d’une valeur de chaîne, d’un service de tooyour unique. Hello **créer une Source de données** demande doit inclure un `api-key` en-tête défini la clé d’administration tooyour (en tant que clé de requête tooa exécutée). 

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour [Azure Portal](https://portal.azure.com/). Consultez [créer un service de recherche dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

<a name="CreateDataSourceRequestSyntax"></a>
**Syntaxe du corps de la requête**

corps Hello de demande de hello contient une définition de source de données, qui inclut le type de source de données hello, données de salutation tooread informations d’identification, ainsi qu’une détection de changement des données facultatives et identifient les stratégies qui sont utilisée tooefficiently de détection de suppression de données modifiées ou les données supprimées dans la source de données hello lorsqu’il est utilisé avec un indexeur planifié à intervalles réguliers. 

syntaxe Hello pour structurer la charge utile de demande hello est comme suit. Vous trouverez un exemple de requête dans cette rubrique.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

La demande contient hello propriétés suivantes : 

* `name`: requis. nom Hello hello de source de données. Un nom de source de données doit uniquement contenir des lettres minuscules, des chiffres ou des tirets, ne peut commencer ni se terminer par des tirets, et est limitée too128 caractères.
* `description`: une description facultative. 
* `type`: requis. Doit être un des types de sources de données hello pris en charge :
  * `azuresql` - Base de données Azure SQL ou SQL Server sur les machines virtuelles Azure
  * `documentdb` - Azure Cosmos DB
  * `azureblob` - Stockage Blob Azure
  * `azuretable` - Stockage Table Azure
* `credentials`:
  * Hello requis `connectionString` propriété spécifie la chaîne de connexion hello pour la source de données hello. format Hello hello de chaîne de connexion dépend du type de source de données hello : 
    * Pour SQL Azure, il s’agit de chaîne de connexion SQL Server habituelle hello. Si vous utilisez la chaîne de connexion hello hello tooretrieve portail Azure, utilisez hello `ADO.NET connection string` option.
    * Pour la base de données Azure Cosmos, chaîne de connexion hello doit être Bonjour suivant le format : `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`. Toutes les valeurs de hello sont requises. Vous pouvez les trouver dans hello [portail Azure](https://portal.azure.com/).  
    * Pour les objets Blob Azure et le stockage de Table, il s’agit de chaîne de connexion de compte de stockage hello. le format Hello est décrit [ici](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/). Un protocole de point de terminaison HTTPS est obligatoire.  
* `container`, requise : Spécifie hello tooindex de données à l’aide de hello `name` et `query` propriétés : 
  * `name` (obligatoire) :
    * SQL Azure : Spécifie hello table ou vue. Vous pouvez utiliser des noms qualifiés par schéma, tels que `[dbo].[mytable]`.
    * DocumentDB : Spécifie la collection de hello. 
    * Stockage d’objets Blob Azure : Spécifie un conteneur de stockage hello.
    * Stockage de Table Azure : Spécifie le nom hello de table de hello. 
  * `query`(facultatif) :
    * DocumentDB : vous permet de toospecify une requête qui aplanit une disposition de document JSON arbitraire dans un schéma plat Azure Search peut indexer.  
    * Stockage d’objets Blob Azure : vous permet de toospecify un dossier virtuel dans le conteneur d’objets blob hello. Par exemple, pour le chemin d’accès de l’objet blob `mycontainer/documents/blob.pdf`, `documents` peut être utilisée comme dossier virtuel de hello.
    * Stockage de Table Azure : vous permet de toospecify une requête que les filtres hello ensemble de toobe lignes importée.
    * Azure SQL : requête non prise en charge. Si vous avez besoin de cette fonctionnalité, veuillez voter pour [cette suggestion](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* Hello facultatif `dataChangeDetectionPolicy` et `dataDeletionDetectionPolicy` propriétés sont décrites ci-dessous.

<a name="DataChangeDetectionPolicies"></a>
**Stratégies de détection des modifications de données**

objectif Hello d’une donnée de modifier la stratégie de détection est tooefficiently identifient les éléments de données modifiées. Stratégies prises en charge varient selon le type de source de données hello. Les sections ci-dessous décrivent chaque stratégie. 

***Stratégie de détection des modifications de limite supérieure*** 

Utilisez cette stratégie lorsque votre source de données contient une colonne ou propriété répondant hello suivant des critères :

* Toutes les insertions spécifient une valeur pour la colonne de hello. 
* Élément de tooan toutes les mises à jour également modifier valeur hello de colonne de hello. 
* valeur Hello de cette colonne augmente à chaque modification.
* Les requêtes que vous utilisent un clause filtre similaire qui suit toohello `WHERE [High Water Mark Column] > [Current High Water Mark Value]` peuvent être exécutées efficacement.

Par exemple, lors de l’utilisation de sources de données SQL Azure, une liste indexées `rowversion` colonne est hello le candidat idéal pour une utilisation avec la stratégie de limite supérieure hello. 

Cette stratégie peut être spécifiée comme suit :

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

Lorsque vous utilisez des sources de données de base de données Azure Cosmos, vous devez utiliser hello `_ts` cette propriété est fournie par la base de données Azure Cosmos. 

Lorsque vous utilisez des sources de données d’objets Blob Azure, Azure Search automatiquement utilise une limite supérieure Modifier stratégie de détection en fonction de l’horodatage de dernière modification d’un objet blob ; vous n’avez pas besoin toospecify une telle stratégie vous-même.   

***Stratégie SQL de détection des modifications intégrée***

Si votre base de données SQL prend en charge le [suivi des modifications](https://msdn.microsoft.com/library/bb933875.aspx), nous recommandons d'utiliser la stratégie SQL de suivi des modifications intégrée. Cette stratégie permet le suivi des modifications plus efficace de hello et permet des lignes de tooidentify supprimé d’Azure Search sans que vous ayez toohave une colonne explicite « suppression réversible » dans votre schéma.

Suivi des modifications intégrée sont prise en charge avec hello versions de base de données SQL Server suivantes : 

* SQL Server 2008 R2, si vous utilisez SQL Server on Azure VMs.
* Azure SQL Database V12, si vous utilisez Azure SQL Database.  

En cas d'utilisation d'une stratégie SQL de suivi des modifications intégrée, ne spécifiez pas de stratégie de détection des suppressions de données distincte. Cette stratégie intègre la prise en charge de l'identification des lignes supprimées. 

Elle n’est utilisable que sur des tables, non sur des vues. Vous devez tooenable suivi des modifications pour table hello à l’aide d’avant de pouvoir utiliser cette stratégie. Pour plus d’informations, consultez la section [Activer et désactiver le suivi des modifications](https://msdn.microsoft.com/library/bb964713.aspx) .    

Lorsque vous structurez hello **créer une Source de données** demander, SQL stratégie le suivi intégré peut être spécifié comme suit :

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**Stratégies de détection des suppressions de données**

objectif de Hello d’une stratégie de détection de suppression de données est tooefficiently identifient les éléments de données supprimées. Actuellement, la stratégie de hello uniquement pris en charge est hello `Soft Delete` stratégie, qui permet l’identification des éléments en fonction de la valeur hello supprimés un `soft delete` colonne ou propriété dans la source de données hello. Cette stratégie peut être spécifiée comme suit :

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> Seules les colonnes contenant des valeurs de type chaîne de caractères, entier ou booléennes sont prises en charge. Hello valeur utilisée comme `softDeleteMarkerValue` doit être une chaîne, même si la colonne correspondante de hello contient des entiers ou des valeurs booléennes. Par exemple, si la valeur hello qui apparaît dans votre source de données est 1, utilisez `"1"` comme hello `softDeleteMarkerValue`.    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**Exemples de corps de requête**

Si vous avez l’intention de source de données toouse hello avec un indexeur qui s’exécute sur une planification, cet exemple montre comment modifier les toospecify et la suppression des stratégies de détection : 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

Si vous envisagez uniquement la source de données toouse hello pour une copie ponctuelle des données de hello, les stratégies hello peuvent être omis :

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**Réponse**

Pour une requête réussie : « 201 Créé ». 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>Mise à jour d'une source de données
Vous pouvez mettre à jour une source de données existante à l'aide d'une requête HTTP PUT. Vous spécifiez nom hello de tooupdate de source de données hello sur l’URI de la demande hello :

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Hello `api-version` est requis. version actuelle de Hello est `2015-02-28`. Pour plus d’informations, notamment sur d’autres versions, consultez [Versions d’API Recherche Azure](https://msdn.microsoft.com/library/azure/dn864560.aspx).

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Requête**

Hello syntaxe du corps de demande est hello même que pour [demande de créer une Source de données](#CreateDataSourceRequestSyntax).

Certaines propriétés ne peuvent pas être mises à jour dans une source de données existante. Par exemple, vous ne pouvez pas modifier type hello d’une source de données existante.  

Si vous ne souhaitez pas chaîne de connexion toochange hello pour une source de données existante, vous pouvez spécifier hello littéral `<unchanged>` pour la chaîne de connexion hello. Cela est utile dans les situations où vous devez tooupdate une source de données, mais n’avez pas chaîne de connexion accès pratique toohello puisqu’il s’agit des données de sécurité sensibles.

**Réponse**

Pour une requête réussie : 201 Créé est renvoyé si une source de données a été créée, et 204 Pas de contenu si une source de données existante a été mise à jour.

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>Liste des sources de données
Hello **liste des Sources de données** opération renvoie une liste des sources de données hello dans votre service Azure Search. 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` est requis. version actuelle de Hello est `2015-02-28`. 

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Réponse**

Pour une requête réussie : « 200 OK ».

Voici un exemple de corps de réponse :

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

Notez que vous pouvez filtrer la réponse hello vers le bas les propriétés de hello toojust que vous intéresse. Par exemple, si vous souhaitez uniquement la liste des noms de source de données, utilisez hello OData `$select` option de requête :

    GET /datasources?api-version=205-02-28&$select=name

Dans ce cas, réponse hello hello exemple ci-dessus apparaît comme suit : 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

Il s’agit d’une bande de passante toosave technique utile si vous avez un grand nombre de sources de données dans votre service de recherche.

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>Obtention de source de données
Hello **obtenir la Source de données** opération Obtient la définition de source de données hello à partir d’Azure Search.

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` est requis. version actuelle de Hello est `2015-02-28`. 

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Réponse**

Code d'état : 200 OK est retourné pour une réponse correcte.

réponse de Hello est similaire tooexamples dans [créer une Source de données exemple demandes](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> Ne définissez pas hello `Accept` en-tête de demande trop`application/json;odata.metadata=none` lorsque l’appel de cette API, car cela provoque `@odata.type` toobe attribut omis de la réponse de hello et que vous ne sera pas en mesure de toodifferentiate entre la modification de données et la détection de suppression de données stratégies de types différents. 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>Suppression de sources de données 
Hello **supprimer la Source de données** opération supprime une source de données à partir de votre service Azure Search.

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Si des indexeurs font référence à des sources de données hello que vous supprimez, opération de suppression hello continue. Toutefois, ces indexeurs passeront à un état d'erreur lors de leur prochaine exécution.  
> 
> 

Hello `api-version` est requis. version actuelle de Hello est `2015-02-28`. 

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Réponse**

Code d'état : 204 Pas de contenu est renvoyé en cas de réponse correcte.

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>Création d'indexeur
Vous pouvez créer un indexeur dans un service Azure Search à l'aide d'une requête HTTP POST.

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Vous pouvez également utiliser une requête PUT et spécifiez le nom de source de données hello sur hello URI. Si la source de données hello n’existe pas, il sera créé.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> nombre maximal de Hello d’indexeurs autorisé varie en fonction du niveau de tarification. service gratuit de Hello permet des too3 indexeurs. Le service standard autorise 50 indexeurs. Pour plus d’informations, consultez [Limites de service](search-limits-quotas-capacity.md) .
> 
> 

Hello `api-version` est requis. version actuelle de Hello est `2015-02-28`. 

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

<a name="CreateIndexerRequestSyntax"></a>
**Syntaxe du corps de la requête**

corps de Hello de demande de hello contient une définition d’indexeur, qui spécifie la source de données hello et des index cible de hello pour l’indexation, ainsi que de planification d’indexation facultatif et de paramètres. 

syntaxe Hello pour structurer la charge utile de demande hello est comme suit. Vous trouverez un exemple de requête dans cette rubrique.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**Planification de l'indexeur**

Un indexeur peut éventuellement spécifier une planification. Si une planification est présente, indexeur de hello exécutera périodiquement selon une planification. Planification a hello suivant d’attributs :

* `interval`: requis. Valeur de durée qui spécifie un intervalle ou une période d'exécution pour l'indexeur. Hello plus petite autorisée intervalle est de 5 minutes. Hello plus longue est un jour. Il doit être formaté en tant que valeur « dayTimeDuration » XSD (un sous-ensemble limité d'une valeur de [durée ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) ). modèle Hello pour cela est : `"P[nD][T[nH][nM]]"`. Exemples : `PT15M` toutes les 15 minutes, `PT2H` toutes les deux heures. 
* `startTime`: requis. Une date et heure UTC lors de l’exécution de l’indexeur hello doit commencer. 

**Paramètres d'indexeur**

Un indexeur peut éventuellement spécifier plusieurs paramètres qui affectent son comportement. Tous les paramètres de hello sont facultatifs.  

* `maxFailedItems`: nombre de hello d’éléments qui peuvent échouer toobe indexée avant une exécution de l’indexeur soit considérée comme un échec. La valeur par défaut est 0. Informations sur les éléments ayant échouées sont retournées par hello [obtenir le statut indexeur](#GetIndexerStatus) opération. 
* `maxFailedItemsPerBatch`: nombre de hello d’éléments qui peuvent échouer toobe indexés dans chaque lot avant une exécution de l’indexeur soit considérée comme un échec. La valeur par défaut est 0.
* `base64EncodeKeys`: spécifie si les clés de document doivent être codées en base 64. Azure Search impose des restrictions relatives aux caractères qui peuvent être présents dans une clé de document. Toutefois, les valeurs hello dans votre source de données peuvent contenir des caractères qui ne sont pas valides. S’il est nécessaire tooindex ces valeurs en tant que clés de document, cet indicateur peut être défini tootrue. La valeur par défaut est `false`.
* `batchSize`: Spécifie le nombre hello d’éléments qui sont lues à partir de la source de données hello et indexés comme un lot unique des performances de tooimprove de commande. par défaut de Hello varie selon le type de source de données hello : il s’agit de 1000 pour SQL Azure et base de données Azure Cosmos et 10 pour le stockage d’objets Blob Azure.

**Mappages de champs**

Vous pouvez utiliser les mappages de champ toomap un nom de champ dans hello données source tooa autre nom de champ dans des index cible de hello. Par exemple, considérez une table source avec un champ `_id`. Azure Search n’autorise pas un nom de champ commençant par un trait de soulignement pour le champ de hello doit être renommé. Cela est possible à l’aide de hello `fieldMappings` propriété d’indexeur hello comme suit : 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

Vous pouvez spécifier plusieurs mappages de champs. 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

Les noms de champs sources et cibles sont sensibles à la casse.

<a name="FieldMappingFunctions"></a>
***Fonctions de mappage de champs***

Mappages de champs peuvent également être des valeurs de champ de source de tootransform utilisé à l’aide de *mappage des fonctions*.

Seule une de ces fonctions est actuellement prise en charge : `jsonArrayToStringCollection`. Il analyse un champ qui contient une chaîne mise en forme en tant que tableau JSON dans un champ de la collection (EDM.String) dans des index cible de hello. Elle est conçue pour une utilisation avec l'indexeur SQL Azure en particulier, car SQL ne dispose pas d'un type de données de collection natif. Elle peut être utilisée comme suit : 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

Par exemple, si hello champ source contient la chaîne de hello `["red", "white", "blue"]`, puis le champ cible de hello de type `Collection(Edm.String)` sera rempli avec les valeurs hello trois `"red"`, `"white"` et `"blue"`.

Notez que hello `targetFieldName` propriété est facultative ; si omis, hello `sourceFieldName` valeur est utilisée. 

<a name="CreateIndexerRequestExamples"></a>
**Exemples de corps de requête**

Hello exemple suivant crée un indexeur qui copie les données à partir de la table de hello référencée par hello `ordersds` toohello de source de données `orders` index selon une planification qui commence le 1er janvier 2015 UTC et s’exécute toutes les heures. Chaque appel de l’indexeur est réussi si pas plus de 5 éléments échouent toobe indexé dans chaque lot, et pas plus de 10 éléments échouent toobe au total. 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**Réponse**

Pour une requête réussie : « 201 Créé ».

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>Mise à jour d'un indexeur
Vous pouvez mettre à jour un indexeur existant à l'aide d'une requête HTTP PUT. Vous spécifiez nom hello de hello indexeur tooupdate sur l’URI de la demande hello :

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Hello `api-version` est requis. version actuelle de Hello est `2015-02-28`. 

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Requête**

Hello syntaxe du corps de demande est hello même que pour [créer un indexeur demande](#CreateIndexerRequestSyntax).

**Réponse**

Pour une requête réussie : 201 Créé si un indexeur a été créé, et 204 Pas de contenu si un indexeur existant a été mis à jour.

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>Liste des indexeurs
Hello **liste des indexeurs** opération renvoie la liste hello des indexeurs dans votre service Azure Search. 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


Hello `api-version` est requis. version d’évaluation Hello `2015-02-28-Preview`. [Contrôle de version Azure Search](https://msdn.microsoft.com/library/azure/dn864560.aspx) .

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Réponse**

Pour une requête réussie : « 200 OK ».

Voici un exemple de corps de réponse :

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

Notez que vous pouvez filtrer la réponse hello vers le bas les propriétés de hello toojust que vous intéresse. Par exemple, si vous souhaitez uniquement la liste des noms d’indexeur, utilisez hello OData `$select` option de requête :

    GET /indexers?api-version=2014-10-20-Preview&$select=name

Dans ce cas, réponse hello hello exemple ci-dessus apparaît comme suit : 

    {
      "value" : [ { "name": "myindexer" } ]
    }

Il s’agit d’une bande de passante toosave technique utile si vous avez un grand nombre d’indexeurs dans votre service de recherche.

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>Obtention d'indexeur
Hello **Get Indexer** opération Obtient la définition d’indexeur hello à partir d’Azure Search.

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` est requis. version d’évaluation Hello `2015-02-28-Preview`. 

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Réponse**

Code d'état : 200 OK est retourné pour une réponse correcte.

réponse de Hello est similaire tooexamples dans [indexeur de créer des exemples de demandes](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>Suppression d'indexeur
Hello **supprimer l’indexeur** opération supprime un indexeur de votre service Azure Search.

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Lors de la suppression d’un indexeur, les exécutions d’indexeur hello en cours à ce moment-là exécutera toocompletion, mais aucun autre n’est planifiée. Toouse tentatives qu'un indexeur inexistant génère le code d’état HTTP 404 introuvable. 

Hello `api-version` est requis. version d’évaluation Hello `2015-02-28-Preview`. 

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Réponse**

Code d'état : 204 Pas de contenu est renvoyé en cas de réponse correcte.

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>Exécuter l'indexeur
Dans toorunning Ajout périodiquement selon une planification, un indexeur peut également être appelé à la demande via hello **exécuter l’indexeur** opération : 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` est requis. version d’évaluation Hello `2015-02-28-Preview`. 

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Réponse**

Code d'état : 202 Accepté est retourné en cas de réponse correcte.

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>Get Indexer Status
Hello **obtenir le statut indexeur** opération récupère hello actuel état et l’exécution de l’historique d’un indexeur : 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


Hello `api-version` est requis. version d’évaluation Hello `2015-02-28-Preview`. 

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Réponse**

Code d'état : 200 OK en cas de réponse correcte.

corps de réponse Hello contient des informations sur l’état de santé global indexeur, appel de l’indexeur dernière hello, ainsi que l’historique de hello des appels de l’indexeur récentes (le cas échéant). 

Voici un exemple de corps de réponse : 

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

**État de l'indexeur**

État de l’indexeur peut être une des valeurs suivantes de hello :

* `running`Indique que cet indexeur hello s’exécute normalement. Notez que certaines des exécutions des indexeurs hello peuvent encore échouer, afin qu’il soit un Bonjour de toocheck conseillé `lastResult` propriété également. 
* `error`Indique que cet indexeur hello a rencontré une erreur qui ne peut pas être corrigée sans intervention humaine. Par exemple, les informations d’identification de source de données hello a peut-être expiré, ou schéma hello hello source de données ou des index cible de hello a changé moyen. 

**Résultat d'exécution de l'indexeur**

Un résultat d'exécution de l'indexeur contient des informations sur une seule exécution de l'indexeur. Hello dernier résultat est présenté comme hello `lastResult` propriété d’état de l’indexeur hello. Autres résultats récents, le cas échéant, sont retournés en tant que hello `executionHistory` propriété d’état de l’indexeur hello. 

Résultat de l’exécution d’indexeur contient hello propriétés suivantes : 

* `status`: hello état d’exécution. Pour plus d'informations, consultez [État d'exécution de l'indexeur](#IndexerExecutionStatus) ci-dessous. 
* `errorMessage`: message d'erreur pour un échec d'exécution. 
* `startTime`: hello en heure UTC lorsque cette exécution a commencé.
* `endTime`: hello en heure UTC lorsque cette exécution s’est terminée. Cette valeur n’est pas définie si l’exécution de hello est toujours en cours.
* `errors`: tableau d’éventuelles erreurs au niveau des éléments. Chaque entrée contient une clé de document (`key` propriété) et un message d'erreur (`errorMessage` propriété). 
* `itemsProcessed`: hello le nombre d’éléments de source de données (par exemple, les lignes de table) qui hello indexeur a tenté de tooindex durant cette exécution. 
* `itemsFailed`: hello le nombre d’éléments qui ont échoué pendant cette exécution.  
* `initialTrackingState`: toujours `null` pour la première exécution d’indexeur hello, ou si les données de salutation stratégie de suivi des modifications n’est pas activé sur la source de données hello utilisée. Si une telle stratégie est activée, cette valeur indique hello première (la plus basse) valeur suivi des modifications traitée par cette exécution lors des exécutions suivantes. 
* `finalTrackingState`: toujours `null` si la stratégie de suivi des modifications des données de la hello n’est pas activé sur la source de données hello utilisée. Sinon, indique hello plus récente (le plus élevé) valeur suivi des modifications a été traitée par cette exécution. 

<a name="IndexerExecutionStatus"></a>
**État d’exécution de l’indexeur**

État de l’exécution d’indexeur capture l’état hello d’une seule exécution. Il peut avoir hello valeurs suivantes :

* `success`Indique que l’exécution d’indexeur hello s’est terminée avec succès.
* `inProgress`Indique que l’exécution d’indexeur hello est en cours d’exécution. 
* `transientFailure` indique qu'une exécution de l'indexeur a échoué. Pour plus d'informations, consultez la propriété `errorMessage`. Échec de Hello peut-être exiger ou non une intervention humaine toofix - par exemple, la résolution d’une incompatibilité de schéma entre la source de données hello et des index cible de hello requiert une action de l’utilisateur, n’est pas le cas d’un temps d’arrêt de source de données temporaires. Les appels de l'indexeur continuent conformément à la planification, si celle-ci est définie. 
* `persistentFailure`Indique que cet indexeur hello a échoué d’une manière qui requiert une intervention humaine. Les exécutions planifiées de l'indexeur s'arrêtent. Après avoir corrigé le problème de hello, utilisez les exécutions de réinitialiser les API indexeur toorestart hello planifiée. 
* `reset`Indique que cet indexeur hello a été réinitialisé par un tooReset appel API d’indexeur (voir ci-dessous). 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>Réinitialisation de l'indexeur
Hello **réinitialiser l’indexeur** opération réinitialise hello suivi d’état associé hello indexeur. Cela vous permet de tootrigger à partir de zéro réindexation (par exemple, si votre schéma de source de données a changé) ou la stratégie de détection toochange hello données modifiées pour une source de données associée à hello indexeur.   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` est requis. version d’évaluation Hello `2015-02-28-Preview`. 

Hello `api-key` doit être une clé d’administration (en tant que clé de requête tooa exécutée). Consultez la section de l’authentification toohello de [API REST du Service recherche](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn plus d’informations sur les clés. [Créer un service de recherche dans le portail de hello](search-create-service-portal.md) explique comment les URL du service tooget hello et les propriétés de clé utilisées dans la demande de hello.

**Réponse**

Code d'état : 204 Pas de contenu en cas de réponse correcte.

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>Mappage entre les types de données SQL et les types de données Azure Search
<table style="font-size:12">
<tr>
<td>Type de données SQL</td>    
<td>Types de champs d'index cible autorisés</td>
<td>Remarques</td>
</tr>
<tr>
<td>bit</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>int, smallint, tinyint</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>real, float</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>smallmoney, money<br>décimal<br>numérique
</td>
<td>Edm.String</td>
<td>Azure Search ne prend pas en charge la conversion de types décimaux en Edm.Double, car elle entraîne une perte de précision
</td>
</tr>
<tr>
<td>char, nchar, varchar, nvarchar</td>
<td>Edm.String<br/>Collection(Edm.String)</td>
<td>Consultez [fonctions de mappage de champ](#FieldMappingFunctions) dans ce document pour plus d’informations sur la façon de tootransform une colonne de chaîne dans une collection (EDM.String)</td>
</tr>
<tr>
<td>smalldatetime, datetime, datetime2, date, datetimeoffset</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>Geography</td>
<td>Edm.GeographyPoint</td>
<td>Seules les instances de geography de type POINT avec SRID 4326 (valeur par défaut hello) sont pris en charge.</td>
</tr>
<tr>
<td>rowversion</td>
<td>N/A</td>
<td>Colonnes de la version de ligne ne peut pas être stockés dans l’index de recherche hello, mais elles peuvent être utilisées pour le suivi des modifications</td>
</tr>
<tr>
<td>time, timespan<br>binary, varbinary, image<br>xml, geometry, types CLR</td>
<td>N/A</td>
<td>Non pris en charge</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mappage entre les types de données JSON et les types de données Azure Search
<table style="font-size:12">
<tr>
<td>Type de données JSON</td>    
<td>Types de champs d'index cible autorisés</td>
<td>Remarques</td>
</tr>
<tr>
<td>valeur booléenne</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Nombres entiers</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Nombres à virgule flottante</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>string</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>Tableaux de types primitifs, par exemple [ « a », « b », « c » ]</td>
<td>Collection(Edm.String)</td>
<td></td>
</tr>
<tr>
<td>Chaînes qui ressemblent à des dates</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Objets point GeoJSON</td>
<td>Edm.GeographyPoint</td>
<td>Points GeoJSON sont des objets JSON Bonjour suivant le format : {« type » : « Point », « coordonnées » : [long, lat]} </td>
</tr>
<tr>
<td>Autres objets JSON</td>
<td>N/A</td>
<td>Non pris en charge. Azure Search prend actuellement en charge uniquement les types primitifs et les collections de chaînes de caractères</td>
</tr>
</table>
