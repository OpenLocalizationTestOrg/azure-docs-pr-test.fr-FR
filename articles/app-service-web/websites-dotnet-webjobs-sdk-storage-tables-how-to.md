---
title: aaaHow toouse stockage de tables Azure avec hello WebJobs SDK
description: "Découvrez comment toouse Azure table storage avec hello WebJobs SDK. Créer des tables, ajouter des entités tootables et lire des tables existantes."
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
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="28e6a-104">Comment toouse Azure table storage avec hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="28e6a-104">How toouse Azure table storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="28e6a-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="28e6a-105">Overview</span></span>
<span data-ttu-id="28e6a-106">Ce guide fournit des exemples de code c# qui montrent comment les tables tooread et écriture de stockage Azure à l’aide de [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="28e6a-106">This guide provides C# code samples that show how tooread and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="28e6a-107">guide de Hello suppose que vous connaissez [comment toocreate un projet de la tâche Web dans Visual Studio avec connexion chaînes ce compte de stockage point tooyour](websites-dotnet-webjobs-sdk-get-started.md) ou trop[plusieurs comptes de stockage](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="28e6a-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="28e6a-108">Certains des extraits de code hello affichent hello `Table` attribut utilisé dans les fonctions qui sont [appelée manuellement](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), autrement dit, ne pas à l’aide d’un des attributs de déclencheur hello.</span><span class="sxs-lookup"><span data-stu-id="28e6a-108">Some of hello code snippets show hello `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of hello trigger attributes.</span></span> 

## <span data-ttu-id="28e6a-109"><a id="ingress"></a>La table de tooa tooadd entités</span><span class="sxs-lookup"><span data-stu-id="28e6a-109"><a id="ingress"></a> How tooadd entities tooa table</span></span>
<span data-ttu-id="28e6a-110">table de tooa tooadd entités, utilisez hello `Table` d’attribut avec une `ICollector<T>` ou `IAsyncCollector<T>` paramètre où `T` Spécifie le schéma de hello d’entités de hello souhaité tooadd.</span><span class="sxs-lookup"><span data-stu-id="28e6a-110">tooadd entities tooa table, use hello `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="28e6a-111">constructeur d’attribut Hello prend un paramètre de chaîne indiquant le nom de la table de hello hello.</span><span class="sxs-lookup"><span data-stu-id="28e6a-111">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span> 

<span data-ttu-id="28e6a-112">Hello exemple de code suivant ajoute `Person` table de tooa d’entités nommée *entrée*.</span><span class="sxs-lookup"><span data-stu-id="28e6a-112">hello following code sample adds `Person` entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="28e6a-113">En général, hello type que vous utilisez avec `ICollector` dérive `TableEntity` ou implémente `ITableEntity`, mais il ne doit pas nécessairement.</span><span class="sxs-lookup"><span data-stu-id="28e6a-113">Typically hello type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="28e6a-114">Un des éléments suivants de hello `Person` classes de travail avec code hello illustré hello précédent `Ingress` (méthode).</span><span class="sxs-lookup"><span data-stu-id="28e6a-114">Either of hello following `Person` classes work with hello code shown in hello preceding `Ingress` method.</span></span>

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

<span data-ttu-id="28e6a-115">Si vous souhaitez toowork directement avec hello API de stockage Azure, vous pouvez ajouter un `CloudStorageAccount` la signature de méthode toohello paramètre.</span><span class="sxs-lookup"><span data-stu-id="28e6a-115">If you want toowork directly with hello Azure storage API, you can add a `CloudStorageAccount` parameter toohello method signature.</span></span>

## <span data-ttu-id="28e6a-116"><a id="monitor"></a> Surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="28e6a-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="28e6a-117">Étant donné que les fonctions d’entrée de données traitent souvent des volumes importants de données, hello du tableau de bord WebJobs SDK fournit des données d’analyse en temps réel.</span><span class="sxs-lookup"><span data-stu-id="28e6a-117">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="28e6a-118">Hello **Invocation journal** section vous indique si la fonction de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="28e6a-118">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Fonction d’entrée en cours d’exécution](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="28e6a-120">Hello **détails de l’appel** page Rapports hello la progression de la fonction (nombre d’entités écrites) pendant qu’il est en cours d’exécution et vous donne une occasion tooabort il.</span><span class="sxs-lookup"><span data-stu-id="28e6a-120">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span> 

![Fonction d’entrée en cours d’exécution](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="28e6a-122">Lorsque fonction hello se termine, hello **détails de l’appel** page signale le nombre de hello de lignes écrites.</span><span class="sxs-lookup"><span data-stu-id="28e6a-122">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Arrêt de la fonction d’entrée](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="28e6a-124"><a id="multiple"></a>Comment tooread plusieurs entités à partir d’une table</span><span class="sxs-lookup"><span data-stu-id="28e6a-124"><a id="multiple"></a> How tooread multiple entities from a table</span></span>
<span data-ttu-id="28e6a-125">tooread une table, utilisez hello `Table` d’attribut avec une `IQueryable<T>` paramètre où taper `T` dérive `TableEntity` ou implémente `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="28e6a-125">tooread a table, use hello `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="28e6a-126">Hello exemple de code suivant lit et des journaux de toutes les lignes à partir de hello `Ingress` table :</span><span class="sxs-lookup"><span data-stu-id="28e6a-126">hello following code sample reads and logs all rows from hello `Ingress` table:</span></span>

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

### <span data-ttu-id="28e6a-127"><a id="readone"></a>Comment tooread une seule entité à partir d’une table</span><span class="sxs-lookup"><span data-stu-id="28e6a-127"><a id="readone"></a> How tooread a single entity from a table</span></span>
<span data-ttu-id="28e6a-128">Il existe un `Table` constructeur d’attribut avec deux paramètres supplémentaires qui vous permettent de spécifier la clé de partition hello et clé de ligne lorsque vous souhaitez que les entités de table unique toobind tooa.</span><span class="sxs-lookup"><span data-stu-id="28e6a-128">There is a `Table` attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="28e6a-129">Hello exemple de code suivant lit une ligne de table pour une `Person` entité en fonction de partition clé et la ligne de valeurs de clé a reçu un message de la file d’attente :</span><span class="sxs-lookup"><span data-stu-id="28e6a-129">hello following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="28e6a-130">Hello `Person` classe dans cet exemple n’a pas de tooimplement `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="28e6a-130">hello `Person` class in this example does not have tooimplement `ITableEntity`.</span></span>

