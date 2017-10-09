---
title: "ressources de stockage Azure aaaList avec hello bibliothèque cliente de stockage pour C++ | Documents Microsoft"
description: "Découvrez comment hello toouse répertoriant les API dans la bibliothèque cliente de Microsoft Azure Storage pour les conteneurs tooenumerate C++, les objets BLOB, files d’attente, tables et des entités."
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
ms.openlocfilehash: a76a5ce3cd690f32914f8f0c1f64273f13c5063e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="963b2-103">Listage des ressources Azure Storage en C++</span><span class="sxs-lookup"><span data-stu-id="963b2-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="963b2-104">Opérations de liste sont les scénarios de développement clé réduire avec le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="963b2-104">Listing operations are key toomany development scenarios with Azure Storage.</span></span> <span data-ttu-id="963b2-105">Cet article décrit la façon dont le toomost efficacement pour énumérer les objets dans le stockage Azure à l’aide de hello répertoriant les API fournies dans hello bibliothèque cliente de Microsoft Azure Storage pour C++.</span><span class="sxs-lookup"><span data-stu-id="963b2-105">This article describes how toomost efficiently enumerate objects in Azure Storage using hello listing APIs provided in hello Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="963b2-106">Ce guide vise hello bibliothèque cliente Azure Storage pour C++ version 2.x, qui est disponible via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="963b2-106">This guide targets hello Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="963b2-107">Hello bibliothèque cliente de stockage fournit un éventail de toolist des méthodes ou des objets de requête dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="963b2-107">hello Storage Client Library provides a variety of methods toolist or query objects in Azure Storage.</span></span> <span data-ttu-id="963b2-108">Cet article traite hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="963b2-108">This article addresses hello following scenarios:</span></span>

* <span data-ttu-id="963b2-109">liste les conteneurs présents dans un compte ;</span><span class="sxs-lookup"><span data-stu-id="963b2-109">List containers in an account</span></span>
* <span data-ttu-id="963b2-110">lister les objets blob présents dans un conteneur ou un répertoire d'objets blob virtuel ;</span><span class="sxs-lookup"><span data-stu-id="963b2-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="963b2-111">lister les files d'attente contenues dans un compte ;</span><span class="sxs-lookup"><span data-stu-id="963b2-111">List queues in an account</span></span>
* <span data-ttu-id="963b2-112">lister les tables contenues dans un compte ;</span><span class="sxs-lookup"><span data-stu-id="963b2-112">List tables in an account</span></span>
* <span data-ttu-id="963b2-113">interroger les entités d’une table.</span><span class="sxs-lookup"><span data-stu-id="963b2-113">Query entities in a table</span></span>

