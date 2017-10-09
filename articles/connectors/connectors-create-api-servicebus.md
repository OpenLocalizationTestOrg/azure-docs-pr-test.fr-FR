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
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="ba95c-105">Prise en main connecteur de Service Bus de Azure hello</span><span class="sxs-lookup"><span data-stu-id="ba95c-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="ba95c-106">Se connecter tooAzure Service Bus toosend et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="ba95c-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="ba95c-107">Vous pouvez effectuer des actions comme l’envoi tooqueue, tootopic d’envoi, de file d’attente de réception et de réception de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="ba95c-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="ba95c-108">toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique.</span><span class="sxs-lookup"><span data-stu-id="ba95c-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="ba95c-109">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ba95c-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="ba95c-110">Se connecter tooService Bus</span><span class="sxs-lookup"><span data-stu-id="ba95c-110">Connect tooService Bus</span></span>
<span data-ttu-id="ba95c-111">Avant que votre application logique peut accéder à n’importe quel service, vous devez d’abord toocreate un service de toohello de connexion.</span><span class="sxs-lookup"><span data-stu-id="ba95c-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="ba95c-112">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="ba95c-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="ba95c-113">Utiliser un déclencheur Service Bus</span><span class="sxs-lookup"><span data-stu-id="ba95c-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="ba95c-114">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="ba95c-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="ba95c-115">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ba95c-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="ba95c-116">Utiliser une action Service Bus</span><span class="sxs-lookup"><span data-stu-id="ba95c-116">Use a Service Bus action</span></span>
<span data-ttu-id="ba95c-117">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="ba95c-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="ba95c-118">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ba95c-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="ba95c-119">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="ba95c-119">Connector-specific details</span></span>

<span data-ttu-id="ba95c-120">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="ba95c-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ba95c-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba95c-121">Next steps</span></span>
<span data-ttu-id="ba95c-122">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ba95c-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

