---
title: "Prise en main du stockage Azure et des services connectés Visual Studio (projets WebJob)"
description: "Comment prendre en main le stockage de tables Azure dans un projet WebJobs Azure dans Visual Studio après s'être connecté à un compte de stockage à l'aide des services connectés de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 0bf51f9113c45c747cd4fd3f76bdabd4a4c1f8e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="f5068-103">Prise en main d’Azure Storage (projets de tâche web Azure)</span><span class="sxs-lookup"><span data-stu-id="f5068-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="f5068-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f5068-104">Overview</span></span>
<span data-ttu-id="f5068-105">Cet article fournit des exemples de code C# qui montrent comment utiliser la version 1.x du Kit de développement logiciel (SDK) WebJobs Azure avec le service de stockage de tables Azure.</span><span class="sxs-lookup"><span data-stu-id="f5068-105">This article provides C# code samples that show show how to use the Azure WebJobs SDK version 1.x with the Azure table storage service.</span></span> <span data-ttu-id="f5068-106">Les exemples de code utilisent le [Kit de développement logiciel (SDK) WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="f5068-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="f5068-107">Le service de stockage de tables Azure vous permet de stocker de grandes quantités de données structurées.</span><span class="sxs-lookup"><span data-stu-id="f5068-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="f5068-108">Il s'agit d'une banque de données NoSQL qui accepte les appels authentifiés provenant de l'intérieur et de l'extérieur du cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="f5068-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="f5068-109">Les tables Azure sont idéales pour le stockage des données structurées non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="f5068-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="f5068-110">Pour plus d’informations, consultez la section [Prise en main d’Azure Table Storage à l’aide de .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) .</span><span class="sxs-lookup"><span data-stu-id="f5068-110">See [Get started with Azure Table storage using .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) for more information.</span></span>

<span data-ttu-id="f5068-111">Certains extraits de code illustrent l’attribut **Table** utilisé dans des fonctions appelées manuellement, c’est-à-dire sans utiliser l’un des attributs de déclenchement.</span><span class="sxs-lookup"><span data-stu-id="f5068-111">Some of the code snippets show the **Table** attribute used in functions that are called manually, that is, not by using one of the trigger attributes.</span></span>

## <a name="how-to-add-entities-to-a-table"></a><span data-ttu-id="f5068-112">Ajout d’une entité à une table</span><span class="sxs-lookup"><span data-stu-id="f5068-112">How to add entities to a table</span></span>
<span data-ttu-id="f5068-113">Pour ajouter des entités à une table, utilisez l’attribut **Table** avec un paramètre **ICollector<T>** ou **IAsyncCollector<T>**, où **T** spécifie le schéma des entités que vous souhaitez ajouter.</span><span class="sxs-lookup"><span data-stu-id="f5068-113">To add entities to a table, use the **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="f5068-114">Le constructeur d’attribut prend un paramètre de chaîne qui spécifie le nom de la table.</span><span class="sxs-lookup"><span data-stu-id="f5068-114">The attribute constructor takes a string parameter that specifies the name of the table.</span></span>

