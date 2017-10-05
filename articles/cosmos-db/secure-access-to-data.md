---
title: "Sécurisation de l’accès aux données Azure Cosmos DB | Microsoft Docs"
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
ms.openlocfilehash: 383e04f91eec2f465b381ce30f2d6d24c488b731
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="securing-access-to-azure-cosmos-db-data"></a><span data-ttu-id="8ec6f-103">Sécurisation de l’accès aux données d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8ec6f-103">Securing access to Azure Cosmos DB data</span></span>
<span data-ttu-id="8ec6f-104">Cet article fournit une vue d’ensemble de la sécurisation de l’accès aux données stockées dans [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="8ec6f-104">This article provides an overview of securing access to data stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="8ec6f-105">Azure Cosmos DB utilise deux types de clés pour authentifier les utilisateurs et permettre d’accéder à ses données et à ses ressources.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-105">Azure Cosmos DB uses two types of keys to authenticate users and provide access to its data and resources.</span></span> 

|<span data-ttu-id="8ec6f-106">Type de clé</span><span class="sxs-lookup"><span data-stu-id="8ec6f-106">Key type</span></span>|<span data-ttu-id="8ec6f-107">Ressources</span><span class="sxs-lookup"><span data-stu-id="8ec6f-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="8ec6f-108">Clés principales</span><span class="sxs-lookup"><span data-stu-id="8ec6f-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="8ec6f-109">Utilisées pour les ressources d’administration : comptes de base de données, bases de données, utilisateurs et autorisations</span><span class="sxs-lookup"><span data-stu-id="8ec6f-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="8ec6f-110">Jetons de ressource</span><span class="sxs-lookup"><span data-stu-id="8ec6f-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="8ec6f-111">Utilisés pour les ressources de l’application : collections, documents, pièces jointes, procédures stockées, déclencheurs et fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="8ec6f-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="8ec6f-112">Clés principales</span><span class="sxs-lookup"><span data-stu-id="8ec6f-112">Master keys</span></span> 

<span data-ttu-id="8ec6f-113">Les clés principales fournissent un accès à toutes les ressources d’administration du compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-113">Master keys provide access to the all the administrative resources for the database account.</span></span> <span data-ttu-id="8ec6f-114">Clés principales :</span><span class="sxs-lookup"><span data-stu-id="8ec6f-114">Master keys:</span></span>  
- <span data-ttu-id="8ec6f-115">Fournissent un accès aux comptes, aux bases de données, aux utilisateurs et aux autorisations.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-115">Provide access to accounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="8ec6f-116">Ne peuvent pas être utilisées pour fournir un accès précis aux collections et aux documents.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-116">Cannot be used to provide granular access to collections and documents.</span></span>
- <span data-ttu-id="8ec6f-117">Sont créées lors de la création d’un compte.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-117">Are created during the creation of an account.</span></span>
- <span data-ttu-id="8ec6f-118">Peuvent être régénérées à tout moment.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="8ec6f-119">Chaque compte comporte deux clés principales : une clé primaire et une clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="8ec6f-120">L’objectif de ces paires de clés est de pouvoir régénérer ou restaurer des clés tout en fournissant un accès permanent à votre compte et à vos données.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span></span> 

<span data-ttu-id="8ec6f-121">Outre les deux clés principales du compte Azure Cosmos DB, il existe deux clés en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-121">In addition to the two master keys for the Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="8ec6f-122">Ces clés en lecture seule autorisent uniquement les opérations de lecture sur le compte.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-122">These read-only keys only allow read operations on the account.</span></span> <span data-ttu-id="8ec6f-123">Les clés en lecture seule ne permettent pas de lire les ressources d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-123">Read-only keys do not provide access to read permissions resources.</span></span>

<span data-ttu-id="8ec6f-124">Les clés principales primaire, secondaire, en lecture seule et en lecture-écriture peuvent être récupérées et régénérées à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span></span> <span data-ttu-id="8ec6f-125">Pour connaître la procédure, consultez [Affichage, copie et régénération des clés d’accès](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="8ec6f-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Contrôle d’accès (IAM) dans le portail Azure - Démonstration de la sécurité de la base de données NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="8ec6f-127">Le processus de rotation de votre clé principale est simple.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-127">The process of rotating your master key is simple.</span></span> <span data-ttu-id="8ec6f-128">Accédez au portail Azure pour récupérer votre clé secondaire, puis remplacez votre clé primaire par votre clé secondaire dans votre application. Enfin, faites pivoter la clé primaire dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span></span>

![Rotation de clé principale dans le portail Azure - Démonstration de la sécurité de la base de données NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-to-use-a-master-key"></a><span data-ttu-id="8ec6f-130">Exemple de code pour utiliser une clé principale</span><span class="sxs-lookup"><span data-stu-id="8ec6f-130">Code sample to use a master key</span></span>

<span data-ttu-id="8ec6f-131">L’exemple de code suivant montre comment utiliser une clé principale et un point de terminaison de compte Azure Cosmos DB pour instancier un DocumentClient et créer une base de données.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-131">The following code sample illustrates how to use a Cosmos DB account endpoint and master key to instantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read the Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from the Azure portal on the Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access to your DocDB account.

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

## <a name="resource-tokens"></a><span data-ttu-id="8ec6f-132">Jetons de ressource</span><span class="sxs-lookup"><span data-stu-id="8ec6f-132">Resource tokens</span></span>

<span data-ttu-id="8ec6f-133">Les jetons de ressource fournissent un accès aux ressources d’application au sein d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-133">Resource tokens provide access to the application resources within a database.</span></span> <span data-ttu-id="8ec6f-134">Jetons de ressource :</span><span class="sxs-lookup"><span data-stu-id="8ec6f-134">Resource tokens:</span></span>
- <span data-ttu-id="8ec6f-135">Fournissent un accès à des collections, clés de partition, documents, pièces jointes, procédures stockées, déclencheurs et fonctions définies par l’utilisateur spécifiques.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-135">Provide access to specific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="8ec6f-136">Sont créés lorsqu’un [utilisateur](#users) dispose des [autorisations](#permissions) sur une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span></span>
- <span data-ttu-id="8ec6f-137">Sont recréés lorsqu’une ressource d’autorisation est exécutée par un appel POST, GET ou PUT.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="8ec6f-138">Utilisent un jeton de ressource de hachage créé spécifiquement pour l’utilisateur, la ressource et les autorisations.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span></span>
- <span data-ttu-id="8ec6f-139">Sont liés à une période de validité personnalisable.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="8ec6f-140">La durée de validité par défaut est d’une heure.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-140">The default valid timespan is one hour.</span></span> <span data-ttu-id="8ec6f-141">La durée de vie du jeton peut cependant être définie de manière explicite (cinq heures maximum).</span><span class="sxs-lookup"><span data-stu-id="8ec6f-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span></span>
- <span data-ttu-id="8ec6f-142">Offrent une alternative sûre pour céder la clé principale.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-142">Provide a safe alternative to giving out the master key.</span></span> 
- <span data-ttu-id="8ec6f-143">Permettent aux clients de lire, d’écrire et de supprimer des ressources dans le compte Azure Cosmos DB en fonction des autorisations qui leur ont été accordées.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-143">Enable clients to read, write, and delete resources in the Cosmos DB account according to the permissions they've been granted.</span></span>

<span data-ttu-id="8ec6f-144">Vous pouvez utiliser un jeton de ressource (en créant des utilisateurs et des autorisations Azure Cosmos DB) lorsque vous voulez fournir un accès aux ressources dans votre compte Azure Cosmos DB à un client qui ne peut pas être approuvé avec la clé principale.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want to provide access to resources in your Cosmos DB account to a client that cannot be trusted with the master key.</span></span>  

<span data-ttu-id="8ec6f-145">Les jetons de ressource Azure Cosmos DB offrent une alternative sûre qui permet aux clients de lire, d’écrire et de supprimer des ressources dans votre compte Azure Cosmos DB en fonction des autorisations que vous avez octroyées, sans avoir besoin d’une clé principale ou en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-145">Cosmos DB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your Cosmos DB account according to the permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="8ec6f-146">Voici un modèle de conception standard dans le cadre duquel des jetons de ressource peuvent être demandés, générés et fournis aux clients :</span><span class="sxs-lookup"><span data-stu-id="8ec6f-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span></span>

1. <span data-ttu-id="8ec6f-147">Un service de niveau intermédiaire est configuré pour servir une application mobile pour partager les photos de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-147">A mid-tier service is set up to serve a mobile application to share user photos.</span></span> 
2. <span data-ttu-id="8ec6f-148">Le service de niveau intermédiaire détient la clé principale du compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-148">The mid-tier service possesses the master key of the Cosmos DB account.</span></span>
3. <span data-ttu-id="8ec6f-149">L’application photo est installée sur les appareils mobiles des utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-149">The photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="8ec6f-150">Lors de la connexion, l'application photo établit l'identité de l'utilisateur avec le service de niveau intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span></span> <span data-ttu-id="8ec6f-151">Ce mécanisme d'identification dépend totalement de l'application.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-151">This mechanism of identity establishment is purely up to the application.</span></span>
5. <span data-ttu-id="8ec6f-152">Une fois l'identité établie, le service de niveau intermédiaire demande des autorisations en fonction de l'identité.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span></span>
6. <span data-ttu-id="8ec6f-153">Le service de niveau intermédiaire renvoie un jeton de ressource à l'application du téléphone.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-153">The mid-tier service sends a resource token back to the phone app.</span></span>
7. <span data-ttu-id="8ec6f-154">Cette dernière peut continuer à utiliser le jeton de ressource pour accéder directement aux ressources Azure Cosmos DB avec les autorisations définies et pendant l’intervalle autorisé.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-154">The phone app can continue to use the resource token to directly access Cosmos DB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span></span> 
8. <span data-ttu-id="8ec6f-155">À expiration du jeton de ressource, les demandes suivantes reçoivent une exception non autorisée 401.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="8ec6f-156">L'application du téléphone établit alors de nouveau l'identité de l'utilisateur et demande un nouveau jeton de ressource.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span></span>

    ![Workflow de jetons de ressource Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="8ec6f-158">La gestion et la génération des jetons de ressource sont prises en charge par les bibliothèques clientes natives Azure Cosmos DB. Toutefois, si vous utilisez REST, vous devez créer les en-têtes de demande/d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-158">Resource token generation and management is handled by the native Cosmos DB client libraries; however, if you use REST you must construct the request/authentication headers.</span></span> <span data-ttu-id="8ec6f-159">Pour plus d’informations sur la création d’en-têtes d’authentification pour REST, consultez [Access Control on DocumentDB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) (Contrôle d’accès aux ressources Azure Cosmos DB) ou le [code source de nos Kits de développement logiciel (SDK)](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="8ec6f-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="8ec6f-160">Pour obtenir un exemple de service de niveau intermédiaire utilisé pour générer ou répartir les jetons de ressource, consultez [l’application ResourceTokenBroker](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="8ec6f-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="8ec6f-161">Utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8ec6f-161">Users</span></span>
<span data-ttu-id="8ec6f-162">Les utilisateurs d’Azure Cosmos DB sont associés à une base de données Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="8ec6f-163">Chaque base de données peut contenir zéro, un ou plusieurs utilisateurs Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="8ec6f-164">L’exemple de code suivant indique comment créer une ressource utilisateur DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-164">The following code sample shows how to create a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="8ec6f-165">Chaque utilisateur Azure Cosmos DB dispose d’une propriété PermissionsLink qui permet de récupérer la liste des [autorisations](#permissions) qui lui sont associées.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-165">Each Cosmos DB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="8ec6f-166">Autorisations</span><span class="sxs-lookup"><span data-stu-id="8ec6f-166">Permissions</span></span>
<span data-ttu-id="8ec6f-167">Une ressource d’autorisation Azure Cosmos DB est associée à un utilisateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="8ec6f-168">Chaque utilisateur peut contenir zéro, une ou plusieurs autorisations Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="8ec6f-169">Une ressource d'autorisation donne accès à un jeton de sécurité dont l'utilisateur a besoin lorsqu'il tente d'accéder à une ressource d'application spécifique.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span></span>
<span data-ttu-id="8ec6f-170">Il existe deux niveaux d’accès disponibles qui peuvent être fournis par une ressource d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="8ec6f-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="8ec6f-171">Tout : L’utilisateur dispose de toutes les autorisations sur la ressource.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-171">All: The user has full permission on the resource.</span></span>
* <span data-ttu-id="8ec6f-172">Lecture : L’utilisateur peut uniquement lire le contenu de la ressource, mais il ne peut pas procéder à des opérations d’écriture, de mise à jour ou de suppression au niveau de la ressource.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="8ec6f-173">Pour exécuter les procédures stockées Azure Cosmos DB, l’utilisateur doit disposer de toutes les autorisations sur la collection dans laquelle la procédure stockée sera exécutée.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-173">In order to run Cosmos DB stored procedures the user must have the All permission on the collection in which the stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-to-create-permission"></a><span data-ttu-id="8ec6f-174">Exemple de code pour créer une autorisation</span><span class="sxs-lookup"><span data-stu-id="8ec6f-174">Code sample to create permission</span></span>

<span data-ttu-id="8ec6f-175">L’exemple de code suivant indique comment créer une ressource d’autorisation, lire le jeton de ressource de la ressource d’autorisation et associer les autorisations à [l’utilisateur](#users) créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span></span>

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

<span data-ttu-id="8ec6f-176">Si vous avez spécifié une clé de partition pour votre collection, l’autorisation pour les ressources de collection, de document et de pièce jointe doit inclure l’élément ResourcePartitionKey en plus de l’élément ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span></span>

### <a name="code-sample-to-read-permissions-for-user"></a><span data-ttu-id="8ec6f-177">Exemple de code pour les autorisations de lecture de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="8ec6f-177">Code sample to read permissions for user</span></span>

<span data-ttu-id="8ec6f-178">Pour obtenir facilement toutes les ressources d’autorisation associées à un utilisateur, Azure Cosmos DB met à disposition un flux d’autorisations pour chaque objet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-178">To easily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="8ec6f-179">L'extrait de code suivant indique comment récupérer l'autorisation associée à l'utilisateur créé ci-dessus, créer une liste d'autorisations et instancier un nouveau DocumentClient pour l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8ec6f-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8ec6f-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ec6f-180">Next steps</span></span>
* <span data-ttu-id="8ec6f-181">Pour en savoir plus sur la sécurité de la base de données Azure Cosmos DB, consultez [Sécurité de la base de données Azure Cosmos DB](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="8ec6f-181">To learn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="8ec6f-182">Pour en savoir plus sur la gestion des clés principales et en lecture seule, consultez [Gestion d’un compte Azure Cosmos DB](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="8ec6f-182">To learn about managing master and read-only keys, see [How to manage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="8ec6f-183">Pour savoir comment créer des jetons d’autorisation Azure Cosmos DB, consultez [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) (Contrôle d’accès aux ressources Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="8ec6f-183">To learn how to construct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
