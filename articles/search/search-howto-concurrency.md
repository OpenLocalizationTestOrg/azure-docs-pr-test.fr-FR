---
title: "Gestion des écritures simultanées dans les ressources Recherche Azure"
description: "Utilisez l’accès concurrentiel optimiste pour éviter les collisions entre des mises à jour ou des suppressions d’index, d’indexeurs et de sources de données Recherche Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: aee1b7376d4829e3e2f5a232525e3c3cb4df9d8e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-manage-concurrency-in-azure-search"></a><span data-ttu-id="0de64-103">Gestion de l’accès concurrentiel dans Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="0de64-103">How to manage concurrency in Azure Search</span></span>

<span data-ttu-id="0de64-104">Lors de la gestion de ressources Recherche Azure telles que des index et des sources de données, il est important de mettre à jour les ressources en toute sécurité, surtout si elles sont accessibles simultanément par différents composants de votre application.</span><span class="sxs-lookup"><span data-stu-id="0de64-104">When managing Azure Search resources such as indexes and data sources, it's important to update resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="0de64-105">Lorsque deux clients mettent à jour une ressource en même temps sans coordination, cela peut créer des conditions de concurrence.</span><span class="sxs-lookup"><span data-stu-id="0de64-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="0de64-106">Pour éviter ce problème, Recherche Azure offre un *modèle d’accès concurrentiel optimiste*.</span><span class="sxs-lookup"><span data-stu-id="0de64-106">To prevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="0de64-107">Aucun verrou n’est appliqué aux ressources.</span><span class="sxs-lookup"><span data-stu-id="0de64-107">There are no locks on a resource.</span></span> <span data-ttu-id="0de64-108">Au lieu de cela, chaque ressource présente une étiquette d’entité (ETag) qui identifie la version de la ressource afin que vous puissiez élaborer des requêtes sans risquer de remplacements accidentels.</span><span class="sxs-lookup"><span data-stu-id="0de64-108">Instead, there is an ETag for every resource that identifies the resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="0de64-109">Le code conceptuel de cet [exemple de solution C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) illustre le fonctionnement du contrôle d’accès concurrentiel dans Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="0de64-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="0de64-110">Le code crée des conditions qui appellent le contrôle d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="0de64-110">The code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="0de64-111">La lecture du [fragment de code ci-dessous](#samplecode) est probablement suffisante pour la plupart des développeurs, mais si vous souhaitez l’exécuter, modifiez le fichier appsettings.json pour y ajouter le nom du service et une clé API d’administration.</span><span class="sxs-lookup"><span data-stu-id="0de64-111">Reading the [code fragment below](#samplecode) is probably sufficient for most developers, but if you want to run it, edit appsettings.json to add the service name and an admin api-key.</span></span> <span data-ttu-id="0de64-112">Pour une URL de service `http://myservice.search.windows.net`, le nom du service est `myservice`.</span><span class="sxs-lookup"><span data-stu-id="0de64-112">Given a service URL of `http://myservice.search.windows.net`, the service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="0de64-113">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="0de64-113">How it works</span></span>

