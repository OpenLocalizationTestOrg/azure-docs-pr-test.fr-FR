---
title: "didacticiel de distribution globale aaaAzure Cosmos DB pour l’API DocumentDB | Documents Microsoft"
description: "Découvrez comment à l’aide de distribution globale de base de données Azure Cosmos toosetup hello des API DocumentDB."
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
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a><span data-ttu-id="44257-104">À l’aide de distribution globale de base de données Azure Cosmos toosetup comment hello des API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="44257-104">How toosetup Azure Cosmos DB global distribution using hello DocumentDB API</span></span>

<span data-ttu-id="44257-105">Dans cet article, nous montrons comment toouse hello toosetup portail Azure distribution globale de base de données Azure Cosmos et connectez-vous à l’aide de hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="44257-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello DocumentDB API.</span></span>

<span data-ttu-id="44257-106">Cet article traite des hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="44257-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="44257-107">Configurer la distribution globale à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="44257-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="44257-108">Configurer la distribution globale à l’aide de hello [APIs DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="44257-108">Configure global distribution using hello [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a><span data-ttu-id="44257-109">Connexion tooa la région préférée à l’aide de hello API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="44257-109">Connecting tooa preferred region using hello DocumentDB API</span></span>

<span data-ttu-id="44257-110">Dans l’avantage de tootake d’ordre de [distribution globale](distribute-data-globally.md), les applications clientes peuvent spécifier hello classés de liste de préférence des régions toobe utilisé tooperform les opérations de document.</span><span class="sxs-lookup"><span data-stu-id="44257-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="44257-111">Pour ce faire, vous pouvez définir la stratégie de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="44257-111">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="44257-112">Selon la configuration du compte de base de données Azure Cosmos hello, disponibilité régionale en cours et la liste de préférence hello spécifié, hello la plupart des point de terminaison optimale est sélectionnée par hello DocumentDB SDK tooperform écrire et lire des opérations.</span><span class="sxs-lookup"><span data-stu-id="44257-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello DocumentDB SDK tooperform write and read operations.</span></span>

<span data-ttu-id="44257-113">Cette liste de préférence est spécifiée lors de l’initialisation d’une connexion à l’aide de kits de développement logiciel hello DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="44257-113">This preference list is specified when initializing a connection using hello DocumentDB SDKs.</span></span> <span data-ttu-id="44257-114">Hello kits de développement logiciel accepte un paramètre facultatif « PreferredLocations » qui est une liste ordonnée des régions Azure.</span><span class="sxs-lookup"><span data-stu-id="44257-114">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="44257-115">Hello Kit de développement logiciel enverra automatiquement région pour l’écriture de toutes les écritures toohello actuelle.</span><span class="sxs-lookup"><span data-stu-id="44257-115">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="44257-116">Toutes les lectures seront envoyés toohello de première région disponibles dans la liste de PreferredLocations hello.</span><span class="sxs-lookup"><span data-stu-id="44257-116">All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="44257-117">En cas de demande de hello, client de hello échouer la région de hello liste toohello suivante et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="44257-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="44257-118">Hello kits de développement logiciel tente uniquement tooread de régions hello spécifié dans PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="44257-118">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="44257-119">Ainsi, par exemple, si hello compte de base de données est disponible dans trois régions, mais le client de hello spécifie uniquement deux des régions de non-écriture hello pour PreferredLocations, puis aucune lecture ne sera utilisée en dehors de la région d’écriture hello, même dans les cas de hello de basculement.</span><span class="sxs-lookup"><span data-stu-id="44257-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="44257-120">application Hello peut vérifier le point de terminaison hello actuel écriture et lecture de point de terminaison choisi par hello SDK par la vérification deux propriétés, WriteEndpoint et ReadEndpoint, disponible dans la version du Kit de développement logiciel 1.8 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="44257-120">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="44257-121">Si hello PreferredLocations propriété n’est pas définie, toutes les demandes seront pris en charge à partir de la zone d’écriture en cours hello.</span><span class="sxs-lookup"><span data-stu-id="44257-121">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="44257-122">Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="44257-122">.NET SDK</span></span>
<span data-ttu-id="44257-123">Hello SDK peut servir sans aucune modification du code.</span><span class="sxs-lookup"><span data-stu-id="44257-123">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="44257-124">Dans ce cas, hello SDK dirige les opérations de lecture automatiquement et écrit la zone d’écriture en cours toohello.</span><span class="sxs-lookup"><span data-stu-id="44257-124">In this case, hello SDK automatically directs both reads and writes toohello current write region.</span></span>

<span data-ttu-id="44257-125">Dans la version 1.8 de hello .NET SDK, hello ConnectionPolicy paramètre de constructeur de DocumentClient hello est une propriété appelée Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="44257-125">In version 1.8 and later of hello .NET SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="44257-126">Cette propriété est de type Collection `<string>` et doit contenir une liste des noms de région.</span><span class="sxs-lookup"><span data-stu-id="44257-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="44257-127">les valeurs de chaîne Hello sont mis en forme par colonne de nom de la région de hello sur hello [régions Azure] [ regions] page, sans espaces avant ou après hello premier et dernier caractère respectivement.</span><span class="sxs-lookup"><span data-stu-id="44257-127">hello string values are formatted per hello Region Name column on hello [Azure Regions][regions] page, with no spaces before or after hello first and last character respectively.</span></span>

<span data-ttu-id="44257-128">écriture en cours de Hello et lecture des points de terminaison sont disponibles dans DocumentClient.WriteEndpoint et DocumentClient.ReadEndpoint respectivement.</span><span class="sxs-lookup"><span data-stu-id="44257-128">hello current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="44257-129">URL de Hello pour les points de terminaison hello ne doivent pas être considérés comme des constantes de longue durées.</span><span class="sxs-lookup"><span data-stu-id="44257-129">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="44257-130">service de Hello peut mettre à jour à tout moment.</span><span class="sxs-lookup"><span data-stu-id="44257-130">hello service may update these at any point.</span></span> <span data-ttu-id="44257-131">Hello SDK gère cette modification automatiquement.</span><span class="sxs-lookup"><span data-stu-id="44257-131">hello SDK handles this change automatically.</span></span>
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

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="44257-132">SDK Node.js, JavaScript et Python</span><span class="sxs-lookup"><span data-stu-id="44257-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="44257-133">Hello SDK peut servir sans aucune modification du code.</span><span class="sxs-lookup"><span data-stu-id="44257-133">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="44257-134">Dans ce cas, hello que SDK dirigera automatiquement à la fois lit et écrit la zone d’écriture en cours toohello.</span><span class="sxs-lookup"><span data-stu-id="44257-134">In this case, hello SDK will automatically direct both reads and writes toohello current write region.</span></span>

<span data-ttu-id="44257-135">Dans la version 1.8 et version ultérieure de chaque SDK, hello ConnectionPolicy paramètre hello DocumentClient constructeur une nouvelle propriété nommée DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="44257-135">In version 1.8 and later of each SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="44257-136">Ce paramètre est un tableau de chaînes qui prend une liste de noms de régions.</span><span class="sxs-lookup"><span data-stu-id="44257-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="44257-137">les noms de Hello sont mis en forme par colonne de nom de la région de hello Bonjour [régions Azure] [ regions] page.</span><span class="sxs-lookup"><span data-stu-id="44257-137">hello names are formatted per hello Region Name column in hello [Azure Regions][regions] page.</span></span> <span data-ttu-id="44257-138">Vous pouvez également utiliser des constantes de hello prédéfini dans l’objet de commodité hello AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="44257-138">You can also use hello predefined constants in hello convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="44257-139">écriture en cours de Hello et lecture des points de terminaison sont disponibles dans DocumentClient.getWriteEndpoint et DocumentClient.getReadEndpoint respectivement.</span><span class="sxs-lookup"><span data-stu-id="44257-139">hello current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="44257-140">URL de Hello pour les points de terminaison hello ne doivent pas être considérés comme des constantes de longue durées.</span><span class="sxs-lookup"><span data-stu-id="44257-140">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="44257-141">service de Hello peut mettre à jour à tout moment.</span><span class="sxs-lookup"><span data-stu-id="44257-141">hello service may update these at any point.</span></span> <span data-ttu-id="44257-142">Hello SDK gère automatiquement ce changement.</span><span class="sxs-lookup"><span data-stu-id="44257-142">hello SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="44257-143">Voici un exemple de code pour NodeJS/Javascript.</span><span class="sxs-lookup"><span data-stu-id="44257-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="44257-144">Python et Java suivront hello même modèle.</span><span class="sxs-lookup"><span data-stu-id="44257-144">Python and Java will follow hello same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="44257-145">REST</span><span class="sxs-lookup"><span data-stu-id="44257-145">REST</span></span>
<span data-ttu-id="44257-146">Une fois qu’un compte de base de données a mis à disposition dans plusieurs régions, les clients peuvent interroger sa disponibilité en effectuant une requête GET sur hello suivant l’URI.</span><span class="sxs-lookup"><span data-stu-id="44257-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on hello following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="44257-147">service de Hello renvoie la liste des régions et de leur base de données Azure Cosmos point de terminaison correspondant URI pour les réplicas de hello.</span><span class="sxs-lookup"><span data-stu-id="44257-147">hello service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for hello replicas.</span></span> <span data-ttu-id="44257-148">zone d’écriture en cours Hello est indiqué dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="44257-148">hello current write region will be indicated in hello response.</span></span> <span data-ttu-id="44257-149">client de Hello peut ensuite sélectionner point de terminaison approprié hello pour toutes les autres demandes d’API REST comme suit.</span><span class="sxs-lookup"><span data-stu-id="44257-149">hello client can then select hello appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="44257-150">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="44257-150">Example response</span></span>

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


* <span data-ttu-id="44257-151">PUT, POST et DELETE de toutes les demandes doivent passer toohello indiqué écrire URI</span><span class="sxs-lookup"><span data-stu-id="44257-151">All PUT, POST and DELETE requests must go toohello indicated write URI</span></span>
* <span data-ttu-id="44257-152">Obtient tous les et les autres demandes en lecture seule (par exemple les requêtes) peuvent être tooany de point de terminaison de choix du client hello</span><span class="sxs-lookup"><span data-stu-id="44257-152">All GETs and other read-only requests (for example queries) may go tooany endpoint of hello client’s choice</span></span>

<span data-ttu-id="44257-153">Écriture des régions tooread uniquement les demandes échouent avec le code d’erreur HTTP 403 (« interdit »).</span><span class="sxs-lookup"><span data-stu-id="44257-153">Write requests tooread-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="44257-154">Si la zone d’écriture hello change après phase de la découverte initiale du client hello, ultérieur écrit toohello précédente région d’écriture échoue avec le code d’erreur HTTP 403 (« interdit »).</span><span class="sxs-lookup"><span data-stu-id="44257-154">If hello write region changes after hello client’s initial discovery phase, subsequent writes toohello previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="44257-155">client de Hello doit ensuite obtenir la liste des régions hello nouveau tooget hello écriture mis à jour la région.</span><span class="sxs-lookup"><span data-stu-id="44257-155">hello client should then GET hello list of regions again tooget hello updated write region.</span></span>

<span data-ttu-id="44257-156">C’est ici que s’achève ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="44257-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="44257-157">Vous pouvez apprendre comment toomanage hello la cohérence de votre compte de réplication globale en lisant [niveaux de cohérence dans la base de données Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="44257-157">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="44257-158">Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Azure Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="44257-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="44257-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="44257-159">Next steps</span></span>

<span data-ttu-id="44257-160">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="44257-160">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44257-161">Configurer la distribution globale à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="44257-161">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="44257-162">Configurer la distribution globale à l’aide de hello APIs DocumentDB</span><span class="sxs-lookup"><span data-stu-id="44257-162">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="44257-163">Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodevelop localement à l’aide de hello émulateur local de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="44257-163">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="44257-164">Développer localement avec l’émulateur de hello</span><span class="sxs-lookup"><span data-stu-id="44257-164">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

