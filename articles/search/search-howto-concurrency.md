---
title: "toomanage aaaHow simultanée écrit tooresources dans Azure Search"
description: "Utilisez les collisions d’accès concurrentiel optimiste tooavoid air intermédiaire sur l’index de recherche tooAzure mises à jour ou suppressions, les indexeurs, les sources de données."
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
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a><span data-ttu-id="c4c33-103">Comment toomanage l’accès concurrentiel dans Azure Search</span><span class="sxs-lookup"><span data-stu-id="c4c33-103">How toomanage concurrency in Azure Search</span></span>

<span data-ttu-id="c4c33-104">Lors de la gestion des ressources Azure Search tels que des index et des sources de données, il est important tooupdate ressources en toute sécurité, surtout si les ressources sont accessibles simultanément par les différents composants de votre application.</span><span class="sxs-lookup"><span data-stu-id="c4c33-104">When managing Azure Search resources such as indexes and data sources, it's important tooupdate resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="c4c33-105">Lorsque deux clients mettent à jour une ressource en même temps sans coordination, cela peut créer des conditions de concurrence.</span><span class="sxs-lookup"><span data-stu-id="c4c33-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="c4c33-106">tooprevent, Azure Search offre les fonctionnalités un *modèle d’accès concurrentiel optimiste*.</span><span class="sxs-lookup"><span data-stu-id="c4c33-106">tooprevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="c4c33-107">Aucun verrou n’est appliqué aux ressources.</span><span class="sxs-lookup"><span data-stu-id="c4c33-107">There are no locks on a resource.</span></span> <span data-ttu-id="c4c33-108">Au lieu de cela, il est un ETag pour toutes les ressources qui identifie la version de la ressource hello afin que vous pouvez créer des requêtes éviter accidentelle remplace.</span><span class="sxs-lookup"><span data-stu-id="c4c33-108">Instead, there is an ETag for every resource that identifies hello resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="c4c33-109">Le code conceptuel de cet [exemple de solution C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) illustre le fonctionnement du contrôle d’accès concurrentiel dans Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="c4c33-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="c4c33-110">code de Hello crée des conditions qui appellent le contrôle d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="c4c33-110">hello code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="c4c33-111">Hello de lecture [fragment de code ci-dessous](#samplecode) est probablement suffisante pour la plupart des développeurs, mais si vous souhaitez toorun, nom du service modifier appsettings.json tooadd hello et une clé d’api admin.</span><span class="sxs-lookup"><span data-stu-id="c4c33-111">Reading hello [code fragment below](#samplecode) is probably sufficient for most developers, but if you want toorun it, edit appsettings.json tooadd hello service name and an admin api-key.</span></span> <span data-ttu-id="c4c33-112">Étant donné une URL de service de `http://myservice.search.windows.net`, nom du service hello est `myservice`.</span><span class="sxs-lookup"><span data-stu-id="c4c33-112">Given a service URL of `http://myservice.search.windows.net`, hello service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="c4c33-113">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="c4c33-113">How it works</span></span>

