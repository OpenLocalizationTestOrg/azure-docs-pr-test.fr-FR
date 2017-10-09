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
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>Prise en main d’Azure Storage (projets de tâche web Azure)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Vue d'ensemble
Cet article fournit des exemples de code c# illustrant montrent comment toouse hello Azure WebJobs SDK version 1.x avec hello service de stockage de table Windows Azure. exemples de code Hello utilisent hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.

Hello service de stockage de Table Azure vous permet de toostore de grandes quantités de données structurées. service de Hello est une banque de données NoSQL qui accepte des appels authentifiés provenant à l’intérieur et extérieur hello cloud Azure. Les tables Azure sont idéales pour le stockage des données structurées non relationnelles.  Pour plus d’informations, consultez la section [Prise en main d’Azure Table Storage à l’aide de .NET](storage-dotnet-how-to-use-tables.md#create-a-table) .

Certains des extraits de code hello affichent hello **Table** attribut utilisé dans les fonctions qui sont appelées manuellement, autrement dit, ne pas à l’aide d’un des attributs de déclencheur hello.

## <a name="how-tooadd-entities-tooa-table"></a>La table de tooa tooadd entités
table de tooa tooadd entités, utilisez hello **Table** d’attribut avec une **ICollector<T>**  ou **IAsyncCollector<T>**  paramètre où **T** Spécifie le schéma de hello d’entités de hello souhaité tooadd. constructeur d’attribut Hello prend un paramètre de chaîne indiquant le nom de la table de hello hello.

Hello exemple de code suivant ajoute **personne** table de tooa d’entités nommée *entrée*.

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

En général, hello type que vous utilisez avec **ICollector** dérive **TableEntity** ou implémente **ITableEntity**, mais il ne doit pas nécessairement. Un des éléments suivants de hello **personne** classes de travail avec code hello illustré hello précédent **entrée** (méthode).

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

Si vous souhaitez toowork directement avec hello API de stockage Azure, vous pouvez ajouter un **CloudStorageAccount** signature de méthode toohello de paramètre.

## <a name="real-time-monitoring"></a>Surveillance en temps réel
Étant donné que les fonctions d’entrée de données traitent souvent des volumes importants de données, hello du tableau de bord WebJobs SDK fournit des données d’analyse en temps réel. Hello **Invocation journal** section vous indique si la fonction de hello est en cours d’exécution.

![Fonction d’entrée en cours d’exécution](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

Hello **détails de l’appel** page Rapports hello la progression de la fonction (nombre d’entités écrites) pendant qu’il est en cours d’exécution et vous donne une occasion tooabort il.

![Fonction d’entrée en cours d’exécution](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

Lorsque fonction hello se termine, hello **détails de l’appel** page signale le nombre de hello de lignes écrites.

![Arrêt de la fonction d’entrée](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>Comment tooread plusieurs entités à partir d’une table
tooread une table, utilisez hello **Table** d’attribut avec une **IQueryable<T>**  paramètre où taper **T** dérive **TableEntity**ou implémente **ITableEntity**.

Hello exemple de code suivant lit et des journaux de toutes les lignes à partir de hello **entrée** table :

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

### <a name="how-tooread-a-single-entity-from-a-table"></a>Comment tooread une seule entité à partir d’une table
Il existe un **Table** constructeur d’attribut avec deux paramètres supplémentaires qui vous permettent de spécifier la clé de partition hello et clé de ligne lorsque vous souhaitez que les entités de table unique toobind tooa.

Hello exemple de code suivant lit une ligne de table pour une **personne** entité en fonction de partition clé et la ligne de valeurs de clé a reçu un message de la file d’attente :  

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


Hello **personne** classe dans cet exemple n’a pas tooimplement **ITableEntity**.

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>Comment toouse hello API de stockage .NET directement toowork avec une table
Vous pouvez également utiliser hello **Table** d’attribut avec un **CloudTable** objet pour une plus grande souplesse de l’utilisation d’une table.

exemple de code suivant de Hello un **CloudTable** tooadd un toohello d’entité unique de l’objet *entrée* table.

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

Pour plus d’informations sur la façon toouse hello **CloudTable** d’objets, consultez [prise en main le stockage de Table Azure à l’aide de .NET](storage-dotnet-how-to-use-tables.md).

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Rubriques connexes couvertes par les files d’attente de hello procédure-tooarticle
Pour plus d’informations sur la façon dont le traitement de table toohandle déclenché par un message de la file d’attente, ou pour les tâches Web scénarios du Kit de développement logiciel pas le traitement, consultez spécifiques tootable [prise en main de stockage de la file d’attente Azure et Visual Studio connecté services (projets de la tâche Web) ](vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>Étapes suivantes
Cet article a fourni le code des exemples qui montrent comment toohandle des scénarios courants pour l’utilisation des tables Azure. Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [les ressources de documentation Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

