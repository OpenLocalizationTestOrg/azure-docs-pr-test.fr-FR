---
title: aaaLearn toouse hello connecteur Salesforce dans vos applications logiques | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. Hello connecteur Salesforce fournit un toowork API avec les objets de la force de vente."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b14b41fa8a4648b4f0090472dc0f9575bf13a2ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-salesforce-connector"></a><span data-ttu-id="259a1-104">Prise en main connecteur Salesforce de hello</span><span class="sxs-lookup"><span data-stu-id="259a1-104">Get started with hello Salesforce connector</span></span>
<span data-ttu-id="259a1-105">Hello connecteur Salesforce fournit un toowork API avec les objets de la force de vente.</span><span class="sxs-lookup"><span data-stu-id="259a1-105">hello Salesforce Connector provides an API toowork with Salesforce objects.</span></span>

<span data-ttu-id="259a1-106">toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique.</span><span class="sxs-lookup"><span data-stu-id="259a1-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="259a1-107">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="259a1-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosalesforce-connector"></a><span data-ttu-id="259a1-108">Se connecter tooSalesforce connecteur</span><span class="sxs-lookup"><span data-stu-id="259a1-108">Connect tooSalesforce connector</span></span>
<span data-ttu-id="259a1-109">Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service.</span><span class="sxs-lookup"><span data-stu-id="259a1-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="259a1-110">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="259a1-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosalesforce-connector"></a><span data-ttu-id="259a1-111">Créer un connecteur de tooSalesforce de connexion</span><span class="sxs-lookup"><span data-stu-id="259a1-111">Create a connection tooSalesforce connector</span></span>
> [!INCLUDE [Steps toocreate a connection tooSalesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="259a1-112">Utiliser un déclencheur du connecteur Salesforce</span><span class="sxs-lookup"><span data-stu-id="259a1-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="259a1-113">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="259a1-113">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="259a1-114">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="259a1-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="259a1-115">Ajouter une condition</span><span class="sxs-lookup"><span data-stu-id="259a1-115">Add a condition</span></span>
> [!INCLUDE [Steps toocreate a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="259a1-116">Utiliser une action du connecteur Salesforce</span><span class="sxs-lookup"><span data-stu-id="259a1-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="259a1-117">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="259a1-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="259a1-118">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="259a1-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="259a1-119">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="259a1-119">Connector-specific details</span></span>

<span data-ttu-id="259a1-120">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="259a1-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="259a1-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="259a1-121">Next steps</span></span>
[<span data-ttu-id="259a1-122">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="259a1-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

