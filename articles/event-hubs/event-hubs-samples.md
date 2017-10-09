---
title: "exemples de concentrateurs d’événements aaaAzure | Documents Microsoft"
description: Exemples Azure Event Hubs
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
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a>Exemples de hubs d’événements 

ensemble d’exemples de concentrateurs d’événements Azure Hello illustre les fonctionnalités clés dans [Azure Event Hubs](/azure/event-hubs/). Cet article de la catégorie et décrit les exemples hello disponibles, avec des liens tooeach.

Au moment de hello de rédaction de cet article, les exemples de concentrateurs d’événements se trouvent à différents endroits :

- [Exemples de code développeur MSDN](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Pour plus d’informations sur les différentes versions de hello .NET Framework, consultez [infrastructures et cibles](/dotnet/articles/standard/frameworks).

D’autres exemples vont être ajoutés au fil du temps, alors consultez régulièrement cette page pour vérifier les mises à jour.

## <a name="net-standard"></a>.NET Standard

Hello exemples suivants montrent comment toosend et recevoir des événements à l’aide de hello [client de concentrateurs d’événements](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) pour hello [bibliothèque .NET Standard](/dotnet/articles/standard/library).

### <a name="send-events"></a>Envoyer des événements 

Hello [prise en main envoi](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) montre comment toowrite un .NET Core console application qui envoie le concentrateur d’événements événements tooan.

### <a name="receive-events"></a>Recevoir des événements 

Hello [prise en main de réception avec hello processeur d’événements hôte](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) exemple est une application console .NET Core qui reçoit des messages à partir d’un concentrateur d’événements à l’aide de hello processeur d’événements hôte.

## <a name="net-framework"></a>.NET Framework   

Ces exemples illustrent diverses fonctionnalités de Azure Event Hubs, ciblage hello [bibliothèque .NET Framework](/dotnet/framework/index).
 
### <a name="notify-users-of-events-received"></a>Avertir les utilisateurs de la réception d’événements

Hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) exemple informe les utilisateurs de données provenant des capteurs ou d’autres systèmes.

### <a name="get-started-with-event-hubs"></a>Prise en main des hubs d’événements 

Hello [événement concentrateurs mise en route](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) exemple illustre les fonctionnalités de base hello des concentrateurs d’événements, telles que comment envoyer le concentrateur d’événements événements tooan toocreate un concentrateur d’événements et consommer des événements à l’aide de hello [processeur d’événements hôte](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).

### <a name="scale-out-event-processing"></a>Traitement d’événement mis à l’échelle 

Hello [montée en charge le traitement des événements](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) exemple illustre comment toouse hello [processeur d’événements hôte](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) la charge de travail hello toodistribute de consommation de flux de concentrateurs d’événements. Il montre comment tooimplement hello **EventProcessor** et **EventProcessorFactory** flux d’événements objets toomanage hello. 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>Extraire des données de SQL dans Event Hub

Hello [de données SQL d’extraction](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) exemple montre comment les données toopull à partir d’un SQL de table et poussez-le tooan toouse en tant qu’entrée dans les applications analytiques en aval, concentrateur d’événements.

### <a name="pull-web-data-into-an-event-hub"></a>Extraire des données web dans un Event Hub 

Hello [importer des données à partir du web de hello](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) montre comment les données de toopull public (par exemple, informations sur le trafic du service de transport flux de hello) de flux et poussez-le tooan concentrateur d’événements.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur les versions du .NET Framework en visitant hello suivant liens :

- [Infrastructures et cibles](/dotnet/articles/standard/frameworks)
- [.NET Framework 4.6 et 4.5](/dotnet/framework/index)

Vous plus d’informations sur les concentrateurs d’événements Bonjour suivant des articles :

- [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
- [Créer un concentrateur d’événements](event-hubs-create.md)
- [FAQ sur les hubs d'événements](event-hubs-faq.md)