<span data-ttu-id="963b2-114">Chacune de ces méthodes est présentée en utilisant différentes surcharges qui varient en fonction des scénarios.</span><span class="sxs-lookup"><span data-stu-id="963b2-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="963b2-115">Opérations asynchrones/synchrones</span><span class="sxs-lookup"><span data-stu-id="963b2-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="963b2-116">Étant donné que hello bibliothèque cliente de stockage pour C++ repose sur hello [bibliothèque de C++ reste](https://github.com/Microsoft/cpprestsdk), nous, par nature, prend en charge les opérations asynchrones à l’aide de [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="963b2-116">Because hello Storage Client Library for C++ is built on top of hello [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="963b2-117">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="963b2-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="963b2-118">Opérations synchrones encapsulent des opérations asynchrones de hello correspondante :</span><span class="sxs-lookup"><span data-stu-id="963b2-118">Synchronous operations wrap hello corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="963b2-119">Si vous travaillez avec plusieurs applications ou services de thread, nous recommandons d’utiliser hello async API directement au lieu de la création d’une synchronisation de hello toocall thread API, ce qui affecte considérablement les performances.</span><span class="sxs-lookup"><span data-stu-id="963b2-119">If you are working with multiple threading applications or services, we recommend that you use hello async APIs directly instead of creating a thread toocall hello sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="963b2-120">Listage segmenté</span><span class="sxs-lookup"><span data-stu-id="963b2-120">Segmented listing</span></span>
<span data-ttu-id="963b2-121">échelle de Hello de stockage cloud nécessite annonce segmenté.</span><span class="sxs-lookup"><span data-stu-id="963b2-121">hello scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="963b2-122">Par exemple, un conteneur d’objets blob Azure peut contenir plus d’un million d’objets blob et une table Azure plus d’un milliard d'entités.</span><span class="sxs-lookup"><span data-stu-id="963b2-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="963b2-123">Il ne s’agit pas là de chiffres théoriques, mais bien de cas d'utilisation réels de clients.</span><span class="sxs-lookup"><span data-stu-id="963b2-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="963b2-124">Il est donc difficile toolist tous les objets dans une seule réponse.</span><span class="sxs-lookup"><span data-stu-id="963b2-124">It is therefore impractical toolist all objects in a single response.</span></span> <span data-ttu-id="963b2-125">En revanche, il est possible de lister des objets en utilisant la pagination.</span><span class="sxs-lookup"><span data-stu-id="963b2-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="963b2-126">Chaque hello répertoriant les API a un *segmenté* de surcharge.</span><span class="sxs-lookup"><span data-stu-id="963b2-126">Each of hello listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="963b2-127">réponse Hello pour une opération de liste segmenté comprend :</span><span class="sxs-lookup"><span data-stu-id="963b2-127">hello response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="963b2-128"><i>_segment</i>, qui contient le jeu de hello de résultats retournés pour un toohello appel unique qui répertorie les API.</span><span class="sxs-lookup"><span data-stu-id="963b2-128"><i>_segment</i>, which contains hello set of results returned for a single call toohello listing API.</span></span>
* <span data-ttu-id="963b2-129">*continuation_token*, qui est transmis toohello prochain appel dans l’ordre tooget hello page de résultats suivante.</span><span class="sxs-lookup"><span data-stu-id="963b2-129">*continuation_token*, which is passed toohello next call in order tooget hello next page of results.</span></span> <span data-ttu-id="963b2-130">Lorsqu’il n’y a aucune tooreturn plus de résultats, le jeton de continuation hello est null.</span><span class="sxs-lookup"><span data-stu-id="963b2-130">When there are no more results tooreturn, hello continuation token is null.</span></span>

<span data-ttu-id="963b2-131">Par exemple, un appel typique de toolist tous les objets BLOB dans un conteneur peuvent ressembler à hello suivant extrait de code.</span><span class="sxs-lookup"><span data-stu-id="963b2-131">For example, a typical call toolist all blobs in a container may look like hello following code snippet.</span></span> <span data-ttu-id="963b2-132">code de Hello est disponible dans notre [exemples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="963b2-132">hello code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in hello blob container
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

<span data-ttu-id="963b2-133">Notez que hello de résultats retournés dans une page peuvent être contrôlés par le paramètre hello *max_results* dans surcharge hello de chaque API, par exemple :</span><span class="sxs-lookup"><span data-stu-id="963b2-133">Note that hello number of results returned in a page can be controlled by hello parameter *max_results* in hello overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="963b2-134">Si vous ne spécifiez pas hello *max_results* paramètre, la valeur maximale de too5000 résultats est retournée dans une seule page de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="963b2-134">If you do not specify hello *max_results* parameter, hello default maximum value of up too5000 results is returned in a single page.</span></span>

<span data-ttu-id="963b2-135">Notez également qu’une requête sur le stockage Azure Table peut-être retourner aucun enregistrement ou moins d’enregistrements que la valeur hello hello *max_results* paramètre que vous avez spécifié, même si le jeton de continuation hello n’est pas vide.</span><span class="sxs-lookup"><span data-stu-id="963b2-135">Also note that a query against Azure Table storage may return no records, or fewer records than hello value of hello *max_results* parameter that you specified, even if hello continuation token is not empty.</span></span> <span data-ttu-id="963b2-136">L’une des raisons peuvent être que cette requête hello ne pourrait pas terminée dans les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="963b2-136">One reason might be that hello query could not complete in five seconds.</span></span> <span data-ttu-id="963b2-137">Tant que jeton de continuation hello n’est pas vide, la requête hello doit continuer et votre code ne doit pas supposer taille de hello de segment de résultats.</span><span class="sxs-lookup"><span data-stu-id="963b2-137">As long as hello continuation token is not empty, hello query should continue, and your code should not assume hello size of segment results.</span></span>

<span data-ttu-id="963b2-138">Hello recommandé de modèle pour la plupart des scénarios de codage est segmentée répertoriant, qui fournit une progression explicite de la liste ou l’interrogation, et comment le service de hello répond tooeach demande.</span><span class="sxs-lookup"><span data-stu-id="963b2-138">hello recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how hello service responds tooeach request.</span></span> <span data-ttu-id="963b2-139">En particulier pour les applications C++ ou services, contrôle de niveau inférieur de hello répertoriant progression peut aider contrôle mémoire et performances.</span><span class="sxs-lookup"><span data-stu-id="963b2-139">Particularly for C++ applications or services, lower-level control of hello listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="963b2-140">Listage vorace</span><span class="sxs-lookup"><span data-stu-id="963b2-140">Greedy listing</span></span>
<span data-ttu-id="963b2-141">Les versions antérieures de hello bibliothèque cliente de stockage pour C++ (versions 0.5.0 afficher un aperçu et versions antérieures) inclus non segmenté annonce API pour les tables et les files d’attente, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="963b2-141">Earlier versions of hello Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in hello following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="963b2-142">Ces méthodes étaient implémentées en tant que wrappers d'API segmentées.</span><span class="sxs-lookup"><span data-stu-id="963b2-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="963b2-143">Pour chaque réponse de liste segmentée, code de hello ajouté le vecteur de tooa résultats hello et retourné tous les résultats une fois que les conteneurs complète hello ont été analysés.</span><span class="sxs-lookup"><span data-stu-id="963b2-143">For each response of segmented listing, hello code appended hello results tooa vector and returned all results after hello full containers were scanned.</span></span>

<span data-ttu-id="963b2-144">Cette approche peut fonctionner lorsque le compte de stockage hello ou une table contient un petit nombre d’objets.</span><span class="sxs-lookup"><span data-stu-id="963b2-144">This approach might work when hello storage account or table contains a small number of objects.</span></span> <span data-ttu-id="963b2-145">Toutefois, avec une augmentation du nombre hello d’objets, mémoire hello requise peut augmenter sans limite, étant donné que tous les résultats restant en mémoire.</span><span class="sxs-lookup"><span data-stu-id="963b2-145">However, with an increase in hello number of objects, hello memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="963b2-146">Une opération de liste peut prendre beaucoup de temps, pendant le hello appelant disposait d’aucune information sur sa progression.</span><span class="sxs-lookup"><span data-stu-id="963b2-146">One listing operation can take a very long time, during which hello caller had no information about its progress.</span></span>

<span data-ttu-id="963b2-147">Ces gourmand répertoriant les API Bonjour SDK n’existe en c#, Java, ou hello JavaScript Node.js environnement.</span><span class="sxs-lookup"><span data-stu-id="963b2-147">These greedy listing APIs in hello SDK do not exist in C#, Java, or hello JavaScript Node.js environment.</span></span> <span data-ttu-id="963b2-148">tooavoid hello des problèmes d’utilisation de ces API gourmand, nous avons supprimé les 0.6.0 la version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="963b2-148">tooavoid hello potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="963b2-149">Si votre code appelle ces API voraces :</span><span class="sxs-lookup"><span data-stu-id="963b2-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="963b2-150">Ensuite, vous devez modifier votre code toouse hello segmenté répertoriant les API :</span><span class="sxs-lookup"><span data-stu-id="963b2-150">Then you should modify your code toouse hello segmented listing APIs:</span></span>

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

<span data-ttu-id="963b2-151">En spécifiant hello *max_results* paramètre du segment de hello, vous pouvez équilibrer entre les nombres de hello de demandes et de la mémoire d’utilisation toomeet considérations sur les performances de votre application.</span><span class="sxs-lookup"><span data-stu-id="963b2-151">By specifying hello *max_results* parameter of hello segment, you can balance between hello numbers of requests and memory usage toomeet performance considerations for your application.</span></span>

<span data-ttu-id="963b2-152">En outre, si vous êtes à l’aide de la liste segmentée API, mais stocker des données de hello dans une collection locale dans un style « gourmande », également fortement recommandé que vous refactorisez votre toohandle code stockant les données dans une collection locale avec soin à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="963b2-152">Additionally, if you're using segmented listing APIs, but store hello data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code toohandle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="963b2-153">Listage paresseux</span><span class="sxs-lookup"><span data-stu-id="963b2-153">Lazy listing</span></span>
<span data-ttu-id="963b2-154">Liste gourmande déclenché les problèmes potentiels, mais il est pratique si il ne sont pas trop d’objets dans le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="963b2-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in hello container.</span></span>

<span data-ttu-id="963b2-155">Si vous utilisez également c# ou kits de développement logiciel Oracle Java, vous devez être familiarisé avec hello énumérable modèle de programmation, qui offre un style différée répertoriant, où hello les données d’un certain décalage sont uniquement extraites si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="963b2-155">If you're also using C# or Oracle Java SDKs, you should be familiar with hello Enumerable programming model, which offers a lazy-style listing, where hello data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="963b2-156">En C++, de modèle d’itérateur hello fournit également une approche similaire.</span><span class="sxs-lookup"><span data-stu-id="963b2-156">In C++, hello iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="963b2-157">Une API de listage paresseux type, utilisant **list_blobs** en guise d’exemple, se présente comme ceci :</span><span class="sxs-lookup"><span data-stu-id="963b2-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="963b2-158">Un extrait de code typique qui utilise un modèle de liste différée hello peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="963b2-158">A typical code snippet that uses hello lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in hello blob container
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

<span data-ttu-id="963b2-159">Notez que le listage paresseux est disponible uniquement en mode synchrone.</span><span class="sxs-lookup"><span data-stu-id="963b2-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="963b2-160">Par rapport au listage vorace, le listage paresseux ne va chercher les données qu’en cas de nécessité.</span><span class="sxs-lookup"><span data-stu-id="963b2-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="963b2-161">Dans les coulisses hello, il extrait les données depuis le stockage Azure lors de l’itérateur suivant de hello déplace dans le segment suivant.</span><span class="sxs-lookup"><span data-stu-id="963b2-161">Under hello covers, it fetches data from Azure Storage only when hello next iterator moves into next segment.</span></span> <span data-ttu-id="963b2-162">Par conséquent, l’utilisation de mémoire est contrôlée avec une taille limite, et l’opération hello est rapide.</span><span class="sxs-lookup"><span data-stu-id="963b2-162">Therefore, memory usage is controlled with a bounded size, and hello operation is fast.</span></span>

<span data-ttu-id="963b2-163">Liste différée API inclus dans hello bibliothèque cliente de stockage pour C++ dans version2.2.0.</span><span class="sxs-lookup"><span data-stu-id="963b2-163">Lazy listing APIs are included in hello Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="963b2-164">Conclusion</span><span class="sxs-lookup"><span data-stu-id="963b2-164">Conclusion</span></span>
<span data-ttu-id="963b2-165">Dans cet article, nous avons parlé des différentes surcharges pour répertorier les API pour différents objets dans la bibliothèque cliente de stockage de hello pour C++.</span><span class="sxs-lookup"><span data-stu-id="963b2-165">In this article, we discussed different overloads for listing APIs for various objects in hello Storage Client Library for C++ .</span></span> <span data-ttu-id="963b2-166">toosummarize :</span><span class="sxs-lookup"><span data-stu-id="963b2-166">toosummarize:</span></span>

* <span data-ttu-id="963b2-167">Les API asynchrones sont vivement recommandées dans divers scénarios de threading.</span><span class="sxs-lookup"><span data-stu-id="963b2-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="963b2-168">Le listage segmenté est recommandé dans la plupart des scénarios.</span><span class="sxs-lookup"><span data-stu-id="963b2-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="963b2-169">Liste de différé est fournie dans la bibliothèque de hello comme un wrapper pratique dans les scénarios synchrones.</span><span class="sxs-lookup"><span data-stu-id="963b2-169">Lazy listing is provided in hello library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="963b2-170">Annonce gourmand est déconseillé et a été supprimé de la bibliothèque de hello.</span><span class="sxs-lookup"><span data-stu-id="963b2-170">Greedy listing is not recommended and has been removed from hello library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="963b2-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="963b2-171">Next steps</span></span>
<span data-ttu-id="963b2-172">Pour plus d’informations sur le stockage Azure et la bibliothèque cliente pour C++, consultez hello suivant des ressources.</span><span class="sxs-lookup"><span data-stu-id="963b2-172">For more information about Azure Storage and Client Library for C++, see hello following resources.</span></span>

* [<span data-ttu-id="963b2-173">Comment toouse stockage d’objets Blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="963b2-173">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="963b2-174">Comment toouse le stockage de Table à partir de C++</span><span class="sxs-lookup"><span data-stu-id="963b2-174">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="963b2-175">Comment toouse stockage de file d’attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="963b2-175">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="963b2-176">Documentation sur les API de la bibliothèque cliente Azure Storage pour C++.</span><span class="sxs-lookup"><span data-stu-id="963b2-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="963b2-177">Blog de l'équipe Azure Storage</span><span class="sxs-lookup"><span data-stu-id="963b2-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="963b2-178">Documentation d'Azure Storage</span><span class="sxs-lookup"><span data-stu-id="963b2-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

