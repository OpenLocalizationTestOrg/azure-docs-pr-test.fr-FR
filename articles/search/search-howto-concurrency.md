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
# <a name="how-toomanage-concurrency-in-azure-search"></a>Comment toomanage l’accès concurrentiel dans Azure Search

Lors de la gestion des ressources Azure Search tels que des index et des sources de données, il est important tooupdate ressources en toute sécurité, surtout si les ressources sont accessibles simultanément par les différents composants de votre application. Lorsque deux clients mettent à jour une ressource en même temps sans coordination, cela peut créer des conditions de concurrence. tooprevent, Azure Search offre les fonctionnalités un *modèle d’accès concurrentiel optimiste*. Aucun verrou n’est appliqué aux ressources. Au lieu de cela, il est un ETag pour toutes les ressources qui identifie la version de la ressource hello afin que vous pouvez créer des requêtes éviter accidentelle remplace.

> [!Tip]
> Le code conceptuel de cet [exemple de solution C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) illustre le fonctionnement du contrôle d’accès concurrentiel dans Recherche Azure. code de Hello crée des conditions qui appellent le contrôle d’accès concurrentiel. Hello de lecture [fragment de code ci-dessous](#samplecode) est probablement suffisante pour la plupart des développeurs, mais si vous souhaitez toorun, nom du service modifier appsettings.json tooadd hello et une clé d’api admin. Étant donné une URL de service de `http://myservice.search.windows.net`, nom du service hello est `myservice`.

## <a name="how-it-works"></a>Fonctionnement

OPTIMISTIC concurrency est implémentée via l’accès condition vérifie dans les appels d’API écriture tooindexes, des indexeurs, des sources de données et des ressources de synonymMap. 

Toutes les ressources présentent une [ *étiquette d’entité (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) qui fournit des informations sur la version de l’objet. En vérifiant hello ETag tout d’abord, vous pouvez éviter les mises à jour simultanées dans un workflow standard (get, modifier localement, mettre à jour) en s’assurant que les correspondances d’ETag de la ressource hello votre copie locale. 

+ Hello API REST utilise un [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) sur l’en-tête de demande hello.
+ Hello SDK .NET définit hello ETag via un objet accessCondition, paramètre hello [If-Match | En-tête If-Match-aucun](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) sur la ressource de hello. Tout objet héritant de l’interface [IResourceWithETag](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) (Kit de développement logiciel [SDK] .NET) présente un objet accessCondition.

À chaque fois que vous mettez à jour une ressource, son ETag change automatiquement. Lorsque vous implémentez la gestion des accès concurrentiels, vous pour placer une condition préalable à la demande de mise à jour hello nécessitant des ressources distantes de hello toohave hello ETag même en tant que copie hello de ressource hello que vous avez modifié sur le client de hello. Si un processus simultané a déjà été modifié les ressources distantes hello, hello ETag ne correspond pas à la condition préalable de hello et demande de hello échoue avec HTTP 412. Si vous utilisez hello .NET SDK, cela se manifeste en tant qu’un `CloudException` où hello `IsAccessConditionFailed()` méthode d’extension retourne la valeur true.

> [!Note]
> Il n’existe qu’un seul mécanisme pour l’accès concurrentiel. Celui-ci est systématiquement utilisé, peu importe l’API employée pour les mises à jour de ressources. 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a>Cas d’usage et exemple de code

Hello suivant de code illustre accessCondition vérifie pour les opérations de mise à jour de clé :

+ Échec d’une mise à jour si les ressources hello n’existe plus
+ Échec d’une mise à jour si la modification de la version de ressource hello

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a>Exemple de code tiré du [programme DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)

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

## <a name="design-pattern"></a>Modèle de conception

Un modèle de conception pour l’implémentation de l’accès concurrentiel optimiste doit inclure une boucle qui effectue une vérification de la condition hello accès, un test de la condition d’accès hello, nouvelle tentative et éventuellement récupère une ressource mise à jour avant de tenter de toore-appliquer les modifications de hello. 

Cet extrait de code illustre l’ajout de hello d’un index tooan synonymMap qui existe déjà. Ce code est issu hello [didacticiel c# synonyme (version préliminaire) pour Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk). 

extrait de code Hello Obtient l’index de « hôtels » de hello, vérifie la version de l’objet hello sur une opération de mise à jour, lève une exception si la condition de hello échoue et puis tentatives hello opération (haut toothree fois), en commençant par la récupération d’index à partir de messages hello du serveur tooget hello plus récentes Version.

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


## <a name="next-steps"></a>Étapes suivantes

Hello de révision [exemple de synonymes c#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) pour plus d’informations sur comment toosafely mettre à jour un index existant.

Essayez de modifier un des éléments suivants de hello échantillonne les objets ETags ou AccessCondition tooinclude.

+ [Exemple d’API REST sur GitHub](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ [Exemple de Kit de développement logiciel (SDK) sur GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started) Cette solution inclut un projet de « DotNetEtagsExplainer » hello contenant du code hello présentée dans cet article.

## <a name="see-also"></a>Voir aussi

  [En-têtes de requête et de réponse HTTP courants](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)    
  [Codes d’état HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes)[Opérations d’index (API REST)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)