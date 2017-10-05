---
title: "Didacticiel de distribution mondiale d’Azure Cosmos DB pour l’API DocumentDB | Microsoft Docs"
description: "Découvrez comment configurer la distribution mondiale d’Azure Cosmos DB à l’aide de l’API DocumentDB."
services: cosmos-db
keywords: distribution mondiale, documentdb
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: f4d8efe9814bd28bb902567a23b541bc9b5414a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-documentdb-api"></a><span data-ttu-id="7fbaa-104">Configuration de la distribution mondiale d’Azure Cosmos DB à l’aide de l’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7fbaa-104">How to setup Azure Cosmos DB global distribution using the DocumentDB API</span></span>

<span data-ttu-id="7fbaa-105">Dans cet article, nous expliquons comment utiliser le portail Azure pour configurer la distribution globale d’Azure Cosmos DB, puis établir une connexion à l’aide de l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the DocumentDB API.</span></span>

<span data-ttu-id="7fbaa-106">Cet article décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7fbaa-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="7fbaa-107">Configurer la distribution mondiale à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="7fbaa-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="7fbaa-108">Configurer la distribution mondiale à l’aide de l’[API DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="7fbaa-108">Configure global distribution using the [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-documentdb-api"></a><span data-ttu-id="7fbaa-109">Connexion à une région de prédilection avec l’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7fbaa-109">Connecting to a preferred region using the DocumentDB API</span></span>

<span data-ttu-id="7fbaa-110">Pour tirer parti de la [distribution mondiale](distribute-data-globally.md), les applications clientes peuvent spécifier la liste ordonnée de préférences de régions à utiliser pour effectuer des opérations sur les documents.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="7fbaa-111">Pour cela, vous devez configurer la stratégie de connexion.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="7fbaa-112">Selon la configuration du compte Azure Cosmos DB, la disponibilité régionale actuelle et la liste de préférences spécifiée, le Kit de développement logiciel (SDK) DocumentDB choisit le point de terminaison optimal pour les opérations de lecture et d’écriture.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the DocumentDB SDK to perform write and read operations.</span></span>