<span data-ttu-id="0de64-114">L’accès concurrentiel optimiste est implémenté via des contrôles de conditions d’accès dans les appels d’API écrivant dans des index, des indexeurs, des sources de données et des ressources synonymMap.</span><span class="sxs-lookup"><span data-stu-id="0de64-114">Optimistic concurrency is implemented through access condition checks in API calls writing to indexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="0de64-115">Toutes les ressources présentent une [ *étiquette d’entité (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) qui fournit des informations sur la version de l’objet.</span><span class="sxs-lookup"><span data-stu-id="0de64-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="0de64-116">En vérifiant d’abord l’ETag, vous pouvez éviter les mises à jour simultanées dans un flux de travail classique (obtention, modification locale, mise à jour) en vous assurant que l’ETag de la ressource correspond à celui de votre copie locale.</span><span class="sxs-lookup"><span data-stu-id="0de64-116">By checking the ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring the resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="0de64-117">L’API REST utilise un [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) sur l’en-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="0de64-117">The REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the request header.</span></span>
+ <span data-ttu-id="0de64-118">Le Kit de développement logiciel (SDK) .NET spécifie l’ETag via un objet accessCondition en définissant l’en-tête [If-Match | If-Match-None](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) sur la ressource.</span><span class="sxs-lookup"><span data-stu-id="0de64-118">The .NET SDK sets the ETag through an accessCondition object, setting the [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the resource.</span></span> <span data-ttu-id="0de64-119">Tout objet héritant de l’interface [IResourceWithETag](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) (Kit de développement logiciel [SDK] .NET) présente un objet accessCondition.</span><span class="sxs-lookup"><span data-stu-id="0de64-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="0de64-120">À chaque fois que vous mettez à jour une ressource, son ETag change automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0de64-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="0de64-121">Lorsque vous implémentez la gestion de l’accès concurrentiel, vous placez simplement sur la requête de mise à jour une condition préalable qui exige que la ressource distante présente le même ETag que la copie de la ressource que vous avez modifiée sur le client.</span><span class="sxs-lookup"><span data-stu-id="0de64-121">When you implement concurrency management, all you're doing is putting a precondition on the update request that requires the remote resource to have the same ETag as the copy of the resource that you modified on the client.</span></span> <span data-ttu-id="0de64-122">Si un processus simultané a déjà modifié la ressource distante, l’ETag ne correspondra pas à la condition préalable et la requête échouera avec l’erreur HTTP 412.</span><span class="sxs-lookup"><span data-stu-id="0de64-122">If a concurrent process has changed the remote resource already, the ETag will not match the precondition and the request will fail with HTTP 412.</span></span> <span data-ttu-id="0de64-123">Si vous utilisez le Kit de développement logiciel (SDK) .NET, cela se manifeste sous la forme d’une exception `CloudException`, où la méthode d’extension `IsAccessConditionFailed()` renvoie la valeur true.</span><span class="sxs-lookup"><span data-stu-id="0de64-123">If you're using the .NET SDK, this manifests as a `CloudException` where the `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="0de64-124">Il n’existe qu’un seul mécanisme pour l’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="0de64-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="0de64-125">Celui-ci est systématiquement utilisé, peu importe l’API employée pour les mises à jour de ressources.</span><span class="sxs-lookup"><span data-stu-id="0de64-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="0de64-126">Cas d’usage et exemple de code</span><span class="sxs-lookup"><span data-stu-id="0de64-126">Use cases and sample code</span></span>

<span data-ttu-id="0de64-127">Le code suivant illustre les contrôles accessCondition pour les opérations de mise à jour de clé :</span><span class="sxs-lookup"><span data-stu-id="0de64-127">The following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="0de64-128">Échec de la mise à jour si la ressource n’existe plus</span><span class="sxs-lookup"><span data-stu-id="0de64-128">Fail an update if the resource no longer exists</span></span>
+ <span data-ttu-id="0de64-129">Échec de la mise à jour si la version de la ressource change</span><span class="sxs-lookup"><span data-stu-id="0de64-129">Fail an update if the resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="0de64-130">Exemple de code tiré du [programme DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="0de64-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of the resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once the resource exists in Azure Search, its ETag will be populated. Make sure to use the object
            // returned by the SearchServiceClient! Otherwise, you will still have the old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that the update will only
            // succeed if the index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates to the same resource. If another
            // client tries to update the resource, it will fail as long as all clients are using the right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. To start, both clients see the same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates the index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries to update the index, but fails, thanks to the ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed to update the index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of the DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using the Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // the resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key to end application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a><span data-ttu-id="0de64-131">Modèle de conception</span><span class="sxs-lookup"><span data-stu-id="0de64-131">Design pattern</span></span>

<span data-ttu-id="0de64-132">Un modèle de conception pour l’implémentation de l’accès concurrentiel optimiste doit inclure une boucle qui effectue une nouvelle tentative de contrôle de la condition d’accès, un test de la condition d’accès et récupère éventuellement une ressource mise à jour avant d’essayer de réappliquer les modifications.</span><span class="sxs-lookup"><span data-stu-id="0de64-132">A design pattern for implementing optimistic concurrency should include a loop that retries the access condition check, a test for the access condition, and optionally retrieves an updated resource before attempting to re-apply the changes.</span></span> 

<span data-ttu-id="0de64-133">Cet extrait de code illustre l’ajout d’une ressource synonymMap à un index existant.</span><span class="sxs-lookup"><span data-stu-id="0de64-133">This code snippet illustrates the addition of a synonymMap to an index that already exists.</span></span> <span data-ttu-id="0de64-134">Ce code est tiré du [didacticiel C# des synonymes (version préliminaire) pour la Recherche Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="0de64-134">This code is from the [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="0de64-135">L’extrait de code obtient l’index « hotel », vérifie la version de l’objet pour une opération de mise à jour, lève une exception si la condition échoue, puis retente l’opération (jusqu’à trois fois), en commençant par extraire l’index du serveur pour obtenir sa dernière version.</span><span class="sxs-lookup"><span data-stu-id="0de64-135">The snippet gets the "hotels" index, checks the object version on an update operation, throws an exception if the condition fails, and then retries the operation (up to three times), starting with index retrieval from the server to get the latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // The IfNotChanged condition ensures that the index is updated only if the ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated the index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a><span data-ttu-id="0de64-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0de64-136">Next steps</span></span>

<span data-ttu-id="0de64-137">Examinez l’[exemple C# de synonymes](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) pour avoir une illustration de la mise à jour en toute sécurité d’un index existant.</span><span class="sxs-lookup"><span data-stu-id="0de64-137">Review the [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how to safely update an existing index.</span></span>

<span data-ttu-id="0de64-138">Essayez de modifier l’un des exemples suivants pour inclure des ETags ou des objets AccessCondition.</span><span class="sxs-lookup"><span data-stu-id="0de64-138">Try modifying either of the following samples to include ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="0de64-139">Exemple d’API REST sur GitHub</span><span class="sxs-lookup"><span data-stu-id="0de64-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="0de64-140">[Exemple de Kit de développement logiciel (SDK) sur GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started)</span><span class="sxs-lookup"><span data-stu-id="0de64-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="0de64-141">Cette solution inclut le projet « DotNetEtagsExplainer », qui contient le code présenté dans cet article.</span><span class="sxs-lookup"><span data-stu-id="0de64-141">This solution includes the "DotNetEtagsExplainer" project containing the code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="0de64-142">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0de64-142">See also</span></span>

  <span data-ttu-id="0de64-143">[En-têtes de requête et de réponse HTTP courants](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span><span class="sxs-lookup"><span data-stu-id="0de64-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="0de64-144">[Codes d’état HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Opérations d’index (API REST)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="0de64-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>