---
title: Connecteur GitHub dans Azure Logic Apps | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. GitHub est un servie d’hébergement de dépôt Git sur le web. Il offre toutes les fonctionnalités distribuées de contrôle de révision et de gestion du code source (SCM) de Git, ainsi que ses propres fonctionnalités."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="28a1d-105">Prise en main du connecteur GitHub</span><span class="sxs-lookup"><span data-stu-id="28a1d-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="28a1d-106">GitHub est un servie d’hébergement de dépôt Git sur le web.</span><span class="sxs-lookup"><span data-stu-id="28a1d-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="28a1d-107">Il offre toutes les fonctionnalités distribuées de contrôle de révision et de gestion du code source (SCM) de Git, ainsi que ses propres fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="28a1d-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="28a1d-108">Vous pouvez commencer par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="28a1d-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-github"></a><span data-ttu-id="28a1d-109">Créer une connexion à GitHub</span><span class="sxs-lookup"><span data-stu-id="28a1d-109">Create a connection to GitHub</span></span>
<span data-ttu-id="28a1d-110">Pour créer des applications logiques avec GitHub, vous devez d’abord créer une **connexion**, puis fournir les détails pour les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="28a1d-110">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="28a1d-111">Propriété</span><span class="sxs-lookup"><span data-stu-id="28a1d-111">Property</span></span> | <span data-ttu-id="28a1d-112">Requis</span><span class="sxs-lookup"><span data-stu-id="28a1d-112">Required</span></span> | <span data-ttu-id="28a1d-113">Description</span><span class="sxs-lookup"><span data-stu-id="28a1d-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28a1d-114">Jeton</span><span class="sxs-lookup"><span data-stu-id="28a1d-114">Token</span></span> |<span data-ttu-id="28a1d-115">Oui</span><span class="sxs-lookup"><span data-stu-id="28a1d-115">Yes</span></span> |<span data-ttu-id="28a1d-116">Fournir des informations d’identification GitHub</span><span class="sxs-lookup"><span data-stu-id="28a1d-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="28a1d-117">Après avoir créé la connexion, vous pouvez l’utiliser pour exécuter les actions et écouter les déclencheurs décrits dans cet article.</span><span class="sxs-lookup"><span data-stu-id="28a1d-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="28a1d-118">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="28a1d-118">Connector-specific details</span></span>

<span data-ttu-id="28a1d-119">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/github/).</span><span class="sxs-lookup"><span data-stu-id="28a1d-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="28a1d-120">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="28a1d-120">More connectors</span></span>
<span data-ttu-id="28a1d-121">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="28a1d-121">Go back to the [APIs list](apis-list.md).</span></span>