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
# <a name="securing-access-tooazure-cosmos-db-data"></a><span data-ttu-id="5314b-103">Sécurisation des données de base de données Cosmos accès tooAzure</span><span class="sxs-lookup"><span data-stu-id="5314b-103">Securing access tooAzure Cosmos DB data</span></span>
<span data-ttu-id="5314b-104">Cet article fournit une vue d’ensemble de la sécurisation de toodata d’accès stocké dans [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="5314b-104">This article provides an overview of securing access toodata stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="5314b-105">Base de données Azure Cosmos utilise deux types d’utilisateurs tooauthenticate de clés et fournissent l’accès tooits données et des ressources.</span><span class="sxs-lookup"><span data-stu-id="5314b-105">Azure Cosmos DB uses two types of keys tooauthenticate users and provide access tooits data and resources.</span></span> 

|<span data-ttu-id="5314b-106">Type de clé</span><span class="sxs-lookup"><span data-stu-id="5314b-106">Key type</span></span>|<span data-ttu-id="5314b-107">Ressources</span><span class="sxs-lookup"><span data-stu-id="5314b-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="5314b-108">Clés principales</span><span class="sxs-lookup"><span data-stu-id="5314b-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="5314b-109">Utilisées pour les ressources d’administration : comptes de base de données, bases de données, utilisateurs et autorisations</span><span class="sxs-lookup"><span data-stu-id="5314b-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="5314b-110">Jetons de ressource</span><span class="sxs-lookup"><span data-stu-id="5314b-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="5314b-111">Utilisés pour les ressources de l’application : collections, documents, pièces jointes, procédures stockées, déclencheurs et fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="5314b-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="5314b-112">Clés principales</span><span class="sxs-lookup"><span data-stu-id="5314b-112">Master keys</span></span> 

<span data-ttu-id="5314b-113">Les clés principales fournissent accès toohello toutes les ressources d’administration hello pour le compte de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="5314b-113">Master keys provide access toohello all hello administrative resources for hello database account.</span></span> <span data-ttu-id="5314b-114">Clés principales :</span><span class="sxs-lookup"><span data-stu-id="5314b-114">Master keys:</span></span>  
- <span data-ttu-id="5314b-115">Fournir l’accès tooaccounts, les bases de données, les utilisateurs et les autorisations.</span><span class="sxs-lookup"><span data-stu-id="5314b-115">Provide access tooaccounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="5314b-116">Ne peut pas être tooprovide utilisé un accès granulaire toocollections et des documents.</span><span class="sxs-lookup"><span data-stu-id="5314b-116">Cannot be used tooprovide granular access toocollections and documents.</span></span>
- <span data-ttu-id="5314b-117">Sont créés lors de la création de hello d’un compte.</span><span class="sxs-lookup"><span data-stu-id="5314b-117">Are created during hello creation of an account.</span></span>
- <span data-ttu-id="5314b-118">Peuvent être régénérées à tout moment.</span><span class="sxs-lookup"><span data-stu-id="5314b-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="5314b-119">Chaque compte comporte deux clés principales : une clé primaire et une clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="5314b-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="5314b-120">Hello clés vise afin que vous pouvez régénérer ou substituer les clés, fournissant des données et le compte d’accès continu tooyour.</span><span class="sxs-lookup"><span data-stu-id="5314b-120">hello purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access tooyour account and data.</span></span> 

<span data-ttu-id="5314b-121">En outre toohello deux des clés principales pour le compte de base de données Cosmos hello, il existe deux clés en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="5314b-121">In addition toohello two master keys for hello Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="5314b-122">Ces clés en lecture seule autoriser uniquement les opérations de lecture sur le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="5314b-122">These read-only keys only allow read operations on hello account.</span></span> <span data-ttu-id="5314b-123">Clés en lecture seule ne fournissent pas d’accès aux ressources d’autorisations tooread.</span><span class="sxs-lookup"><span data-stu-id="5314b-123">Read-only keys do not provide access tooread permissions resources.</span></span>

<span data-ttu-id="5314b-124">Principal, secondaire en lecture seule et en lecture-écriture des clés principales peuvent être récupérées et régénérées à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5314b-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using hello Azure portal.</span></span> <span data-ttu-id="5314b-125">Pour connaître la procédure, consultez [Affichage, copie et régénération des clés d’accès](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="5314b-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Contrôle d’accès (IAM) Bonjour Azure portal - démonstration de sécurité de base de données NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="5314b-127">processus de Hello de rotation de votre clé principale est simple.</span><span class="sxs-lookup"><span data-stu-id="5314b-127">hello process of rotating your master key is simple.</span></span> <span data-ttu-id="5314b-128">Accédez toohello tooretrieve portail Azure votre clé secondaire, remplacez votre clé primaire avec votre clé secondaire dans votre application, puis faire pivoter la clé primaire de hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5314b-128">Navigate toohello Azure portal tooretrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate hello primary key in hello Azure portal.</span></span>

![Permutation des clés principales Bonjour Azure portal - démonstration de sécurité de base de données NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a><span data-ttu-id="5314b-130">Le code exemple toouse une clé principale</span><span class="sxs-lookup"><span data-stu-id="5314b-130">Code sample toouse a master key</span></span>

<span data-ttu-id="5314b-131">Hello exemple de code suivant illustre comment toouse une base de données Cosmos tooinstantiate de point de terminaison et la clé principale du compte un DocumentClient et créer une base de données.</span><span class="sxs-lookup"><span data-stu-id="5314b-131">hello following code sample illustrates how toouse a Cosmos DB account endpoint and master key tooinstantiate a DocumentClient and create a database.</span></span> 

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

## <a name="resource-tokens"></a><span data-ttu-id="5314b-132">Jetons de ressource</span><span class="sxs-lookup"><span data-stu-id="5314b-132">Resource tokens</span></span>

<span data-ttu-id="5314b-133">Jetons de ressource fournissent un accès à des ressources d’application toohello au sein d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="5314b-133">Resource tokens provide access toohello application resources within a database.</span></span> <span data-ttu-id="5314b-134">Jetons de ressource :</span><span class="sxs-lookup"><span data-stu-id="5314b-134">Resource tokens:</span></span>
- <span data-ttu-id="5314b-135">Fournir l’accès toospecific collections, les clés de partition, documents, pièces jointes, procédures stockées, déclencheurs et UDF.</span><span class="sxs-lookup"><span data-stu-id="5314b-135">Provide access toospecific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="5314b-136">Sont créés quand un [utilisateur](#users) est accordé [autorisations](#permissions) tooa des ressources spécifiques.</span><span class="sxs-lookup"><span data-stu-id="5314b-136">Are created when a [user](#users) is granted [permissions](#permissions) tooa specific resource.</span></span>
- <span data-ttu-id="5314b-137">Sont recréés lorsqu’une ressource d’autorisation est exécutée par un appel POST, GET ou PUT.</span><span class="sxs-lookup"><span data-stu-id="5314b-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="5314b-138">Utiliser un jeton de ressource de hachage spécifiquement construit utilisateur de hello, les ressources et les autorisations.</span><span class="sxs-lookup"><span data-stu-id="5314b-138">Use a hash resource token specifically constructed for hello user, resource, and permission.</span></span>
- <span data-ttu-id="5314b-139">Sont liés à une période de validité personnalisable.</span><span class="sxs-lookup"><span data-stu-id="5314b-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="5314b-140">intervalle de temps valide Hello par défaut est d’une heure.</span><span class="sxs-lookup"><span data-stu-id="5314b-140">hello default valid timespan is one hour.</span></span> <span data-ttu-id="5314b-141">Durée de vie de jeton, toutefois, peut-être être spécifiée explicitement, les tooa maximum de cinq heures.</span><span class="sxs-lookup"><span data-stu-id="5314b-141">Token lifetime, however, may be explicitly specified, up tooa maximum of five hours.</span></span>
- <span data-ttu-id="5314b-142">Fournir un toogiving sécurisé autre clé principale de hello.</span><span class="sxs-lookup"><span data-stu-id="5314b-142">Provide a safe alternative toogiving out hello master key.</span></span> 
- <span data-ttu-id="5314b-143">Activer les clients tooread, écriture et suppression des ressources dans le compte de base de données Cosmos hello selon qu’ils ont été attribuées des autorisations toohello.</span><span class="sxs-lookup"><span data-stu-id="5314b-143">Enable clients tooread, write, and delete resources in hello Cosmos DB account according toohello permissions they've been granted.</span></span>

<span data-ttu-id="5314b-144">Vous pouvez utiliser un jeton de ressource (en créant des autorisations et les utilisateurs de base de données Cosmos) lorsque vous souhaitez tooresources d’accès tooprovide dans votre base de données Cosmos compte tooa client qui ne peut pas être fiable avec la clé principale de hello.</span><span class="sxs-lookup"><span data-stu-id="5314b-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want tooprovide access tooresources in your Cosmos DB account tooa client that cannot be trusted with hello master key.</span></span>  

<span data-ttu-id="5314b-145">Les jetons de ressource COSMOS DB fournissent une alternative sécurisée qui permet les clients tooread, écriture et suppression des ressources dans votre compte de base de données Cosmos selon que vous avez accordé des autorisations toohello et sans nécessité d’une forme de base ou en lecture seule clé.</span><span class="sxs-lookup"><span data-stu-id="5314b-145">Cosmos DB resource tokens provide a safe alternative that enables clients tooread, write, and delete resources in your Cosmos DB account according toohello permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="5314b-146">Voici un modèle de conception classique par laquelle les jetons de ressource peuvent être demandés, générés et remis tooclients :</span><span class="sxs-lookup"><span data-stu-id="5314b-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered tooclients:</span></span>

1. <span data-ttu-id="5314b-147">Un service de niveau intermédiaire est configuré tooserve un photos de l’utilisateur tooshare application mobile.</span><span class="sxs-lookup"><span data-stu-id="5314b-147">A mid-tier service is set up tooserve a mobile application tooshare user photos.</span></span> 
2. <span data-ttu-id="5314b-148">service de couche intermédiaire Hello possède la clé principale de hello Hello Cosmos DB compte.</span><span class="sxs-lookup"><span data-stu-id="5314b-148">hello mid-tier service possesses hello master key of hello Cosmos DB account.</span></span>
3. <span data-ttu-id="5314b-149">application de photos Hello est installée sur les périphériques mobiles de l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="5314b-149">hello photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="5314b-150">Sur la connexion, application de photos hello établit identité hello d’utilisateur hello avec le service de couche intermédiaire hello.</span><span class="sxs-lookup"><span data-stu-id="5314b-150">On login, hello photo app establishes hello identity of hello user with hello mid-tier service.</span></span> <span data-ttu-id="5314b-151">Ce mécanisme d’établissement d’identité est purement toohello application.</span><span class="sxs-lookup"><span data-stu-id="5314b-151">This mechanism of identity establishment is purely up toohello application.</span></span>
5. <span data-ttu-id="5314b-152">Une fois que l’identité de hello est établie, les demandes de service de couche intermédiaire hello autorisations selon l’identité de hello.</span><span class="sxs-lookup"><span data-stu-id="5314b-152">Once hello identity is established, hello mid-tier service requests permissions based on hello identity.</span></span>
6. <span data-ttu-id="5314b-153">service de couche intermédiaire Hello envoie une application de téléphone ressource jeton toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="5314b-153">hello mid-tier service sends a resource token back toohello phone app.</span></span>
7. <span data-ttu-id="5314b-154">application de téléphone Hello poursuivre toouse hello toodirectly jeton accès Cosmos DB ressources autorisations hello définies par le jeton de ressource hello et intervalle de salutation autorisée par le jeton de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="5314b-154">hello phone app can continue toouse hello resource token toodirectly access Cosmos DB resources with hello permissions defined by hello resource token and for hello interval allowed by hello resource token.</span></span> 
8. <span data-ttu-id="5314b-155">Expiration du jeton de ressource hello, les demandes suivantes reçoivent une exception non autorisé 401.</span><span class="sxs-lookup"><span data-stu-id="5314b-155">When hello resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="5314b-156">À ce stade, application de téléphone hello rétablit les identités hello et demande un nouveau jeton de ressource.</span><span class="sxs-lookup"><span data-stu-id="5314b-156">At this point, hello phone app re-establishes hello identity and requests a new resource token.</span></span>

    ![Workflow de jetons de ressource Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="5314b-158">Gestion et génération de jetons de ressources sont gérées par hello Cosmos DB bibliothèques native client ; Toutefois, si vous utilisez REST vous devez construire des en-têtes de demande / d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="5314b-158">Resource token generation and management is handled by hello native Cosmos DB client libraries; however, if you use REST you must construct hello request/authentication headers.</span></span> <span data-ttu-id="5314b-159">Pour plus d’informations sur la création d’en-têtes d’authentification pour REST, consultez [contrôle d’accès aux ressources de base de données Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) ou hello [code source pour nos kits de développement logiciel](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="5314b-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or hello [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="5314b-160">Pour obtenir un exemple d’un service de couche intermédiaire toogenerate ou service Broker pour les jetons de ressource, consultez hello [ResourceTokenBroker application](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="5314b-160">For an example of a middle tier service used toogenerate or broker resource tokens, see hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="5314b-161">Utilisateurs</span><span class="sxs-lookup"><span data-stu-id="5314b-161">Users</span></span>
<span data-ttu-id="5314b-162">Les utilisateurs d’Azure Cosmos DB sont associés à une base de données Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5314b-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="5314b-163">Chaque base de données peut contenir zéro, un ou plusieurs utilisateurs Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5314b-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="5314b-164">Hello suivant exemple de code montre comment toocreate une ressource d’utilisateur de base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5314b-164">hello following code sample shows how toocreate a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="5314b-165">Chaque utilisateur de base de données Cosmos a une propriété PermissionsLink qui peut être utilisé tooretrieve la liste hello des [autorisations](#permissions) associé hello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5314b-165">Each Cosmos DB user has a PermissionsLink property that can be used tooretrieve hello list of [permissions](#permissions) associated with hello user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="5314b-166">Autorisations</span><span class="sxs-lookup"><span data-stu-id="5314b-166">Permissions</span></span>
<span data-ttu-id="5314b-167">Une ressource d’autorisation Azure Cosmos DB est associée à un utilisateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5314b-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="5314b-168">Chaque utilisateur peut contenir zéro, une ou plusieurs autorisations Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5314b-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="5314b-169">Une ressource d’autorisation fournit un jeton de sécurité accès tooa hello des besoins de l’utilisateur lors de la tentative de tooaccess une ressource d’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="5314b-169">A permission resource provides access tooa security token that hello user needs when trying tooaccess a specific application resource.</span></span>
<span data-ttu-id="5314b-170">Il existe deux niveaux d’accès disponibles qui peuvent être fournis par une ressource d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="5314b-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="5314b-171">All : utilisateur de hello dispose des autorisations complètes sur la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="5314b-171">All: hello user has full permission on hello resource.</span></span>
* <span data-ttu-id="5314b-172">Lecture : utilisateur de hello peut lire uniquement le contenu hello de ressource de hello, mais ne peut pas effectuer les opérations de suppression sur la ressource de hello, mise à jour ou écriture.</span><span class="sxs-lookup"><span data-stu-id="5314b-172">Read: hello user can only read hello contents of hello resource but cannot perform write, update, or delete operations on hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="5314b-173">Dans l’ordre toorun Cosmos DB des procédures stockées hello utilisateur doit disposer hello toutes les autorisations sur la collection hello dans le hello procédure stockée sera exécutée.</span><span class="sxs-lookup"><span data-stu-id="5314b-173">In order toorun Cosmos DB stored procedures hello user must have hello All permission on hello collection in which hello stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-toocreate-permission"></a><span data-ttu-id="5314b-174">Autorisation du code exemple toocreate</span><span class="sxs-lookup"><span data-stu-id="5314b-174">Code sample toocreate permission</span></span>

<span data-ttu-id="5314b-175">Hello exemple de code suivant montre comment toocreate une ressource d’autorisation de lecture hello du jeton de ressource de la ressource d’autorisation hello et associer les autorisations hello hello [utilisateur](#users) créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="5314b-175">hello following code sample shows how toocreate a permission resource, read hello resource token of hello permission resource, and associate hello permissions with hello [user](#users) created above.</span></span>

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

<span data-ttu-id="5314b-176">Si vous avez spécifié qu'une clé de partition pour votre collection, puis autorisation hello pour les ressources de collection, des documents et des pièces jointes doit également inclure hello ResourcePartitionKey dans Ajout toohello ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="5314b-176">If you have specified a partition key for your collection, then hello permission for collection, document, and attachment resources must also include hello ResourcePartitionKey in addition toohello ResourceLink.</span></span>

### <a name="code-sample-tooread-permissions-for-user"></a><span data-ttu-id="5314b-177">Autorisations de tooread exemple de code pour l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="5314b-177">Code sample tooread permissions for user</span></span>

<span data-ttu-id="5314b-178">tooeasily obtenir toutes les ressources d’autorisation associées à un utilisateur particulier, Cosmos DB met à disposition une autorisation de flux pour chaque objet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5314b-178">tooeasily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="5314b-179">Hello extrait de code suivant montre comment construire une liste d’autorisation autorisation de hello tooretrieve associée utilisateur hello créé ci-dessus, et instancier une nouvelle DocumentClient pour le compte d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="5314b-179">hello following code snippet shows how tooretrieve hello permission associated with hello user created above, construct a permission list, and instantiate a new DocumentClient on behalf of hello user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5314b-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5314b-180">Next steps</span></span>
* <span data-ttu-id="5314b-181">toolearn en savoir plus sur la sécurité de base de données de base de données Cosmos, consultez [Cosmos DB : sécurité de base de données](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="5314b-181">toolearn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="5314b-182">toolearn sur la gestion des clés principales et en lecture seule, consultez [comment toomanage un compte de base de données Azure Cosmos](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="5314b-182">toolearn about managing master and read-only keys, see [How toomanage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="5314b-183">toolearn jetons d’autorisation de base de données Azure Cosmos tooconstruct, voir [contrôle d’accès aux ressources de base de données Azure Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="5314b-183">toolearn how tooconstruct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
