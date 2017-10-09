---
title: "aaaGetting démarré avec le stockage Azure et Visual Studio connecté services (projets de la tâche Web)"
description: "Comment tooget démarrer l’utilisation du stockage de Table Azure dans un projet de tâches Web Azure dans Visual Studio une fois la connexion de compte de stockage tooa à l’aide de Visual Studio services connectés"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 448dee3369207062ee85c6636c84bcb4e26a2085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="520e4-103">Prise en main d’Azure Storage (projets de tâche web Azure)</span><span class="sxs-lookup"><span data-stu-id="520e4-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="520e4-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="520e4-104">Overview</span></span>
<span data-ttu-id="520e4-105">Cet article fournit des exemples de code c# illustrant montrent comment toouse hello Azure WebJobs SDK version 1.x avec hello service de stockage de table Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="520e4-105">This article provides C# code samples that show show how toouse hello Azure WebJobs SDK version 1.x with hello Azure table storage service.</span></span> <span data-ttu-id="520e4-106">exemples de code Hello utilisent hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="520e4-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="520e4-107">Hello service de stockage de Table Azure vous permet de toostore de grandes quantités de données structurées.</span><span class="sxs-lookup"><span data-stu-id="520e4-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="520e4-108">service de Hello est une banque de données NoSQL qui accepte des appels authentifiés provenant à l’intérieur et extérieur hello cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="520e4-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="520e4-109">Les tables Azure sont idéales pour le stockage des données structurées non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="520e4-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="520e4-110">Pour plus d’informations, consultez la section [Prise en main d’Azure Table Storage à l’aide de .NET](storage-dotnet-how-to-use-tables.md#create-a-table) .</span><span class="sxs-lookup"><span data-stu-id="520e4-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="520e4-111">Certains des extraits de code hello affichent hello **Table** attribut utilisé dans les fonctions qui sont appelées manuellement, autrement dit, ne pas à l’aide d’un des attributs de déclencheur hello.</span><span class="sxs-lookup"><span data-stu-id="520e4-111">Some of hello code snippets show hello **Table** attribute used in functions that are called manually, that is, not by using one of hello trigger attributes.</span></span>

## <a name="how-tooadd-entities-tooa-table"></a><span data-ttu-id="520e4-112">La table de tooa tooadd entités</span><span class="sxs-lookup"><span data-stu-id="520e4-112">How tooadd entities tooa table</span></span>
<span data-ttu-id="520e4-113">table de tooa tooadd entités, utilisez hello **Table** d’attribut avec une **ICollector<T>**  ou **IAsyncCollector<T>**  paramètre où **T** Spécifie le schéma de hello d’entités de hello souhaité tooadd.</span><span class="sxs-lookup"><span data-stu-id="520e4-113">tooadd entities tooa table, use hello **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="520e4-114">constructeur d’attribut Hello prend un paramètre de chaîne indiquant le nom de la table de hello hello.</span><span class="sxs-lookup"><span data-stu-id="520e4-114">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span>

<span data-ttu-id="520e4-115">Hello exemple de code suivant ajoute **personne** table de tooa d’entités nommée *entrée*.</span><span class="sxs-lookup"><span data-stu-id="520e4-115">hello following code sample adds **Person** entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="520e4-116">En général, hello type que vous utilisez avec **ICollector** dérive **TableEntity** ou implémente **ITableEntity**, mais il ne doit pas nécessairement.</span><span class="sxs-lookup"><span data-stu-id="520e4-116">Typically hello type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="520e4-117">Un des éléments suivants de hello **personne** classes de travail avec code hello illustré hello précédent **entrée** (méthode).</span><span class="sxs-lookup"><span data-stu-id="520e4-117">Either of hello following **Person** classes work with hello code shown in hello preceding **Ingress** method.</span></span>

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

