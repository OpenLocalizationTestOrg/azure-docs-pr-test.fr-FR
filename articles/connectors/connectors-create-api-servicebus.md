---
title: "Découvrez comment utiliser le connecteur Azure Service Bus dans vos applications logiques | Microsoft Docs"
description: "Créez des applications logiques avec Azure App Service. Connectez-vous à Azure Service Bus pour envoyer et recevoir des messages. Vous pouvez effectuer des actions comme envoyer vers une file d'attente, envoyer vers une rubrique, recevoir d’une file d'attente et recevoir d'un abonnement."
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
ms.openlocfilehash: 1e2ce06f5993280dbdb67121849591e67f7979e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-service-bus-connector"></a><span data-ttu-id="f9609-105">Prise en main du connecteur Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="f9609-105">Get started with the Azure Service Bus connector</span></span>
<span data-ttu-id="f9609-106">Connectez-vous à Azure Service Bus pour envoyer et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="f9609-106">Connect to Azure Service Bus to send and receive messages.</span></span> <span data-ttu-id="f9609-107">Vous pouvez effectuer des actions comme envoyer vers une file d'attente, envoyer vers une rubrique, recevoir d’une file d'attente et recevoir d'un abonnement.</span><span class="sxs-lookup"><span data-stu-id="f9609-107">You can perform actions such as send to queue, send to topic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="f9609-108">Pour utiliser [n’importe quel connecteur](apis-list.md), vous devez commencer par créer une application logique.</span><span class="sxs-lookup"><span data-stu-id="f9609-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="f9609-109">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f9609-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-service-bus"></a><span data-ttu-id="f9609-110">Se connecter à Service Bus</span><span class="sxs-lookup"><span data-stu-id="f9609-110">Connect to Service Bus</span></span>
<span data-ttu-id="f9609-111">Pour que votre application logique puisse accéder à un service, vous devez commencer par créer une connexion à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="f9609-111">Before your logic app can access any service, you first need to create a connection to the service.</span></span> <span data-ttu-id="f9609-112">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="f9609-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps to create a connection to Azure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="f9609-113">Utiliser un déclencheur Service Bus</span><span class="sxs-lookup"><span data-stu-id="f9609-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="f9609-114">Un déclencheur est un événement qui peut être utilisé pour lancer le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="f9609-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="f9609-115">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f9609-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="f9609-116">Utiliser une action Service Bus</span><span class="sxs-lookup"><span data-stu-id="f9609-116">Use a Service Bus action</span></span>
<span data-ttu-id="f9609-117">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="f9609-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="f9609-118">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f9609-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps to create a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="f9609-119">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="f9609-119">Connector-specific details</span></span>

<span data-ttu-id="f9609-120">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="f9609-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f9609-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9609-121">Next steps</span></span>
<span data-ttu-id="f9609-122">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f9609-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

