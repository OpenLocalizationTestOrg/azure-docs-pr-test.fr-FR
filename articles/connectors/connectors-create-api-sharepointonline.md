---
title: "Découvrez comment utiliser le connecteur SharePoint Online dans les applications logiques | Microsoft Docs"
description: "Créez des applications logiques avec le connecteur SharePoint Online pour gérer des listes sur SharePoint."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e0ec3149-507a-409d-8e7b-d5fbded006ce
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 96fc1347604c0c6cc2c2463a5dbd83b560183a16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-online-connector"></a><span data-ttu-id="68f6d-103">Prise en main du connecteur SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="68f6d-103">Get started with the SharePoint Online connector</span></span>
<span data-ttu-id="68f6d-104">Utilisez le connecteur SharePoint Online pour gérer des listes SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68f6d-104">Use the SharePoint Online connector to manage SharePoint lists.</span></span>  

<span data-ttu-id="68f6d-105">Pour utiliser [n’importe quel connecteur](apis-list.md), vous devez commencer par créer une application logique.</span><span class="sxs-lookup"><span data-stu-id="68f6d-105">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="68f6d-106">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="68f6d-106">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sharepoint-online"></a><span data-ttu-id="68f6d-107">Se connecter à SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="68f6d-107">Connect to SharePoint Online</span></span>
<span data-ttu-id="68f6d-108">Pour que votre application logique puisse accéder à un service, vous devez commencer par créer une *connexion* à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="68f6d-108">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="68f6d-109">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="68f6d-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sharepoint-online"></a><span data-ttu-id="68f6d-110">Créer une connexion à SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="68f6d-110">Create a connection to SharePoint Online</span></span>
> [!INCLUDE [Steps to create a connection to SharePoint](../../includes/connectors-create-api-sharepointonline.md)]


## <a name="use-a-sharepoint-online-trigger"></a><span data-ttu-id="68f6d-111">Utiliser un déclencheur SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="68f6d-111">Use a SharePoint Online trigger</span></span>
<span data-ttu-id="68f6d-112">Un déclencheur est un événement qui peut être utilisé pour lancer le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="68f6d-112">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="68f6d-113">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="68f6d-113">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online trigger](../../includes/connectors-create-api-sharepointonline-trigger.md)]


## <a name="use-a-sharepoint-online-action"></a><span data-ttu-id="68f6d-114">Utiliser une action SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="68f6d-114">Use a SharePoint Online action</span></span>
<span data-ttu-id="68f6d-115">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="68f6d-115">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="68f6d-116">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="68f6d-116">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online action](../../includes/connectors-create-api-sharepointonline-action.md)]


## <a name="connector-specific-details"></a><span data-ttu-id="68f6d-117">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="68f6d-117">Connector-specific details</span></span>

<span data-ttu-id="68f6d-118">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="68f6d-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="68f6d-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68f6d-119">Next Steps</span></span>
[<span data-ttu-id="68f6d-120">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="68f6d-120">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

