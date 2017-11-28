---
title: "Utilisation du stockage de tables Microsoft Azure avec le Kit de développement logiciel (SDK) WebJobs"
description: "Découvrez comment utiliser le stockage de tables Microsoft Azure avec le Kit de développement logiciel (SDK) WebJobs. Créez des tables, ajoutez des entités à des tables et lisez les tables existantes."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="c7112-104">Utilisation du stockage de tables Microsoft Azure avec le Kit de développement logiciel (SDK) WebJobs</span><span class="sxs-lookup"><span data-stu-id="c7112-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="c7112-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="c7112-105">Overview</span></span>
<span data-ttu-id="c7112-106">Ce guide fournit des exemples de code C# qui indiquent comment lire et écrire des tables de stockage Azure à l’aide du [Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="c7112-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="c7112-107">Ce guide suppose que vous savez [comment créer un projet WebJob dans Visual Studio avec des chaînes de connexion qui pointent vers votre compte de stockage](websites-dotnet-webjobs-sdk-get-started.md) ou [plusieurs comptes de stockage](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="c7112-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="c7112-108">Certains extraits de code illustrent l’attribut `Table` utilisé dans des fonctions [appelées manuellement](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), c’est-à-dire sans utiliser l’un des attributs de déclenchement.</span><span class="sxs-lookup"><span data-stu-id="c7112-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <span data-ttu-id="c7112-109"><a id="ingress"></a> Ajout d’une entité à une table</span><span class="sxs-lookup"><span data-stu-id="c7112-109"><a id="ingress"></a> How to add entities to a table</span></span>
<span data-ttu-id="c7112-110">Pour ajouter des entités à une table, utilisez l’attribut `Table` avec un paramètre `ICollector<T>` ou `IAsyncCollector<T>`, dans lequel `T` spécifie le schéma des entités que vous souhaitez ajouter.</span><span class="sxs-lookup"><span data-stu-id="c7112-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="c7112-111">Le constructeur d’attribut prend un paramètre de chaîne qui spécifie le nom de la table.</span><span class="sxs-lookup"><span data-stu-id="c7112-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="c7112-112">L'exemple de code suivant ajoute `Person` entités à une table nommée *Entrée*.</span><span class="sxs-lookup"><span data-stu-id="c7112-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="c7112-113">En général, le type que vous utilisez avec `ICollector` dérive de l’élément `TableEntity` ou implémente `ITableEntity`, mais ce n’est pas obligatoire.</span><span class="sxs-lookup"><span data-stu-id="c7112-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="c7112-114">L’une ou l’autre des classes `Person` suivantes fonctionne avec le code indiqué dans la méthode `Ingress` précédente.</span><span class="sxs-lookup"><span data-stu-id="c7112-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

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

