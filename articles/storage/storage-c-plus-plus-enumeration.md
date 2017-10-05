---
title: "Listage des ressources de stockage Azure avec la bibliothèque cliente de stockage pour C++ | Microsoft Docs"
description: "Apprenez à utiliser les API de listage de la bibliothèque cliente Microsoft Azure Storage pour C++ pour énumérer conteneurs, objets blob, files d'attente, tables et autres entités."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: 4a4ac7938989f821c092379aff3085f5e440d1c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="a60a9-103">Listage des ressources Azure Storage en C++</span><span class="sxs-lookup"><span data-stu-id="a60a9-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="a60a9-104">Les opérations de listage sont essentielles dans de nombreux scénarios de développement avec Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a60a9-104">Listing operations are key to many development scenarios with Azure Storage.</span></span> <span data-ttu-id="a60a9-105">Cet article explique comment énumérer de façon optimale les objets d’Azure Storage à l’aide des API de listage fournies par la bibliothèque cliente Microsoft Azure Storage pour C++.</span><span class="sxs-lookup"><span data-stu-id="a60a9-105">This article describes how to most efficiently enumerate objects in Azure Storage using the listing APIs provided in the Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="a60a9-106">Ce guide cible la bibliothèque cliente Stockage Azure C++ version 2.x, qui est disponible par le biais de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="a60a9-106">This guide targets the Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="a60a9-107">La bibliothèque cliente Storage propose diverses méthodes pour lister ou interroger les objets présents dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a60a9-107">The Storage Client Library provides a variety of methods to list or query objects in Azure Storage.</span></span> <span data-ttu-id="a60a9-108">Cet article traite les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="a60a9-108">This article addresses the following scenarios:</span></span>

* <span data-ttu-id="a60a9-109">liste les conteneurs présents dans un compte ;</span><span class="sxs-lookup"><span data-stu-id="a60a9-109">List containers in an account</span></span>
* <span data-ttu-id="a60a9-110">lister les objets blob présents dans un conteneur ou un répertoire d'objets blob virtuel ;</span><span class="sxs-lookup"><span data-stu-id="a60a9-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="a60a9-111">lister les files d'attente contenues dans un compte ;</span><span class="sxs-lookup"><span data-stu-id="a60a9-111">List queues in an account</span></span>
* <span data-ttu-id="a60a9-112">lister les tables contenues dans un compte ;</span><span class="sxs-lookup"><span data-stu-id="a60a9-112">List tables in an account</span></span>
* <span data-ttu-id="a60a9-113">interroger les entités d’une table.</span><span class="sxs-lookup"><span data-stu-id="a60a9-113">Query entities in a table</span></span>