## <span data-ttu-id="28e6a-131"><a id="storageapi"></a>Comment toouse hello API de stockage .NET directement toowork avec une table</span><span class="sxs-lookup"><span data-stu-id="28e6a-131"><a id="storageapi"></a> How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="28e6a-132">Vous pouvez également utiliser hello `Table` d’attribut avec un `CloudTable` objet pour une plus grande souplesse de l’utilisation d’une table.</span><span class="sxs-lookup"><span data-stu-id="28e6a-132">You can also use hello `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="28e6a-133">exemple de code suivant de Hello un `CloudTable` tooadd un toohello d’entité unique de l’objet *entrée* table.</span><span class="sxs-lookup"><span data-stu-id="28e6a-133">hello following code sample uses a `CloudTable` object tooadd a single entity toohello *Ingress* table.</span></span> 

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

<span data-ttu-id="28e6a-134">Pour plus d’informations sur la façon toouse hello `CloudTable` d’objets, consultez [comment toouse le stockage de Table à partir de .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="28e6a-134">For more information about how toouse hello `CloudTable` object, see [How toouse Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="28e6a-135"><a id="queues"></a>Rubriques connexes couvertes par les files d’attente de hello procédure-tooarticle</span><span class="sxs-lookup"><span data-stu-id="28e6a-135"><a id="queues"></a>Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="28e6a-136">Pour plus d’informations sur la façon dont le traitement de table toohandle déclenché par un message de la file d’attente, ou pour les tâches Web scénarios du Kit de développement logiciel pas le traitement, consultez spécifiques tootable [comment toouse Azure file d’attente de stockage avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="28e6a-136">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="28e6a-137">Les sujets abordés dans cet article hello suivants :</span><span class="sxs-lookup"><span data-stu-id="28e6a-137">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="28e6a-138">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="28e6a-138">Async functions</span></span>
* <span data-ttu-id="28e6a-139">Instances multiples</span><span class="sxs-lookup"><span data-stu-id="28e6a-139">Multiple instances</span></span>
* <span data-ttu-id="28e6a-140">Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="28e6a-140">Graceful shutdown</span></span>
* <span data-ttu-id="28e6a-141">Utiliser les attributs de WebJobs SDK dans le corps d’une fonction de hello</span><span class="sxs-lookup"><span data-stu-id="28e6a-141">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="28e6a-142">Définir des chaînes de connexion du Kit de développement logiciel hello dans le code</span><span class="sxs-lookup"><span data-stu-id="28e6a-142">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="28e6a-143">Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="28e6a-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="28e6a-144">Déclenchement manuel d’une fonction</span><span class="sxs-lookup"><span data-stu-id="28e6a-144">Trigger a function manually</span></span>
* <span data-ttu-id="28e6a-145">Écriture de journaux</span><span class="sxs-lookup"><span data-stu-id="28e6a-145">Write logs</span></span>

## <span data-ttu-id="28e6a-146"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="28e6a-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="28e6a-147">Ce guide a fourni le code des exemples qui montrent comment toohandle des scénarios courants pour l’utilisation des tables Azure.</span><span class="sxs-lookup"><span data-stu-id="28e6a-147">This guide has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="28e6a-148">Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [Azure WebJobs recommandé de ressources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="28e6a-148">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

