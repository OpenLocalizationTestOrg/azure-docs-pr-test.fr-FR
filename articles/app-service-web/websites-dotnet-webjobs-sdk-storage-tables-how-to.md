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
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a>Comment toouse Azure table storage avec hello WebJobs SDK
## <a name="overview"></a>Vue d'ensemble
Ce guide fournit des exemples de code c# qui montrent comment les tables tooread et écriture de stockage Azure à l’aide de [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.

guide de Hello suppose que vous connaissez [comment toocreate un projet de la tâche Web dans Visual Studio avec connexion chaînes ce compte de stockage point tooyour](websites-dotnet-webjobs-sdk-get-started.md) ou trop[plusieurs comptes de stockage](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Certains des extraits de code hello affichent hello `Table` attribut utilisé dans les fonctions qui sont [appelée manuellement](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), autrement dit, ne pas à l’aide d’un des attributs de déclencheur hello. 

## <a id="ingress"></a>La table de tooa tooadd entités
table de tooa tooadd entités, utilisez hello `Table` d’attribut avec une `ICollector<T>` ou `IAsyncCollector<T>` paramètre où `T` Spécifie le schéma de hello d’entités de hello souhaité tooadd. constructeur d’attribut Hello prend un paramètre de chaîne indiquant le nom de la table de hello hello. 

Hello exemple de code suivant ajoute `Person` table de tooa d’entités nommée *entrée*.

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

En général, hello type que vous utilisez avec `ICollector` dérive `TableEntity` ou implémente `ITableEntity`, mais il ne doit pas nécessairement. Un des éléments suivants de hello `Person` classes de travail avec code hello illustré hello précédent `Ingress` (méthode).

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

Si vous souhaitez toowork directement avec hello API de stockage Azure, vous pouvez ajouter un `CloudStorageAccount` la signature de méthode toohello paramètre.

## <a id="monitor"></a> Surveillance en temps réel
Étant donné que les fonctions d’entrée de données traitent souvent des volumes importants de données, hello du tableau de bord WebJobs SDK fournit des données d’analyse en temps réel. Hello **Invocation journal** section vous indique si la fonction de hello est en cours d’exécution.

![Fonction d’entrée en cours d’exécution](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

Hello **détails de l’appel** page Rapports hello la progression de la fonction (nombre d’entités écrites) pendant qu’il est en cours d’exécution et vous donne une occasion tooabort il. 

![Fonction d’entrée en cours d’exécution](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

Lorsque fonction hello se termine, hello **détails de l’appel** page signale le nombre de hello de lignes écrites.

![Arrêt de la fonction d’entrée](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>Comment tooread plusieurs entités à partir d’une table
tooread une table, utilisez hello `Table` d’attribut avec une `IQueryable<T>` paramètre où taper `T` dérive `TableEntity` ou implémente `ITableEntity`.

Hello exemple de code suivant lit et des journaux de toutes les lignes à partir de hello `Ingress` table :

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

### <a id="readone"></a>Comment tooread une seule entité à partir d’une table
Il existe un `Table` constructeur d’attribut avec deux paramètres supplémentaires qui vous permettent de spécifier la clé de partition hello et clé de ligne lorsque vous souhaitez que les entités de table unique toobind tooa.

Hello exemple de code suivant lit une ligne de table pour une `Person` entité en fonction de partition clé et la ligne de valeurs de clé a reçu un message de la file d’attente :  

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


Hello `Person` classe dans cet exemple n’a pas de tooimplement `ITableEntity`.

## <a id="storageapi"></a>Comment toouse hello API de stockage .NET directement toowork avec une table
Vous pouvez également utiliser hello `Table` d’attribut avec un `CloudTable` objet pour une plus grande souplesse de l’utilisation d’une table.

exemple de code suivant de Hello un `CloudTable` tooadd un toohello d’entité unique de l’objet *entrée* table. 

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

Pour plus d’informations sur la façon toouse hello `CloudTable` d’objets, consultez [comment toouse le stockage de Table à partir de .NET](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Rubriques connexes couvertes par les files d’attente de hello procédure-tooarticle
Pour plus d’informations sur la façon dont le traitement de table toohandle déclenché par un message de la file d’attente, ou pour les tâches Web scénarios du Kit de développement logiciel pas le traitement, consultez spécifiques tootable [comment toouse Azure file d’attente de stockage avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Les sujets abordés dans cet article hello suivants :

* Fonctions asynchrones
* Instances multiples
* Arrêt approprié
* Utiliser les attributs de WebJobs SDK dans le corps d’une fonction de hello
* Définir des chaînes de connexion du Kit de développement logiciel hello dans le code
* Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code
* Déclenchement manuel d’une fonction
* Écriture de journaux

## <a id="nextsteps"></a> Étapes suivantes
Ce guide a fourni le code des exemples qui montrent comment toohandle des scénarios courants pour l’utilisation des tables Azure. Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [Azure WebJobs recommandé de ressources](http://go.microsoft.com/fwlink/?linkid=390226).