<span data-ttu-id="520e4-118">Si vous souhaitez toowork directement avec hello API de stockage Azure, vous pouvez ajouter un **CloudStorageAccount** signature de méthode toohello de paramètre.</span><span class="sxs-lookup"><span data-stu-id="520e4-118">If you want toowork directly with hello Azure storage API, you can add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="520e4-119">Surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="520e4-119">Real-time monitoring</span></span>
<span data-ttu-id="520e4-120">Étant donné que les fonctions d’entrée de données traitent souvent des volumes importants de données, hello du tableau de bord WebJobs SDK fournit des données d’analyse en temps réel.</span><span class="sxs-lookup"><span data-stu-id="520e4-120">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="520e4-121">Hello **Invocation journal** section vous indique si la fonction de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="520e4-121">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Fonction d’entrée en cours d’exécution](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="520e4-123">Hello **détails de l’appel** page Rapports hello la progression de la fonction (nombre d’entités écrites) pendant qu’il est en cours d’exécution et vous donne une occasion tooabort il.</span><span class="sxs-lookup"><span data-stu-id="520e4-123">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span>

![Fonction d’entrée en cours d’exécution](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="520e4-125">Lorsque fonction hello se termine, hello **détails de l’appel** page signale le nombre de hello de lignes écrites.</span><span class="sxs-lookup"><span data-stu-id="520e4-125">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Arrêt de la fonction d’entrée](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a><span data-ttu-id="520e4-127">Comment tooread plusieurs entités à partir d’une table</span><span class="sxs-lookup"><span data-stu-id="520e4-127">How tooread multiple entities from a table</span></span>
<span data-ttu-id="520e4-128">tooread une table, utilisez hello **Table** d’attribut avec une **IQueryable<T>**  paramètre où taper **T** dérive **TableEntity**ou implémente **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="520e4-128">tooread a table, use hello **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="520e4-129">Hello exemple de code suivant lit et des journaux de toutes les lignes à partir de hello **entrée** table :</span><span class="sxs-lookup"><span data-stu-id="520e4-129">hello following code sample reads and logs all rows from hello **Ingress** table:</span></span>

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

### <a name="how-tooread-a-single-entity-from-a-table"></a><span data-ttu-id="520e4-130">Comment tooread une seule entité à partir d’une table</span><span class="sxs-lookup"><span data-stu-id="520e4-130">How tooread a single entity from a table</span></span>
<span data-ttu-id="520e4-131">Il existe un **Table** constructeur d’attribut avec deux paramètres supplémentaires qui vous permettent de spécifier la clé de partition hello et clé de ligne lorsque vous souhaitez que les entités de table unique toobind tooa.</span><span class="sxs-lookup"><span data-stu-id="520e4-131">There is a **Table** attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="520e4-132">Hello exemple de code suivant lit une ligne de table pour une **personne** entité en fonction de partition clé et la ligne de valeurs de clé a reçu un message de la file d’attente :</span><span class="sxs-lookup"><span data-stu-id="520e4-132">hello following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="520e4-133">Hello **personne** classe dans cet exemple n’a pas tooimplement **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="520e4-133">hello **Person** class in this example does not have tooimplement **ITableEntity**.</span></span>

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a><span data-ttu-id="520e4-134">Comment toouse hello API de stockage .NET directement toowork avec une table</span><span class="sxs-lookup"><span data-stu-id="520e4-134">How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="520e4-135">Vous pouvez également utiliser hello **Table** d’attribut avec un **CloudTable** objet pour une plus grande souplesse de l’utilisation d’une table.</span><span class="sxs-lookup"><span data-stu-id="520e4-135">You can also use hello **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="520e4-136">exemple de code suivant de Hello un **CloudTable** tooadd un toohello d’entité unique de l’objet *entrée* table.</span><span class="sxs-lookup"><span data-stu-id="520e4-136">hello following code sample uses a **CloudTable** object tooadd a single entity toohello *Ingress* table.</span></span>

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

<span data-ttu-id="520e4-137">Pour plus d’informations sur la façon toouse hello **CloudTable** d’objets, consultez [prise en main le stockage de Table Azure à l’aide de .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="520e4-137">For more information about how toouse hello **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a><span data-ttu-id="520e4-138">Rubriques connexes couvertes par les files d’attente de hello procédure-tooarticle</span><span class="sxs-lookup"><span data-stu-id="520e4-138">Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="520e4-139">Pour plus d’informations sur la façon dont le traitement de table toohandle déclenché par un message de la file d’attente, ou pour les tâches Web scénarios du Kit de développement logiciel pas le traitement, consultez spécifiques tootable [prise en main de stockage de la file d’attente Azure et Visual Studio connecté services (projets de la tâche Web) ](vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="520e4-139">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="520e4-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="520e4-140">Next steps</span></span>
<span data-ttu-id="520e4-141">Cet article a fourni le code des exemples qui montrent comment toohandle des scénarios courants pour l’utilisation des tables Azure.</span><span class="sxs-lookup"><span data-stu-id="520e4-141">This article has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="520e4-142">Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [les ressources de documentation Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="520e4-142">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