<span data-ttu-id="c4c33-114">OPTIMISTIC concurrency est implémentée via l’accès condition vérifie dans les appels d’API écriture tooindexes, des indexeurs, des sources de données et des ressources de synonymMap.</span><span class="sxs-lookup"><span data-stu-id="c4c33-114">Optimistic concurrency is implemented through access condition checks in API calls writing tooindexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="c4c33-115">Toutes les ressources présentent une [ *étiquette d’entité (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) qui fournit des informations sur la version de l’objet.</span><span class="sxs-lookup"><span data-stu-id="c4c33-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="c4c33-116">En vérifiant hello ETag tout d’abord, vous pouvez éviter les mises à jour simultanées dans un workflow standard (get, modifier localement, mettre à jour) en s’assurant que les correspondances d’ETag de la ressource hello votre copie locale.</span><span class="sxs-lookup"><span data-stu-id="c4c33-116">By checking hello ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring hello resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="c4c33-117">Hello API REST utilise un [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) sur l’en-tête de demande hello.</span><span class="sxs-lookup"><span data-stu-id="c4c33-117">hello REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello request header.</span></span>
+ <span data-ttu-id="c4c33-118">Hello SDK .NET définit hello ETag via un objet accessCondition, paramètre hello [If-Match | En-tête If-Match-aucun](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) sur la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="c4c33-118">hello .NET SDK sets hello ETag through an accessCondition object, setting hello [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello resource.</span></span> <span data-ttu-id="c4c33-119">Tout objet héritant de l’interface [IResourceWithETag](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) (Kit de développement logiciel [SDK] .NET) présente un objet accessCondition.</span><span class="sxs-lookup"><span data-stu-id="c4c33-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="c4c33-120">À chaque fois que vous mettez à jour une ressource, son ETag change automatiquement.</span><span class="sxs-lookup"><span data-stu-id="c4c33-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="c4c33-121">Lorsque vous implémentez la gestion des accès concurrentiels, vous pour placer une condition préalable à la demande de mise à jour hello nécessitant des ressources distantes de hello toohave hello ETag même en tant que copie hello de ressource hello que vous avez modifié sur le client de hello.</span><span class="sxs-lookup"><span data-stu-id="c4c33-121">When you implement concurrency management, all you're doing is putting a precondition on hello update request that requires hello remote resource toohave hello same ETag as hello copy of hello resource that you modified on hello client.</span></span> <span data-ttu-id="c4c33-122">Si un processus simultané a déjà été modifié les ressources distantes hello, hello ETag ne correspond pas à la condition préalable de hello et demande de hello échoue avec HTTP 412.</span><span class="sxs-lookup"><span data-stu-id="c4c33-122">If a concurrent process has changed hello remote resource already, hello ETag will not match hello precondition and hello request will fail with HTTP 412.</span></span> <span data-ttu-id="c4c33-123">Si vous utilisez hello .NET SDK, cela se manifeste en tant qu’un `CloudException` où hello `IsAccessConditionFailed()` méthode d’extension retourne la valeur true.</span><span class="sxs-lookup"><span data-stu-id="c4c33-123">If you're using hello .NET SDK, this manifests as a `CloudException` where hello `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="c4c33-124">Il n’existe qu’un seul mécanisme pour l’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="c4c33-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="c4c33-125">Celui-ci est systématiquement utilisé, peu importe l’API employée pour les mises à jour de ressources.</span><span class="sxs-lookup"><span data-stu-id="c4c33-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="c4c33-126">Cas d’usage et exemple de code</span><span class="sxs-lookup"><span data-stu-id="c4c33-126">Use cases and sample code</span></span>

<span data-ttu-id="c4c33-127">Hello suivant de code illustre accessCondition vérifie pour les opérations de mise à jour de clé :</span><span class="sxs-lookup"><span data-stu-id="c4c33-127">hello following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="c4c33-128">Échec d’une mise à jour si les ressources hello n’existe plus</span><span class="sxs-lookup"><span data-stu-id="c4c33-128">Fail an update if hello resource no longer exists</span></span>
+ <span data-ttu-id="c4c33-129">Échec d’une mise à jour si la modification de la version de ressource hello</span><span class="sxs-lookup"><span data-stu-id="c4c33-129">Fail an update if hello resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="c4c33-130">Exemple de code tiré du [programme DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="c4c33-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

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
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
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
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
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

## <a name="design-pattern"></a><span data-ttu-id="c4c33-131">Modèle de conception</span><span class="sxs-lookup"><span data-stu-id="c4c33-131">Design pattern</span></span>

<span data-ttu-id="c4c33-132">Un modèle de conception pour l’implémentation de l’accès concurrentiel optimiste doit inclure une boucle qui effectue une vérification de la condition hello accès, un test de la condition d’accès hello, nouvelle tentative et éventuellement récupère une ressource mise à jour avant de tenter de toore-appliquer les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="c4c33-132">A design pattern for implementing optimistic concurrency should include a loop that retries hello access condition check, a test for hello access condition, and optionally retrieves an updated resource before attempting toore-apply hello changes.</span></span> 

<span data-ttu-id="c4c33-133">Cet extrait de code illustre l’ajout de hello d’un index tooan synonymMap qui existe déjà.</span><span class="sxs-lookup"><span data-stu-id="c4c33-133">This code snippet illustrates hello addition of a synonymMap tooan index that already exists.</span></span> <span data-ttu-id="c4c33-134">Ce code est issu hello [didacticiel c# synonyme (version préliminaire) pour Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="c4c33-134">This code is from hello [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="c4c33-135">extrait de code Hello Obtient l’index de « hôtels » de hello, vérifie la version de l’objet hello sur une opération de mise à jour, lève une exception si la condition de hello échoue et puis tentatives hello opération (haut toothree fois), en commençant par la récupération d’index à partir de messages hello du serveur tooget hello plus récentes Version.</span><span class="sxs-lookup"><span data-stu-id="c4c33-135">hello snippet gets hello "hotels" index, checks hello object version on an update operation, throws an exception if hello condition fails, and then retries hello operation (up toothree times), starting with index retrieval from hello server tooget hello latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
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


## <a name="next-steps"></a><span data-ttu-id="c4c33-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c4c33-136">Next steps</span></span>

<span data-ttu-id="c4c33-137">Hello de révision [exemple de synonymes c#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) pour plus d’informations sur comment toosafely mettre à jour un index existant.</span><span class="sxs-lookup"><span data-stu-id="c4c33-137">Review hello [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how toosafely update an existing index.</span></span>

<span data-ttu-id="c4c33-138">Essayez de modifier un des éléments suivants de hello échantillonne les objets ETags ou AccessCondition tooinclude.</span><span class="sxs-lookup"><span data-stu-id="c4c33-138">Try modifying either of hello following samples tooinclude ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="c4c33-139">Exemple d’API REST sur GitHub</span><span class="sxs-lookup"><span data-stu-id="c4c33-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="c4c33-140">[Exemple de Kit de développement logiciel (SDK) sur GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started)</span><span class="sxs-lookup"><span data-stu-id="c4c33-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="c4c33-141">Cette solution inclut un projet de « DotNetEtagsExplainer » hello contenant du code hello présentée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c4c33-141">This solution includes hello "DotNetEtagsExplainer" project containing hello code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="c4c33-142">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c4c33-142">See also</span></span>

  <span data-ttu-id="c4c33-143">[En-têtes de requête et de réponse HTTP courants](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span><span class="sxs-lookup"><span data-stu-id="c4c33-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="c4c33-144">[Codes d’état HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes)[Opérations d’index (API REST)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="c4c33-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>