<span data-ttu-id="c7112-115">Si vous souhaitez utiliser directement l’API Microsoft Azure Storage, vous pouvez ajouter un paramètre `CloudStorageAccount` à la signature de méthode.</span><span class="sxs-lookup"><span data-stu-id="c7112-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <span data-ttu-id="c7112-116"><a id="monitor"></a> Surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="c7112-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="c7112-117">Étant donné que les fonctions d’entrée de données traitent souvent des volumes importants de données, le tableau de bord du Kit de développement logiciel (SDK) WebJobs fournit des données d’analyse en temps réel.</span><span class="sxs-lookup"><span data-stu-id="c7112-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="c7112-118">La section **Journal d’appels** vous signale si la fonction est toujours en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c7112-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![Fonction d’entrée en cours d’exécution](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="c7112-120">La page **Détails des appels** signale la progression de la fonction (c’est-à-dire le nombre d’entités écrites) alors qu’elle s’exécute et vous permet de l’arrêter.</span><span class="sxs-lookup"><span data-stu-id="c7112-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![Fonction d’entrée en cours d’exécution](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="c7112-122">Lorsque l’exécution de la fonction se termine, la page **Détails des appels** indique le nombre de lignes écrites.</span><span class="sxs-lookup"><span data-stu-id="c7112-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Arrêt de la fonction d’entrée](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="c7112-124"><a id="multiple"></a> Lecture de plusieurs entrées à partir d’une table</span><span class="sxs-lookup"><span data-stu-id="c7112-124"><a id="multiple"></a> How to read multiple entities from a table</span></span>
<span data-ttu-id="c7112-125">Pour lire une table, utilisez l’attribut `Table` avec un paramètre `IQueryable<T>`, dans lequel le type `T` dérive de `TableEntity` ou implémente `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="c7112-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="c7112-126">L’exemple de code suivant lit et enregistre toutes les lignes de la table `Ingress` :</span><span class="sxs-lookup"><span data-stu-id="c7112-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

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

### <span data-ttu-id="c7112-127"><a id="readone"></a> Lecture d’une entité unique à partir d’une table</span><span class="sxs-lookup"><span data-stu-id="c7112-127"><a id="readone"></a> How to read a single entity from a table</span></span>
<span data-ttu-id="c7112-128">Il existe un constructeur d’attribut `Table` présentant deux paramètres supplémentaires, qui vous permettent de spécifier la clé de partition et la clé de ligne lorsque vous souhaitez effectuer une liaison avec une entité de table unique.</span><span class="sxs-lookup"><span data-stu-id="c7112-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="c7112-129">L’exemple de code suivant lit une ligne de table pour une entité `Person` basée sur des valeurs de clé de partition et de clé de ligne reçues dans un message en file d’attente :</span><span class="sxs-lookup"><span data-stu-id="c7112-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="c7112-130">La classe `Person` figurant dans cet exemple n’est pas obligée d’implémenter `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="c7112-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <span data-ttu-id="c7112-131"><a id="storageapi"></a> Utilisation directe de l’API de stockage .NET pour travailler avec une table</span><span class="sxs-lookup"><span data-stu-id="c7112-131"><a id="storageapi"></a> How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="c7112-132">Vous pouvez également utiliser l’attribut `Table` avec un objet `CloudTable`, afin de garantir une utilisation plus souple des tables.</span><span class="sxs-lookup"><span data-stu-id="c7112-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="c7112-133">L’exemple de code suivant utilise un objet `CloudTable` pour ajouter une entité unique à la table *Entrée* .</span><span class="sxs-lookup"><span data-stu-id="c7112-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

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

<span data-ttu-id="c7112-134">Pour en savoir plus sur l’utilisation de l’objet `CloudTable` , voir [Utilisation du stockage de tables à partir de .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c7112-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="c7112-135"><a id="queues"></a>Sujets connexes traités dans l’article de procédure relatif aux files d’attente</span><span class="sxs-lookup"><span data-stu-id="c7112-135"><a id="queues"></a>Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="c7112-136">Pour en savoir plus sur la gestion du traitement de tables déclenché par un message en file d’attente, ou pour consulter des scénarios relatifs au Kit de développement logiciel (SDK) WebJobs non spécifiques du traitement des tables, voir [Comment utiliser le stockage de la file d’attente Azure avec le Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="c7112-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="c7112-137">Les sujets abordés dans cet article sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="c7112-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="c7112-138">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="c7112-138">Async functions</span></span>
* <span data-ttu-id="c7112-139">Instances multiples</span><span class="sxs-lookup"><span data-stu-id="c7112-139">Multiple instances</span></span>
* <span data-ttu-id="c7112-140">Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="c7112-140">Graceful shutdown</span></span>
* <span data-ttu-id="c7112-141">Utilisation des attributs du Kit de développement logiciel (SDK) WebJobs dans le corps d’une fonction</span><span class="sxs-lookup"><span data-stu-id="c7112-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="c7112-142">Définition des chaînes de connexion du SDK dans le code</span><span class="sxs-lookup"><span data-stu-id="c7112-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="c7112-143">Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="c7112-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="c7112-144">Déclenchement manuel d’une fonction</span><span class="sxs-lookup"><span data-stu-id="c7112-144">Trigger a function manually</span></span>
* <span data-ttu-id="c7112-145">Écriture de journaux</span><span class="sxs-lookup"><span data-stu-id="c7112-145">Write logs</span></span>

## <span data-ttu-id="c7112-146"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7112-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="c7112-147">Ce guide fournit des exemples de code qui indiquent comment gérer des scénarios courants pour l’utilisation des tables Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c7112-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="c7112-148">Pour plus d’informations sur l’utilisation d’Azure Webjobs et du Kit de développement logiciel (SDK) WebJobs Azure, consultez la rubrique [Azure Webjobs - Ressources recommandées](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="c7112-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

