---
title: "aaaSend événements tooAzure concentrateurs d’événements à l’aide de .NET Standard | Documents Microsoft"
description: "Prise en main de l’envoi d’événements tooEvent concentrateurs dans .NET Standard"
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a>Commencer l’envoi de messages tooAzure concentrateurs d’événements dans .NET Standard

> [!NOTE]
> Cet exemple est disponible sur [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).

Ce didacticiel montre comment toowrite une application console .NET Core qui envoie un ensemble de messages tooan concentrateur d’événements. Vous pouvez exécuter hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution en tant que-remplacer hello `EhConnectionString` et `EhEntityPath` de chaînes avec vos valeurs de concentrateur d’événements. Vous pouvez également suivre hello étapes de ce didacticiel toocreate votre propre.

## <a name="prerequisites"></a>Composants requis

* [Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com). exemples de Hello dans ce didacticiel, utilisez Visual Studio 2017, mais Visual Studio 2015 est également pris en charge.
* [Outils Visual Studio 2015 ou 2017 .NET Core](http://www.microsoft.com/net/core).
* Un abonnement Azure.
* Un espace de noms de concentrateur d’événements.

concentrateur d’événements toosend messages tooan, nous allons utiliser Visual Studio toowrite une application console c#.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Création d’un espace de noms Event Hubs et d’un concentrateur d’événements

première étape de Hello est toouse hello [portail Azure](https://portal.azure.com) toocreate un espace de noms pour le type de concentrateur d’événements hello et obtenir des informations d’identification de gestion que votre application doit toocommunicate avec un concentrateur d’événements hello hello. toocreate un espace de noms et d’un concentrateur d’événements, suivez la procédure hello dans [cet article](event-hubs-create.md), puis poursuivez hello comme suit.

## <a name="create-a-console-application"></a>Création d’une application console

Démarrez Visual Studio. À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**. Créez une application console .NET Core.

![Nouveau projet][1]

## <a name="add-hello-event-hubs-nuget-package"></a>Ajouter un package NuGet de concentrateurs d’événements de hello

Ajouter hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard bibliothèque NuGet package tooyour projet en procédant comme suit : 

1. Avec le bouton droit de projet de hello nouvellement créé et sélectionnez **gérer les Packages NuGet**.
2. Cliquez sur hello **Parcourir** tab, puis recherchez « Microsoft.Azure.EventHubs » et sélectionnez hello **Microsoft.Azure.EventHubs** package. Cliquez sur **installer** toocomplete hello installation, puis fermez cette boîte de dialogue.

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a>Écrire certaines concentrateur d’événements toohello messages code toosend

1. Ajoutez hello suit `using` haut de toohello instructions du fichier Program.cs de hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. Ajouter des constantes toohello `Program` classe hello concentrateurs d’événements connexion entité et la chaîne de chemin d’accès (nom du concentrateur d’événements). Remplacez les espaces réservés de hello entre crochets avec les valeurs appropriées hello qui ont été obtenus lors de la création du concentrateur d’événements hello.

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. Ajoutez une nouvelle méthode nommée `MainAsync` toohello `Program` de classe, comme suit :

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. Ajoutez une nouvelle méthode nommée `SendMessagesToEventHub` toohello `Program` de classe, comme suit :

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. Ajouter hello suivant code toohello `Main` méthode Bonjour `Program` classe.

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   Voici à quoi doit ressembler votre fichier Program.cs.

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. Exécuter le programme de hello et vérifiez qu’il n’y a aucune erreur.

Félicitations ! Vous avez maintenant envoyé concentrateur d’événements tooan messages.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Recevoir des événements d’Event Hubs](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
* [Créer un concentrateur d’événements](event-hubs-create.md)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