<span data-ttu-id="7fbaa-113">Cette liste de préférences est spécifiée lors de l’initialisation d’une connexion à l’aide des SDK DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-113">This preference list is specified when initializing a connection using the DocumentDB SDKs.</span></span> <span data-ttu-id="7fbaa-114">Les SDK acceptent un paramètre facultatif « PreferredLocations » qui est une liste ordonnée des régions Azure.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="7fbaa-115">Le SDK envoie automatiquement toutes les écritures vers la région d’écriture en cours.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="7fbaa-116">Toutes les lectures sont envoyées vers la première région disponible dans la liste PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="7fbaa-117">Si la demande échoue, le client passe à la région suivante dans la liste et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="7fbaa-118">Les SDK tentent des opérations de lecture uniquement à partir des régions spécifiées dans PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="7fbaa-119">Ainsi, par exemple, si le compte de base de données est disponible dans trois régions, mais que le client spécifie uniquement deux des régions sans écriture de PreferredLocations, aucune lecture n’est traitée hors de la région d’écriture, même en cas de basculement.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="7fbaa-120">L’application peut vérifier le point de terminaison d’écriture et le point de terminaison de lecture actuels choisis par le SDK en vérifiant deux propriétés, WriteEndpoint et ReadEndpoint, disponibles dans le SDK version 1.8 et ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-120">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="7fbaa-121">Si la propriété PreferredLocations n’est pas définie, toutes les demandes seront traitées par la zone d’écriture en cours.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-121">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="7fbaa-122">Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="7fbaa-122">.NET SDK</span></span>
<span data-ttu-id="7fbaa-123">Le SDK peut être utilisé sans aucune modification du code.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-123">The SDK can be used without any code changes.</span></span> <span data-ttu-id="7fbaa-124">Dans ce cas, le SDK dirige automatiquement les lectures et les écritures vers la région d’écriture en cours.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-124">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="7fbaa-125">Dans la version 1.8 et ultérieure du SDK .NET, le paramètre ConnectionPolicy du constructeur DocumentClient comporte une propriété appelée Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-125">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="7fbaa-126">Cette propriété est de type Collection `<string>` et doit contenir une liste des noms de région.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="7fbaa-127">Les valeurs de chaîne sont mises en forme par la colonne Nom de la région, sur la page [Régions Azure][regions], sans espaces avant ou après le premier et le dernier caractère, respectivement.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-127">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="7fbaa-128">Les points de terminaison d’écriture et de lecture en cours sont disponibles dans DocumentClient.WriteEndpoint et DocumentClient.ReadEndpoint, respectivement.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-128">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="7fbaa-129">Les URL des points de terminaison ne doivent pas être considérées comme des constantes à long terme.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-129">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="7fbaa-130">Le service peut les mettre à jour à tout moment.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-130">The service may update these at any point.</span></span> <span data-ttu-id="7fbaa-131">Le SDK gère ce changement automatiquement.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-131">The SDK handles this change automatically.</span></span>
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="7fbaa-132">SDK Node.js, JavaScript et Python</span><span class="sxs-lookup"><span data-stu-id="7fbaa-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="7fbaa-133">Le SDK peut être utilisé sans aucune modification du code.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-133">The SDK can be used without any code changes.</span></span> <span data-ttu-id="7fbaa-134">Dans ce cas, le SDK dirige automatiquement les lectures et les écritures vers la région d’écriture en cours.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-134">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="7fbaa-135">Dans la version 1.8 et ultérieure de chaque SDK, le paramètre ConnectionPolicy du constructeur DocumentClient comporte une nouvelle propriété appelée DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-135">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="7fbaa-136">Ce paramètre est un tableau de chaînes qui prend une liste de noms de régions.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="7fbaa-137">Les noms sont mis en forme en fonction de la colonne Nom de la région, sur la page [Régions Azure][regions].</span><span class="sxs-lookup"><span data-stu-id="7fbaa-137">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="7fbaa-138">Vous pouvez également utiliser des constantes prédéfinies dans l’objet de commodité AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="7fbaa-138">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="7fbaa-139">Les points de terminaison d’écriture et de lecture en cours sont disponibles dans DocumentClient.getWriteEndpoint et DocumentClient.getReadEndpoint, respectivement.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-139">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="7fbaa-140">Les URL des points de terminaison ne doivent pas être considérées comme des constantes à long terme.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-140">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="7fbaa-141">Le service peut les mettre à jour à tout moment.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-141">The service may update these at any point.</span></span> <span data-ttu-id="7fbaa-142">Le SDK gère ce changement automatiquement.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-142">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="7fbaa-143">Voici un exemple de code pour NodeJS/Javascript.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="7fbaa-144">Python et Java suivent le même modèle.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-144">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="7fbaa-145">REST</span><span class="sxs-lookup"><span data-stu-id="7fbaa-145">REST</span></span>
<span data-ttu-id="7fbaa-146">Une fois qu’un compte de base de données est mis à disposition dans plusieurs régions, les clients peuvent interroger sa disponibilité en exécutant une requête GET sur l’URI suivant.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="7fbaa-147">Le service renvoie une liste des régions et leurs URI de points de terminaison Azure Cosmos DB correspondants pour les réplicas.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-147">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="7fbaa-148">La région d’écriture en cours est indiquée dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-148">The current write region will be indicated in the response.</span></span> <span data-ttu-id="7fbaa-149">Le client peut ensuite sélectionner le point de terminaison approprié pour toutes les autres requêtes d’API REST, comme suit.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-149">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="7fbaa-150">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="7fbaa-150">Example response</span></span>

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* <span data-ttu-id="7fbaa-151">Les requêtes PUT, POST et DELETE doivent accéder à l’URI d’écriture indiqué</span><span class="sxs-lookup"><span data-stu-id="7fbaa-151">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="7fbaa-152">Toutes les requêtes GET et autres demandes en lecture seule (par ex., Requêtes) peuvent accéder à n’importe quel point de terminaison choisi par le client</span><span class="sxs-lookup"><span data-stu-id="7fbaa-152">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="7fbaa-153">L’écriture de demandes dans les régions en lecture seule échoue avec le code d’erreur HTTP 403 (« Interdit »).</span><span class="sxs-lookup"><span data-stu-id="7fbaa-153">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="7fbaa-154">Si la région d’écriture change après la phase de découverte initiale du client, les écritures suivantes dans la région d’écriture précédente échouent avec le code d’erreur HTTP 403 (« Interdit »).</span><span class="sxs-lookup"><span data-stu-id="7fbaa-154">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="7fbaa-155">Le client doit alors exécuter à nouveau la requête GET sur la liste des régions pour obtenir la région d’écriture mise à jour.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-155">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="7fbaa-156">C’est ici que s’achève ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="7fbaa-157">Découvrez comment gérer la cohérence de votre compte répliqué à l’échelle mondiale en lisant l’article [Niveaux de cohérence dans Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="7fbaa-157">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="7fbaa-158">Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Azure Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="7fbaa-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fbaa-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7fbaa-159">Next steps</span></span>

<span data-ttu-id="7fbaa-160">Dans ce didacticiel, vous avez effectué les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7fbaa-160">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7fbaa-161">Configurer la distribution mondiale à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="7fbaa-161">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="7fbaa-162">Configurer la distribution mondiale à l’aide des API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7fbaa-162">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="7fbaa-163">Vous pouvez maintenant passer au didacticiel suivant pour apprendre à développer en local à l’aide de l’émulateur local Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7fbaa-163">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fbaa-164">Développer en local avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="7fbaa-164">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