<span data-ttu-id="f5068-115">L’exemple de code suivant ajoute des entités **Person** à une table nommée *Ingress*.</span><span class="sxs-lookup"><span data-stu-id="f5068-115">The following code sample adds **Person** entities to a table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() {
                        PartitionKey = "Test",
                        RowKey = i.ToString(),
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="f5068-116">En général, le type que vous utilisez avec **ICollector** est dérivé de **TableEntity** ou implémente **ITableEntity**, mais pas nécessairement.</span><span class="sxs-lookup"><span data-stu-id="f5068-116">Typically the type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="f5068-117">Les deux classes **Person** suivantes fonctionnent avec le code indiqué dans la méthode **Ingress** précédente.</span><span class="sxs-lookup"><span data-stu-id="f5068-117">Either of the following **Person** classes work with the code shown in the preceding **Ingress** method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="f5068-118">Si vous souhaitez utiliser directement l’API Azure Storage, vous pouvez ajouter un paramètre **CloudStorageAccount** à la signature de méthode.</span><span class="sxs-lookup"><span data-stu-id="f5068-118">If you want to work directly with the Azure storage API, you can add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="f5068-119">Surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="f5068-119">Real-time monitoring</span></span>
<span data-ttu-id="f5068-120">Étant donné que les fonctions d’entrée de données traitent souvent des volumes importants de données, le tableau de bord du Kit de développement logiciel (SDK) WebJobs fournit des données d’analyse en temps réel.</span><span class="sxs-lookup"><span data-stu-id="f5068-120">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="f5068-121">La section **Journal d’appels** vous signale si la fonction est toujours en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f5068-121">The **Invocation Log** section tells you if the function is still running.</span></span>

![Fonction d’entrée en cours d’exécution](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="f5068-123">La page **Détails des appels** signale la progression de la fonction (c’est-à-dire le nombre d’entités écrites) alors qu’elle s’exécute et vous permet de l’arrêter.</span><span class="sxs-lookup"><span data-stu-id="f5068-123">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span>

![Fonction d’entrée en cours d’exécution](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="f5068-125">Lorsque l’exécution de la fonction se termine, la page **Détails des appels** indique le nombre de lignes écrites.</span><span class="sxs-lookup"><span data-stu-id="f5068-125">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Arrêt de la fonction d’entrée](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-to-read-multiple-entities-from-a-table"></a><span data-ttu-id="f5068-127">Lecture de plusieurs entrées à partir d’une table</span><span class="sxs-lookup"><span data-stu-id="f5068-127">How to read multiple entities from a table</span></span>
<span data-ttu-id="f5068-128">Pour lire une table, utilisez l’attribut **Table** avec un paramètre **IQueryable<T>** où le type **T** est dérivé de **TableEntity** ou implémente **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="f5068-128">To read a table, use the **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="f5068-129">L’exemple de code suivant lit et enregistre toutes les lignes de la table **Ingress** :</span><span class="sxs-lookup"><span data-stu-id="f5068-129">The following code sample reads and logs all rows from the **Ingress** table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}",
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <a name="how-to-read-a-single-entity-from-a-table"></a><span data-ttu-id="f5068-130">Lecture d’une entité unique à partir d’une table</span><span class="sxs-lookup"><span data-stu-id="f5068-130">How to read a single entity from a table</span></span>
<span data-ttu-id="f5068-131">Il existe un constructeur d’attribut **Table** présentant deux paramètres supplémentaires, qui vous permettent de spécifier la clé de partition et la clé de ligne lorsque vous souhaitez effectuer une liaison avec une entité de table unique.</span><span class="sxs-lookup"><span data-stu-id="f5068-131">There is a **Table** attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="f5068-132">L’exemple de code suivant lit une ligne de table pour une entité **Person** basée sur des valeurs de clé de partition et de clé de ligne reçues dans un message en file d’attente :</span><span class="sxs-lookup"><span data-stu-id="f5068-132">The following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="f5068-133">La classe **Person** figurant dans cet exemple n’est pas obligée d’implémenter **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="f5068-133">The **Person** class in this example does not have to implement **ITableEntity**.</span></span>

## <a name="how-to-use-the-net-storage-api-directly-to-work-with-a-table"></a><span data-ttu-id="f5068-134">Utilisation directe de l’API de stockage .NET pour travailler avec une table</span><span class="sxs-lookup"><span data-stu-id="f5068-134">How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="f5068-135">Vous pouvez également utiliser l’attribut **Table** avec un objet **CloudTable**, afin de garantir une utilisation plus souple des tables.</span><span class="sxs-lookup"><span data-stu-id="f5068-135">You can also use the **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="f5068-136">L’exemple de code suivant utilise un objet **CloudTable** pour ajouter une entité unique à la table *Ingress* .</span><span class="sxs-lookup"><span data-stu-id="f5068-136">The following code sample uses a **CloudTable** object to add a single entity to the *Ingress* table.</span></span>

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="f5068-137">Pour en savoir plus sur l’utilisation de l’objet **CloudTable** , consultez la section [Prise en main d’Azure Table Storage à l’aide de .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="f5068-137">For more information about how to use the **CloudTable** object, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-the-queues-how-to-article"></a><span data-ttu-id="f5068-138">Sujets connexes traités dans l’article de procédure relatif aux files d’attente</span><span class="sxs-lookup"><span data-stu-id="f5068-138">Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="f5068-139">Pour en savoir plus sur la gestion du traitement de tables déclenché par un message en file d’attente, ou pour consulter des scénarios relatifs au Kit de développement logiciel (SDK) WebJobs non spécifiques du traitement des tables, consultez la section [Prise en main d’Azure Queue Storage et des services connectés Visual Studio (projets WebJobs)](../storage/vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="f5068-139">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](../storage/vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5068-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f5068-140">Next steps</span></span>
<span data-ttu-id="f5068-141">Cet article a fourni des exemples de code qui montrent comment gérer des scénarios courants pour l’utilisation des tables Azure.</span><span class="sxs-lookup"><span data-stu-id="f5068-141">This article has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="f5068-142">Pour plus d’informations sur l’utilisation d’Azure WebJobs et du Kit de développement logiciel (SDK) WebJobs, consultez la section [Ressources de documentation Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="f5068-142">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

