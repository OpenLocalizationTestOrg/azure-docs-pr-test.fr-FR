---
title: "aaaLearn comment toosecure aux toodata dans la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez les concepts du contrôle d’accès dans Azure Cosmos DB, notamment les clés principales, les clés en lecture seule, les utilisateurs et les autorisations."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a>Sécurisation des données de base de données Cosmos accès tooAzure
Cet article fournit une vue d’ensemble de la sécurisation de toodata d’accès stocké dans [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).

Base de données Azure Cosmos utilise deux types d’utilisateurs tooauthenticate de clés et fournissent l’accès tooits données et des ressources. 

|Type de clé|Ressources|
|---|---|
|[Clés principales](#master-keys) |Utilisées pour les ressources d’administration : comptes de base de données, bases de données, utilisateurs et autorisations|
|[Jetons de ressource](#resource-tokens)|Utilisés pour les ressources de l’application : collections, documents, pièces jointes, procédures stockées, déclencheurs et fonctions définies par l’utilisateur|

<a id="master-keys"></a>

## <a name="master-keys"></a>Clés principales 

Les clés principales fournissent accès toohello toutes les ressources d’administration hello pour le compte de base de données hello. Clés principales :  
- Fournir l’accès tooaccounts, les bases de données, les utilisateurs et les autorisations. 
- Ne peut pas être tooprovide utilisé un accès granulaire toocollections et des documents.
- Sont créés lors de la création de hello d’un compte.
- Peuvent être régénérées à tout moment.

Chaque compte comporte deux clés principales : une clé primaire et une clé secondaire. Hello clés vise afin que vous pouvez régénérer ou substituer les clés, fournissant des données et le compte d’accès continu tooyour. 

En outre toohello deux des clés principales pour le compte de base de données Cosmos hello, il existe deux clés en lecture seule. Ces clés en lecture seule autoriser uniquement les opérations de lecture sur le compte de hello. Clés en lecture seule ne fournissent pas d’accès aux ressources d’autorisations tooread.

Principal, secondaire en lecture seule et en lecture-écriture des clés principales peuvent être récupérées et régénérées à l’aide de hello portail Azure. Pour connaître la procédure, consultez [Affichage, copie et régénération des clés d’accès](manage-account.md#keys).

![Contrôle d’accès (IAM) Bonjour Azure portal - démonstration de sécurité de base de données NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

processus de Hello de rotation de votre clé principale est simple. Accédez toohello tooretrieve portail Azure votre clé secondaire, remplacez votre clé primaire avec votre clé secondaire dans votre application, puis faire pivoter la clé primaire de hello Bonjour portail Azure.

![Permutation des clés principales Bonjour Azure portal - démonstration de sécurité de base de données NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a>Le code exemple toouse une clé principale

Hello exemple de code suivant illustre comment toouse une base de données Cosmos tooinstantiate de point de terminaison et la clé principale du compte un DocumentClient et créer une base de données. 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a>Jetons de ressource

Jetons de ressource fournissent un accès à des ressources d’application toohello au sein d’une base de données. Jetons de ressource :
- Fournir l’accès toospecific collections, les clés de partition, documents, pièces jointes, procédures stockées, déclencheurs et UDF.
- Sont créés quand un [utilisateur](#users) est accordé [autorisations](#permissions) tooa des ressources spécifiques.
- Sont recréés lorsqu’une ressource d’autorisation est exécutée par un appel POST, GET ou PUT.
- Utiliser un jeton de ressource de hachage spécifiquement construit utilisateur de hello, les ressources et les autorisations.
- Sont liés à une période de validité personnalisable. intervalle de temps valide Hello par défaut est d’une heure. Durée de vie de jeton, toutefois, peut-être être spécifiée explicitement, les tooa maximum de cinq heures.
- Fournir un toogiving sécurisé autre clé principale de hello. 
- Activer les clients tooread, écriture et suppression des ressources dans le compte de base de données Cosmos hello selon qu’ils ont été attribuées des autorisations toohello.

Vous pouvez utiliser un jeton de ressource (en créant des autorisations et les utilisateurs de base de données Cosmos) lorsque vous souhaitez tooresources d’accès tooprovide dans votre base de données Cosmos compte tooa client qui ne peut pas être fiable avec la clé principale de hello.  

Les jetons de ressource COSMOS DB fournissent une alternative sécurisée qui permet les clients tooread, écriture et suppression des ressources dans votre compte de base de données Cosmos selon que vous avez accordé des autorisations toohello et sans nécessité d’une forme de base ou en lecture seule clé.

Voici un modèle de conception classique par laquelle les jetons de ressource peuvent être demandés, générés et remis tooclients :

1. Un service de niveau intermédiaire est configuré tooserve un photos de l’utilisateur tooshare application mobile. 
2. service de couche intermédiaire Hello possède la clé principale de hello Hello Cosmos DB compte.
3. application de photos Hello est installée sur les périphériques mobiles de l’utilisateur final. 
4. Sur la connexion, application de photos hello établit identité hello d’utilisateur hello avec le service de couche intermédiaire hello. Ce mécanisme d’établissement d’identité est purement toohello application.
5. Une fois que l’identité de hello est établie, les demandes de service de couche intermédiaire hello autorisations selon l’identité de hello.
6. service de couche intermédiaire Hello envoie une application de téléphone ressource jeton toohello précédent.
7. application de téléphone Hello poursuivre toouse hello toodirectly jeton accès Cosmos DB ressources autorisations hello définies par le jeton de ressource hello et intervalle de salutation autorisée par le jeton de ressource hello. 
8. Expiration du jeton de ressource hello, les demandes suivantes reçoivent une exception non autorisé 401.  À ce stade, application de téléphone hello rétablit les identités hello et demande un nouveau jeton de ressource.

    ![Workflow de jetons de ressource Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

Gestion et génération de jetons de ressources sont gérées par hello Cosmos DB bibliothèques native client ; Toutefois, si vous utilisez REST vous devez construire des en-têtes de demande / d’authentification hello. Pour plus d’informations sur la création d’en-têtes d’authentification pour REST, consultez [contrôle d’accès aux ressources de base de données Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) ou hello [code source pour nos kits de développement logiciel](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).

Pour obtenir un exemple d’un service de couche intermédiaire toogenerate ou service Broker pour les jetons de ressource, consultez hello [ResourceTokenBroker application](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).

<a id="users"></a>

## <a name="users"></a>Utilisateurs
Les utilisateurs d’Azure Cosmos DB sont associés à une base de données Cosmos DB.  Chaque base de données peut contenir zéro, un ou plusieurs utilisateurs Azure Cosmos DB.  Hello suivant exemple de code montre comment toocreate une ressource d’utilisateur de base de données Cosmos.

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> Chaque utilisateur de base de données Cosmos a une propriété PermissionsLink qui peut être utilisé tooretrieve la liste hello des [autorisations](#permissions) associé hello utilisateur.
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a>Autorisations
Une ressource d’autorisation Azure Cosmos DB est associée à un utilisateur Azure Cosmos DB.  Chaque utilisateur peut contenir zéro, une ou plusieurs autorisations Azure Cosmos DB.  Une ressource d’autorisation fournit un jeton de sécurité accès tooa hello des besoins de l’utilisateur lors de la tentative de tooaccess une ressource d’application spécifique.
Il existe deux niveaux d’accès disponibles qui peuvent être fournis par une ressource d’autorisation :

* All : utilisateur de hello dispose des autorisations complètes sur la ressource de hello.
* Lecture : utilisateur de hello peut lire uniquement le contenu hello de ressource de hello, mais ne peut pas effectuer les opérations de suppression sur la ressource de hello, mise à jour ou écriture.

> [!NOTE]
> Dans l’ordre toorun Cosmos DB des procédures stockées hello utilisateur doit disposer hello toutes les autorisations sur la collection hello dans le hello procédure stockée sera exécutée.
> 
> 

### <a name="code-sample-toocreate-permission"></a>Autorisation du code exemple toocreate

Hello exemple de code suivant montre comment toocreate une ressource d’autorisation de lecture hello du jeton de ressource de la ressource d’autorisation hello et associer les autorisations hello hello [utilisateur](#users) créé ci-dessus.

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

Si vous avez spécifié qu'une clé de partition pour votre collection, puis autorisation hello pour les ressources de collection, des documents et des pièces jointes doit également inclure hello ResourcePartitionKey dans Ajout toohello ResourceLink.

### <a name="code-sample-tooread-permissions-for-user"></a>Autorisations de tooread exemple de code pour l’utilisateur

tooeasily obtenir toutes les ressources d’autorisation associées à un utilisateur particulier, Cosmos DB met à disposition une autorisation de flux pour chaque objet utilisateur.  Hello extrait de code suivant montre comment construire une liste d’autorisation autorisation de hello tooretrieve associée utilisateur hello créé ci-dessus, et instancier une nouvelle DocumentClient pour le compte d’utilisateur de hello.

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur la sécurité de base de données de base de données Cosmos, consultez [Cosmos DB : sécurité de base de données](database-security.md).
* toolearn sur la gestion des clés principales et en lecture seule, consultez [comment toomanage un compte de base de données Azure Cosmos](manage-account.md#keys).
* toolearn jetons d’autorisation de base de données Azure Cosmos tooconstruct, voir [contrôle d’accès aux ressources de base de données Azure Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).
