---
title: connecteur de Service Bus de Azure aaaLearn toouse hello dans vos applications logiques | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. Se connecter tooAzure Service Bus toosend et recevoir des messages. Vous pouvez effectuer des actions comme l’envoi tooqueue, tootopic d’envoi, de file d’attente de réception et de réception de l’abonnement."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a>Prise en main connecteur de Service Bus de Azure hello
Se connecter tooAzure Service Bus toosend et recevoir des messages. Vous pouvez effectuer des actions comme l’envoi tooqueue, tootopic d’envoi, de file d’attente de réception et de réception de l’abonnement.

toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique. Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooservice-bus"></a>Se connecter tooService Bus
Avant que votre application logique peut accéder à n’importe quel service, vous devez d’abord toocreate un service de toohello de connexion. Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a>Utiliser un déclencheur Service Bus
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique. [En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a>Utiliser une action Service Bus
Une action est une opération effectuée par flux de travail hello défini dans une application logique. [En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/servicebus/). 

## <a name="next-steps"></a>Étapes suivantes
[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

