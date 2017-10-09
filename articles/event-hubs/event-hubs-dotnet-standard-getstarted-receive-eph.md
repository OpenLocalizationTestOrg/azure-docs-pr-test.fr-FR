---
title: "événements d’aaaReceive de concentrateurs d’événements Azure à l’aide de .NET Standard | Documents Microsoft"
description: "Commencer à recevoir des messages avec hello EventProcessorHost dans .NET Standard"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a>Commencer à recevoir des messages avec hello processeur d’événements hôte dans .NET Standard

> [!NOTE]
> Cet exemple est disponible sur [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).

Ce didacticiel montre comment toowrite un .NET Core console application qui reçoit des messages à partir d’un concentrateur d’événements à l’aide de **EventProcessorHost**. Vous pouvez exécuter hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution en tant que-, remplace les chaînes hello avec vos valeurs de compte événement concentrateur et de stockage. Vous pouvez également suivre hello étapes de ce didacticiel toocreate votre propre.

## <a name="prerequisites"></a>Composants requis

* [Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com). exemples de Hello dans ce didacticiel, utilisez Visual Studio 2017, mais Visual Studio 2015 est également pris en charge.
* [Outils Visual Studio 2015 ou 2017 .NET Core](http://www.microsoft.com/net/core).
* Un abonnement Azure.
* Un espace de noms Azure Event Hubs.
* Un compte de stockage Azure.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Création d’un espace de noms Event Hubs et d’un concentrateur d’événements  

première étape de Hello est toouse hello [portail Azure](https://portal.azure.com) toocreate un espace de noms pour hello concentrateurs d’événements de type et obtenir des informations d’identification de gestion que votre application doit toocommunicate avec un concentrateur d’événements hello hello. toocreate un espace de noms et le concentrateur d’événements, suivez la procédure hello dans [cet article](event-hubs-create.md), puis poursuivez hello comme suit.  

## <a name="create-an-azure-storage-account"></a>Création d'un compte de stockage Azure  

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).  
2. Dans le volet de navigation gauche hello du portail de hello, cliquez sur **nouveau**, cliquez sur **stockage**, puis cliquez sur **compte de stockage**.  
3. Renseignez les champs hello dans le panneau de compte de stockage hello, puis cliquez sur **créer**.

    ![Créer un compte de stockage][1]

4. Une fois que vous consultez hello **a réussi des déploiements** , cliquez sur le nom de hello du nouveau compte de stockage hello. Bonjour **Essentials** panneau, cliquez sur **BLOB**. Hello lorsque **service Blob** panneau s’ouvre, cliquez sur **+ conteneur** haut hello. Donnez un nom à conteneur de hello et fermez hello **service Blob** panneau.  
5. Cliquez sur **clés d’accès** dans hello gauche lame et copie hello le nom du conteneur de stockage hello et valeur hello du compte de stockage hello **key1**. Enregistrez ces tooNotepad de valeurs ou un autre emplacement temporaire.  

## <a name="create-a-console-application"></a>Création d’une application console

Démarrez Visual Studio. À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**. Créez une application console .NET Core.

![Nouveau projet][2]

## <a name="add-hello-event-hubs-nuget-package"></a>Ajouter un package NuGet de concentrateurs d’événements de hello

Ajouter hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) et [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard NuGet packages tooyour projet de bibliothèque d’en procédant comme suit : 

1. Avec le bouton droit de projet de hello nouvellement créé et sélectionnez **gérer les Packages NuGet**.
2. Cliquez sur hello **Parcourir** tab, puis recherchez « Microsoft.Azure.EventHubs » et sélectionnez hello **Microsoft.Azure.EventHubs** package. Cliquez sur **installer** toocomplete hello installation, puis fermez cette boîte de dialogue.
3. Répétez les étapes 1 et 2 et installer hello **Microsoft.Azure.EventHubs.Processor** package.

## <a name="implement-hello-ieventprocessor-interface"></a>Implémenter l’interface IEventProcessor hello

1. Dans l’Explorateur de solutions, projets de hello avec le bouton droit, cliquez sur **ajouter**, puis cliquez sur **classe**. Nommez la nouvelle classe de hello **SimpleEventProcessor**.

2. Ouvrez le fichier de SimpleEventProcessor.cs hello et ajoutez hello suit `using` haut de toohello instructions du fichier de hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. Hello d’implémenter `IEventProcessor` interface. Remplacez hello tout contenu de hello `SimpleEventProcessor` classe avec hello suivant de code :

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a>Écrivez une méthode de console principal qui utilise les messages de salutation SimpleEventProcessor classe tooreceive

1. Ajoutez hello suit `using` haut de toohello instructions du fichier Program.cs de hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. Ajouter des constantes toohello `Program` classe pour la chaîne de connexion du concentrateur hello événement, nom de hub d’événements, nom de conteneur de compte de stockage, nom de compte de stockage et clé de compte de stockage. Ajoutez hello suivant de code, le remplacement des espaces réservés de hello avec leurs valeurs correspondantes.

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. Ajoutez une nouvelle méthode nommée `MainAsync` toohello `Program` de classe, comme suit :

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. Ajouter hello suivant la ligne de code toohello `Main` méthode :

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    Voici à quoi doit ressembler votre fichier Program.cs :

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. Exécuter le programme de hello et vérifiez qu’il n’y a aucune erreur.

Félicitations ! Vous avez désormais reçu des messages à partir d’un concentrateur d’événements à l’aide de hello processeur d’événements hôte.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
* [Créer un concentrateur d’événements](event-hubs-create.md)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
