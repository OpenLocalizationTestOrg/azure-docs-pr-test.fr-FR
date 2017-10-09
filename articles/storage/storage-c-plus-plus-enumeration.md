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
ms.openlocfilehash: d20a86688938704c24339aa9a1145786783fea5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a>Listage des ressources Azure Storage en C++
Opérations de liste sont les scénarios de développement clé réduire avec le stockage Azure. Cet article décrit la façon dont le toomost efficacement pour énumérer les objets dans le stockage Azure à l’aide de hello répertoriant les API fournies dans hello bibliothèque cliente de Microsoft Azure Storage pour C++.

> [!NOTE]
> Ce guide vise hello bibliothèque cliente Azure Storage pour C++ version 2.x, qui est disponible via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

Hello bibliothèque cliente de stockage fournit un éventail de toolist des méthodes ou des objets de requête dans le stockage Azure. Cet article traite hello les scénarios suivants :

* liste les conteneurs présents dans un compte ;
* lister les objets blob présents dans un conteneur ou un répertoire d'objets blob virtuel ;
* lister les files d'attente contenues dans un compte ;
* lister les tables contenues dans un compte ;
* interroger les entités d’une table.

Chacune de ces méthodes est présentée en utilisant différentes surcharges qui varient en fonction des scénarios.

