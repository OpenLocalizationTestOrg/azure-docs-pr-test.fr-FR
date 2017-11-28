---
title: "Découvrez comment utiliser le connecteur Salesforce dans vos applications logiques | Microsoft Docs"
description: "Créez des applications logiques avec Azure App Service. Le connecteur Salesforce offre une API permettant de travailler avec des objets Salesforce."
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
ms.openlocfilehash: c2e2efd356382df9404f5c4ed54f24758b2cd22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="9c1e6-104">Prise en main du connecteur Salesforce</span><span class="sxs-lookup"><span data-stu-id="9c1e6-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="9c1e6-105">Le connecteur Salesforce offre une API permettant de travailler avec des objets Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9c1e6-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="9c1e6-106">Pour utiliser [n’importe quel connecteur](apis-list.md), vous devez commencer par créer une application logique.</span><span class="sxs-lookup"><span data-stu-id="9c1e6-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="9c1e6-107">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9c1e6-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="9c1e6-108">Se connecter au connecteur Salesforce</span><span class="sxs-lookup"><span data-stu-id="9c1e6-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="9c1e6-109">Pour que votre application logique puisse accéder à un service, vous devez commencer par créer une *connexion* à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="9c1e6-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="9c1e6-110">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="9c1e6-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="9c1e6-111">Créer une connexion au connecteur Salesforce</span><span class="sxs-lookup"><span data-stu-id="9c1e6-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="9c1e6-112">Utiliser un déclencheur du connecteur Salesforce</span><span class="sxs-lookup"><span data-stu-id="9c1e6-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="9c1e6-113">Un déclencheur est un événement qui peut être utilisé pour lancer le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="9c1e6-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="9c1e6-114">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9c1e6-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="9c1e6-115">Ajouter une condition</span><span class="sxs-lookup"><span data-stu-id="9c1e6-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="9c1e6-116">Utiliser une action du connecteur Salesforce</span><span class="sxs-lookup"><span data-stu-id="9c1e6-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="9c1e6-117">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="9c1e6-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="9c1e6-118">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9c1e6-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="9c1e6-119">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="9c1e6-119">Connector-specific details</span></span>

<span data-ttu-id="9c1e6-120">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="9c1e6-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9c1e6-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9c1e6-121">Next steps</span></span>
[<span data-ttu-id="9c1e6-122">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="9c1e6-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

