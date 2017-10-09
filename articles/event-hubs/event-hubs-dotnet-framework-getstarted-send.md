---
title: "aaaSend événements tooAzure concentrateurs d’événements à l’aide de hello .NET Framework | Documents Microsoft"
description: "Prise en main de l’envoi d’événements concentrateurs tooEvent à l’aide de hello .NET Framework"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a>Envoyer des événements de concentrateurs d’événements tooAzure à l’aide de hello .NET Framework

## <a name="introduction"></a>Introduction

Event Hubs constitue un service qui traite de grandes quantités de données d'événement (télémétrie) à partir de périphériques et d'applications connectés. Après avoir recueilli les données aux concentrateurs d’événements, vous pouvez stocker les données de salutation à l’aide d’un cluster de stockage ou transformer à l’aide d’un fournisseur de l’analytique en temps réel. Cette fonctionnalité de collecte et de traitement des événements à grande échelle est un composant clé des architectures d’application moderne, y compris hello Internet of Things (IoT).

Ce didacticiel montre comment toouse hello [portail Azure](https://portal.azure.com) toocreate un concentrateur d’événements. Il montre également comment le concentrateur d’événements toosend événements tooan à l’aide d’une application console écrite en c# à l’aide de hello .NET Framework. événements de tooreceive à l’aide de hello .NET Framework, consultez hello [recevoir des événements à l’aide de .NET Framework de hello](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, ou cliquez sur hello réception langue dans la table de gauche hello du contenu.

toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :

* [Microsoft Visual Studio 2015 ou une version ultérieure](http://visualstudio.com). captures d’écran Hello dans ce didacticiel utilisent Visual Studio 2017.
* Un compte Azure actif. Si vous n’en avez pas, vous pouvez créer un compte gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Création d’un espace de noms Event Hubs et d’un concentrateur d’événements

première étape de Hello est toouse hello [portail Azure](https://portal.azure.com) toocreate un espace de noms de concentrateurs d’événements de type et obtenir des informations d’identification d’administration votre application doit toocommunicate avec un concentrateur d’événements hello hello. toocreate un espace de noms et le concentrateur d’événements, suivez la procédure hello dans [cet article](event-hubs-create.md), puis poursuivez hello suivant les étapes de ce didacticiel.

## <a name="create-a-sender-console-application"></a>Créer une application de console d’expéditeur

Dans cette section, vous allez écrire une application de console Windows qui envoie le concentrateur d’événements événements tooyour.

1. Dans Visual Studio, créez un nouveau projet d’application de bureau Visual c# à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **expéditeur**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. Dans l’Explorateur de solutions, cliquez sur hello **expéditeur** de projet, puis cliquez sur **gérer les Packages NuGet pour la Solution**. 
3. Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`. Cliquez sur **installer**et acceptez les conditions d’utilisation de hello. 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    Visual Studio télécharge, installe et ajoute une référence toohello [package NuGet de bibliothèque Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).
4. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. Ajouter hello suivant champs toohello **programme** (classe), en remplaçant les valeurs d’espace réservé hello avec nom hello du concentrateur d’événements hello vous avez créé dans la section précédente de hello et chaîne de connexion au niveau de l’espace de noms hello vous avez enregistré précédemment.
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. Ajouter hello suivant de méthode toohello **programme** classe :
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  Cette méthode envoie en permanence le concentrateur d’événements événements tooyour dans un délai de 200 ms.
7. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. Exécuter le programme de hello et vérifiez qu’il n’y a aucune erreur.
  
Félicitations ! Vous avez maintenant envoyé concentrateur d’événements tooan messages.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez créé une application opérationnelle qui crée un concentrateur d’événements et envoie les données, vous pouvez déplacer sur toohello les scénarios suivants :

* [Recevoir des événements à l’aide de hello processeur d’événements hôte](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [Informations de référence de l’hôte du processeur d’événements](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