## <a name="asynchronous-versus-synchronous"></a>Opérations asynchrones/synchrones
Étant donné que hello bibliothèque cliente de stockage pour C++ repose sur hello [bibliothèque de C++ reste](https://github.com/Microsoft/cpprestsdk), nous, par nature, prend en charge les opérations asynchrones à l’aide de [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html). Par exemple :

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

Opérations synchrones encapsulent des opérations asynchrones de hello correspondante :

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

Si vous travaillez avec plusieurs applications ou services de thread, nous recommandons d’utiliser hello async API directement au lieu de la création d’une synchronisation de hello toocall thread API, ce qui affecte considérablement les performances.

## <a name="segmented-listing"></a>Listage segmenté
échelle de Hello de stockage cloud nécessite annonce segmenté. Par exemple, un conteneur d’objets blob Azure peut contenir plus d’un million d’objets blob et une table Azure plus d’un milliard d'entités. Il ne s’agit pas là de chiffres théoriques, mais bien de cas d'utilisation réels de clients.

Il est donc difficile toolist tous les objets dans une seule réponse. En revanche, il est possible de lister des objets en utilisant la pagination. Chaque hello répertoriant les API a un *segmenté* de surcharge.

réponse Hello pour une opération de liste segmenté comprend :

* <i>_segment</i>, qui contient le jeu de hello de résultats retournés pour un toohello appel unique qui répertorie les API.
* *continuation_token*, qui est transmis toohello prochain appel dans l’ordre tooget hello page de résultats suivante. Lorsqu’il n’y a aucune tooreturn plus de résultats, le jeton de continuation hello est null.

Par exemple, un appel typique de toolist tous les objets BLOB dans un conteneur peuvent ressembler à hello suivant extrait de code. code de Hello est disponible dans notre [exemples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

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

Notez que hello de résultats retournés dans une page peuvent être contrôlés par le paramètre hello *max_results* dans surcharge hello de chaque API, par exemple :

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

Si vous ne spécifiez pas hello *max_results* paramètre, la valeur maximale de too5000 résultats est retournée dans une seule page de la valeur par défaut hello.

Notez également qu’une requête sur le stockage Azure Table peut-être retourner aucun enregistrement ou moins d’enregistrements que la valeur hello hello *max_results* paramètre que vous avez spécifié, même si le jeton de continuation hello n’est pas vide. L’une des raisons peuvent être que cette requête hello ne pourrait pas terminée dans les cinq secondes. Tant que jeton de continuation hello n’est pas vide, la requête hello doit continuer et votre code ne doit pas supposer taille de hello de segment de résultats.

Hello recommandé de modèle pour la plupart des scénarios de codage est segmentée répertoriant, qui fournit une progression explicite de la liste ou l’interrogation, et comment le service de hello répond tooeach demande. En particulier pour les applications C++ ou services, contrôle de niveau inférieur de hello répertoriant progression peut aider contrôle mémoire et performances.

## <a name="greedy-listing"></a>Listage vorace
Les versions antérieures de hello bibliothèque cliente de stockage pour C++ (versions 0.5.0 afficher un aperçu et versions antérieures) inclus non segmenté annonce API pour les tables et les files d’attente, comme dans hello l’exemple suivant :

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

Ces méthodes étaient implémentées en tant que wrappers d'API segmentées. Pour chaque réponse de liste segmentée, code de hello ajouté le vecteur de tooa résultats hello et retourné tous les résultats une fois que les conteneurs complète hello ont été analysés.

Cette approche peut fonctionner lorsque le compte de stockage hello ou une table contient un petit nombre d’objets. Toutefois, avec une augmentation du nombre hello d’objets, mémoire hello requise peut augmenter sans limite, étant donné que tous les résultats restant en mémoire. Une opération de liste peut prendre beaucoup de temps, pendant le hello appelant disposait d’aucune information sur sa progression.

Ces gourmand répertoriant les API Bonjour SDK n’existe en c#, Java, ou hello JavaScript Node.js environnement. tooavoid hello des problèmes d’utilisation de ces API gourmand, nous avons supprimé les 0.6.0 la version préliminaire.

Si votre code appelle ces API voraces :

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

Ensuite, vous devez modifier votre code toouse hello segmenté répertoriant les API :

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

En spécifiant hello *max_results* paramètre du segment de hello, vous pouvez équilibrer entre les nombres de hello de demandes et de la mémoire d’utilisation toomeet considérations sur les performances de votre application.

En outre, si vous êtes à l’aide de la liste segmentée API, mais stocker des données de hello dans une collection locale dans un style « gourmande », également fortement recommandé que vous refactorisez votre toohandle code stockant les données dans une collection locale avec soin à grande échelle.

## <a name="lazy-listing"></a>Listage paresseux
Liste gourmande déclenché les problèmes potentiels, mais il est pratique si il ne sont pas trop d’objets dans le conteneur de hello.

Si vous utilisez également c# ou kits de développement logiciel Oracle Java, vous devez être familiarisé avec hello énumérable modèle de programmation, qui offre un style différée répertoriant, où hello les données d’un certain décalage sont uniquement extraites si nécessaire. En C++, de modèle d’itérateur hello fournit également une approche similaire.

Une API de listage paresseux type, utilisant **list_blobs** en guise d’exemple, se présente comme ceci :

```cpp
list_blob_item_iterator list_blobs() const;
```

Un extrait de code typique qui utilise un modèle de liste différée hello peut ressembler à ceci :

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

Notez que le listage paresseux est disponible uniquement en mode synchrone.

Par rapport au listage vorace, le listage paresseux ne va chercher les données qu’en cas de nécessité. Dans les coulisses hello, il extrait les données depuis le stockage Azure lors de l’itérateur suivant de hello déplace dans le segment suivant. Par conséquent, l’utilisation de mémoire est contrôlée avec une taille limite, et l’opération hello est rapide.

Liste différée API inclus dans hello bibliothèque cliente de stockage pour C++ dans version2.2.0.

## <a name="conclusion"></a>Conclusion
Dans cet article, nous avons parlé des différentes surcharges pour répertorier les API pour différents objets dans la bibliothèque cliente de stockage de hello pour C++. toosummarize :

* Les API asynchrones sont vivement recommandées dans divers scénarios de threading.
* Le listage segmenté est recommandé dans la plupart des scénarios.
* Liste de différé est fournie dans la bibliothèque de hello comme un wrapper pratique dans les scénarios synchrones.
* Annonce gourmand est déconseillé et a été supprimé de la bibliothèque de hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le stockage Azure et la bibliothèque cliente pour C++, consultez hello suivant des ressources.

* [Comment toouse stockage d’objets Blob à partir de C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Comment toouse le stockage de Table à partir de C++](storage-c-plus-plus-how-to-use-tables.md)
* [Comment toouse stockage de file d’attente à partir de C++](storage-c-plus-plus-how-to-use-queues.md)
* [Documentation sur les API de la bibliothèque cliente Azure Storage pour C++.](http://azure.github.io/azure-storage-cpp/)
* [Blog de l'équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)
* [Documentation d'Azure Storage](https://azure.microsoft.com/documentation/services/storage/)