<span data-ttu-id="a60a9-114">Chacune de ces méthodes est présentée en utilisant différentes surcharges qui varient en fonction des scénarios.</span><span class="sxs-lookup"><span data-stu-id="a60a9-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="a60a9-115">Opérations asynchrones/synchrones</span><span class="sxs-lookup"><span data-stu-id="a60a9-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="a60a9-116">Sachant que la bibliothèque cliente de stockage pour C++ s’appuie sur la [bibliothèque REST C++](https://github.com/Microsoft/cpprestsdk), par nature, les opérations asynchrones sont prises en charge en utilisant [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="a60a9-116">Because the Storage Client Library for C++ is built on top of the [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="a60a9-117">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a60a9-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="a60a9-118">Les opérations synchrones englobent les opérations asynchrones correspondantes :</span><span class="sxs-lookup"><span data-stu-id="a60a9-118">Synchronous operations wrap the corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="a60a9-119">Si vous travaillez avec plusieurs applications ou services de threading, nous vous recommandons d’utiliser directement les API asynchrones au lieu de créer un thread pour appeler des API, ce qui nuit considérablement aux performances.</span><span class="sxs-lookup"><span data-stu-id="a60a9-119">If you are working with multiple threading applications or services, we recommend that you use the async APIs directly instead of creating a thread to call the sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="a60a9-120">Listage segmenté</span><span class="sxs-lookup"><span data-stu-id="a60a9-120">Segmented listing</span></span>
<span data-ttu-id="a60a9-121">Du fait de son échelle, le stockage cloud nécessite un listage segmenté.</span><span class="sxs-lookup"><span data-stu-id="a60a9-121">The scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="a60a9-122">Par exemple, un conteneur d’objets blob Azure peut contenir plus d’un million d’objets blob et une table Azure plus d’un milliard d'entités.</span><span class="sxs-lookup"><span data-stu-id="a60a9-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="a60a9-123">Il ne s’agit pas là de chiffres théoriques, mais bien de cas d'utilisation réels de clients.</span><span class="sxs-lookup"><span data-stu-id="a60a9-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="a60a9-124">Il est donc impossible de lister tous les objets dans une même réponse.</span><span class="sxs-lookup"><span data-stu-id="a60a9-124">It is therefore impractical to list all objects in a single response.</span></span> <span data-ttu-id="a60a9-125">En revanche, il est possible de lister des objets en utilisant la pagination.</span><span class="sxs-lookup"><span data-stu-id="a60a9-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="a60a9-126">Chaque API de listage dispose d’une surcharge *segmentée* .</span><span class="sxs-lookup"><span data-stu-id="a60a9-126">Each of the listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="a60a9-127">La réponse à une opération de listage segmenté comporte les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a60a9-127">The response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="a60a9-128"><i>_segment</i>, qui contient le jeu de résultats retourné pour un seul appel à l'API de listage ;</span><span class="sxs-lookup"><span data-stu-id="a60a9-128"><i>_segment</i>, which contains the set of results returned for a single call to the listing API.</span></span>
* <span data-ttu-id="a60a9-129">*continuation_token* (jeton de liaison), qui est transmis à l’appel suivant pour obtenir la page de résultats suivante.</span><span class="sxs-lookup"><span data-stu-id="a60a9-129">*continuation_token*, which is passed to the next call in order to get the next page of results.</span></span> <span data-ttu-id="a60a9-130">Quand il n’y a plus de résultats à retourner, le jeton de liaison prend la valeur null.</span><span class="sxs-lookup"><span data-stu-id="a60a9-130">When there are no more results to return, the continuation token is null.</span></span>

<span data-ttu-id="a60a9-131">Par exemple, un appel type destiné à lister tous les objets blob présents dans un conteneur peut ressembler à l'extrait de code suivant.</span><span class="sxs-lookup"><span data-stu-id="a60a9-131">For example, a typical call to list all blobs in a container may look like the following code snippet.</span></span> <span data-ttu-id="a60a9-132">Le code est disponible dans nos [exemples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="a60a9-132">The code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in the blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="a60a9-133">Notez que le nombre de résultats retournés dans une page peut être contrôlé par le paramètre *max_results* au niveau de la surcharge de chaque API, par exemple :</span><span class="sxs-lookup"><span data-stu-id="a60a9-133">Note that the number of results returned in a page can be controlled by the parameter *max_results* in the overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="a60a9-134">Si vous ne spécifiez pas le paramètre *max_results*, le nombre de résultats retournés dans une seule page peut atteindre 5 000 résultats, soit la valeur maximale par défaut.</span><span class="sxs-lookup"><span data-stu-id="a60a9-134">If you do not specify the *max_results* parameter, the default maximum value of up to 5000 results is returned in a single page.</span></span>

<span data-ttu-id="a60a9-135">Sachez aussi qu’une requête au niveau du stockage d’une table Azure peut retourner aucun enregistrement ou moins d’enregistrements que la valeur du paramètre *max_results* que vous avez spécifiée, même si le jeton de liaison n’est pas vide.</span><span class="sxs-lookup"><span data-stu-id="a60a9-135">Also note that a query against Azure Table storage may return no records, or fewer records than the value of the *max_results* parameter that you specified, even if the continuation token is not empty.</span></span> <span data-ttu-id="a60a9-136">L’une des raisons possibles à cela est que la requête n’a pas pu aboutir dans un délai de cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="a60a9-136">One reason might be that the query could not complete in five seconds.</span></span> <span data-ttu-id="a60a9-137">Tant que le jeton de liaison n'est pas vide, la requête doit se poursuivre et votre code ne doit pas présumer la taille des résultats du segment.</span><span class="sxs-lookup"><span data-stu-id="a60a9-137">As long as the continuation token is not empty, the query should continue, and your code should not assume the size of segment results.</span></span>

<span data-ttu-id="a60a9-138">Le modèle de codage recommandé dans la plupart des scénarios est le listing segmenté, qui indique la progression explicite de l’opération de listing ou d'interrogation et la façon dont le service répond à chaque demande.</span><span class="sxs-lookup"><span data-stu-id="a60a9-138">The recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how the service responds to each request.</span></span> <span data-ttu-id="a60a9-139">Un contrôle de niveau inférieur de la progression du listage peut aider à contrôler la mémoire et les performances, en particulier pour les applications ou services C++.</span><span class="sxs-lookup"><span data-stu-id="a60a9-139">Particularly for C++ applications or services, lower-level control of the listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="a60a9-140">Listage vorace</span><span class="sxs-lookup"><span data-stu-id="a60a9-140">Greedy listing</span></span>
<span data-ttu-id="a60a9-141">Les versions antérieures de la bibliothèque cliente Storage pour C++ (versions 0.5.0 préliminaire et antérieures) comprenaient des API de listage non segmenté pour les tables et les files d'attente, comme dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a60a9-141">Earlier versions of the Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in the following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="a60a9-142">Ces méthodes étaient implémentées en tant que wrappers d'API segmentées.</span><span class="sxs-lookup"><span data-stu-id="a60a9-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="a60a9-143">À chaque réponse de listage segmenté, le code ajoutait les résultats à un vecteur et retournait tous les résultats après l’analyse complète des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a60a9-143">For each response of segmented listing, the code appended the results to a vector and returned all results after the full containers were scanned.</span></span>

<span data-ttu-id="a60a9-144">Autant cette approche pouvait fonctionner quand le compte de stockage ou la table contenait peu d'objets,</span><span class="sxs-lookup"><span data-stu-id="a60a9-144">This approach might work when the storage account or table contains a small number of objects.</span></span> <span data-ttu-id="a60a9-145">autant les besoins en mémoire pouvaient croître sans limite à mesure que le nombre d’objets augmentait, car tous les résultats restaient en mémoire.</span><span class="sxs-lookup"><span data-stu-id="a60a9-145">However, with an increase in the number of objects, the memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="a60a9-146">De plus, l'appelant ne disposait pas d'informations concernant la progression des opérations de listage, qui pouvaient prendre beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="a60a9-146">One listing operation can take a very long time, during which the caller had no information about its progress.</span></span>

<span data-ttu-id="a60a9-147">Ces API de listage, intégrées au Kit de développement logiciel (SDK), n'existent pas dans l'environnement C#, Java ou JavaScript Node.js.</span><span class="sxs-lookup"><span data-stu-id="a60a9-147">These greedy listing APIs in the SDK do not exist in C#, Java, or the JavaScript Node.js environment.</span></span> <span data-ttu-id="a60a9-148">Pour éviter les problèmes potentiels liés à l'utilisation de ces API voraces, nous les avons retirées de la version 0.6.0 préliminaire.</span><span class="sxs-lookup"><span data-stu-id="a60a9-148">To avoid the potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="a60a9-149">Si votre code appelle ces API voraces :</span><span class="sxs-lookup"><span data-stu-id="a60a9-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="a60a9-150">Vous avez tout intérêt à modifier votre code de façon à utiliser les API de listage segmenté :</span><span class="sxs-lookup"><span data-stu-id="a60a9-150">Then you should modify your code to use the segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="a60a9-151">En spécifiant le paramètre *max_results* du segment, vous pouvez établir un juste équilibre entre le nombre de demandes et l’utilisation de mémoire de façon à répondre à des considérations de performance pour votre application.</span><span class="sxs-lookup"><span data-stu-id="a60a9-151">By specifying the *max_results* parameter of the segment, you can balance between the numbers of requests and memory usage to meet performance considerations for your application.</span></span>

<span data-ttu-id="a60a9-152">Par ailleurs, si vous utilisez les API de listage segmenté, mais que vous stockez les données dans une collection locale, méthode qui s’avère « vorace », nous vous recommandons vivement de refactoriser votre code pour une gestion soigneuse et adaptée du stockage des données dans une collection locale.</span><span class="sxs-lookup"><span data-stu-id="a60a9-152">Additionally, if you're using segmented listing APIs, but store the data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code to handle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="a60a9-153">Listage paresseux</span><span class="sxs-lookup"><span data-stu-id="a60a9-153">Lazy listing</span></span>
<span data-ttu-id="a60a9-154">Même si le listage vorace peut poser des problèmes, il est utile s’il n’y a pas trop d’objets dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="a60a9-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in the container.</span></span>

<span data-ttu-id="a60a9-155">Si vous faites aussi appel à des SDK C# ou Oracle Java, vous devez connaître le modèle de programmation « énumérable », qui offre un mode de listage « paresseux », qui ne va chercher certaines données périphériques que s’il y est contraint.</span><span class="sxs-lookup"><span data-stu-id="a60a9-155">If you're also using C# or Oracle Java SDKs, you should be familiar with the Enumerable programming model, which offers a lazy-style listing, where the data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="a60a9-156">En C++, le modèle basé sur un itérateur offre une approche similaire.</span><span class="sxs-lookup"><span data-stu-id="a60a9-156">In C++, the iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="a60a9-157">Une API de listage paresseux type, utilisant **list_blobs** en guise d’exemple, se présente comme ceci :</span><span class="sxs-lookup"><span data-stu-id="a60a9-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="a60a9-158">Un extrait de code type qui utilise le modèle de listage paresseux peut se présenter comme ceci :</span><span class="sxs-lookup"><span data-stu-id="a60a9-158">A typical code snippet that uses the lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in the blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="a60a9-159">Notez que le listage paresseux est disponible uniquement en mode synchrone.</span><span class="sxs-lookup"><span data-stu-id="a60a9-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="a60a9-160">Par rapport au listage vorace, le listage paresseux ne va chercher les données qu’en cas de nécessité.</span><span class="sxs-lookup"><span data-stu-id="a60a9-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="a60a9-161">En réalité, il ne va chercher les données d’Azure Storage qu’à partir du moment où l'itérateur suivant se déplace dans le segment suivant.</span><span class="sxs-lookup"><span data-stu-id="a60a9-161">Under the covers, it fetches data from Azure Storage only when the next iterator moves into next segment.</span></span> <span data-ttu-id="a60a9-162">Par conséquent, l'utilisation de mémoire étant contrôlée et limitée par la taille, l'opération est rapide.</span><span class="sxs-lookup"><span data-stu-id="a60a9-162">Therefore, memory usage is controlled with a bounded size, and the operation is fast.</span></span>

<span data-ttu-id="a60a9-163">Les API de listage paresseux sont incluses dans la bibliothèque cliente Storage pour C++ de version 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="a60a9-163">Lazy listing APIs are included in the Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="a60a9-164">Conclusion</span><span class="sxs-lookup"><span data-stu-id="a60a9-164">Conclusion</span></span>
<span data-ttu-id="a60a9-165">Dans cet article, nous nous sommes intéressés à différentes surcharges pour API de listage pour divers objets de la bibliothèque cliente Storage pour C++.</span><span class="sxs-lookup"><span data-stu-id="a60a9-165">In this article, we discussed different overloads for listing APIs for various objects in the Storage Client Library for C++ .</span></span> <span data-ttu-id="a60a9-166">Pour résumer :</span><span class="sxs-lookup"><span data-stu-id="a60a9-166">To summarize:</span></span>

* <span data-ttu-id="a60a9-167">Les API asynchrones sont vivement recommandées dans divers scénarios de threading.</span><span class="sxs-lookup"><span data-stu-id="a60a9-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="a60a9-168">Le listage segmenté est recommandé dans la plupart des scénarios.</span><span class="sxs-lookup"><span data-stu-id="a60a9-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="a60a9-169">Le listage paresseux est fourni dans la bibliothèque sous forme de wrapper, qui s’avère pratique dans les scénarios synchrones.</span><span class="sxs-lookup"><span data-stu-id="a60a9-169">Lazy listing is provided in the library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="a60a9-170">Le listage vorace est déconseillé et a été retiré de la bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="a60a9-170">Greedy listing is not recommended and has been removed from the library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a60a9-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a60a9-171">Next steps</span></span>
<span data-ttu-id="a60a9-172">Pour plus d'informations sur Azure Storage et la bibliothèque cliente pour C++, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="a60a9-172">For more information about Azure Storage and Client Library for C++, see the following resources.</span></span>

* [<span data-ttu-id="a60a9-173">Utilisation du stockage d'objets blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="a60a9-173">How to use Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="a60a9-174">Utilisation du stockage de tables à partir de C++</span><span class="sxs-lookup"><span data-stu-id="a60a9-174">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="a60a9-175">Utilisation du service de stockage de files d'attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="a60a9-175">How to use Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="a60a9-176">Documentation sur les API de la bibliothèque cliente Azure Storage pour C++.</span><span class="sxs-lookup"><span data-stu-id="a60a9-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="a60a9-177">Blog de l'équipe Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a60a9-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="a60a9-178">Documentation d'Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a60a9-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

