---
title: Connecteur Wunderlist dans Azure Logic Apps | Microsoft Docs
description: "Créez une connexion à Wunderlist et utilisez cette connexion pour générer votre flux de travail dans les applications logiques."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e4773ecf-3ad3-44b4-a1b5-ee5f58baeadd
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 899110992cc52ca5edf1706320fd5570473de784
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-wunderlist-connector"></a><span data-ttu-id="d8ed0-103">Prise en main du connecteur Wunderlist</span><span class="sxs-lookup"><span data-stu-id="d8ed0-103">Get started with the Wunderlist connector</span></span>
<span data-ttu-id="d8ed0-104">Wunderlist fournit un gestionnaire de tâches et de listes de tâches pour aider les utilisateurs à travailler efficacement.</span><span class="sxs-lookup"><span data-stu-id="d8ed0-104">Wunderlist provide a todo list and task manager to help people get their stuff done.</span></span>  <span data-ttu-id="d8ed0-105">Si vous partagez une liste de courses avec un proche, si vous travaillez sur un projet ou planifiez des vacances, Wunderlist facilite la capture, le partage et le suivi de vos listes de tâches.</span><span class="sxs-lookup"><span data-stu-id="d8ed0-105">Whether you’re sharing a grocery list with a loved one, working on a project, or planning a vacation, Wunderlist makes it easy to capture, share, and complete your to¬dos.</span></span> <span data-ttu-id="d8ed0-106">Wunderlist est instantanément synchronisé entre votre téléphone, votre tablette et votre ordinateur, pour vous permettre d’accéder à toutes vos tâches à partir de n’importe quel endroit.</span><span class="sxs-lookup"><span data-stu-id="d8ed0-106">Wunderlist instantly syncs between your phone, tablet and computer, so you can access all your tasks from anywhere.</span></span>

<span data-ttu-id="d8ed0-107">Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d8ed0-107">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-wunderlist"></a><span data-ttu-id="d8ed0-108">Créer une connexion à Wunderlist</span><span class="sxs-lookup"><span data-stu-id="d8ed0-108">Create a connection to Wunderlist</span></span>
<span data-ttu-id="d8ed0-109">Pour créer des applications logiques avec Wunderlist, vous devez d’abord créer une **connexion**, puis fournir les détails pour les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="d8ed0-109">To create Logic apps with Wunderlist, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="d8ed0-110">Propriété</span><span class="sxs-lookup"><span data-stu-id="d8ed0-110">Property</span></span> | <span data-ttu-id="d8ed0-111">Requis</span><span class="sxs-lookup"><span data-stu-id="d8ed0-111">Required</span></span> | <span data-ttu-id="d8ed0-112">Description</span><span class="sxs-lookup"><span data-stu-id="d8ed0-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d8ed0-113">Jeton</span><span class="sxs-lookup"><span data-stu-id="d8ed0-113">Token</span></span> |<span data-ttu-id="d8ed0-114">Oui</span><span class="sxs-lookup"><span data-stu-id="d8ed0-114">Yes</span></span> |<span data-ttu-id="d8ed0-115">Fournir des informations d’identification Wunderlist</span><span class="sxs-lookup"><span data-stu-id="d8ed0-115">Provide Wunderlist Credentials</span></span> |

<span data-ttu-id="d8ed0-116">Après avoir créé la connexion, vous pouvez l’utiliser pour exécuter les actions et écouter les déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="d8ed0-116">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Wunderlist](../../includes/connectors-create-api-wunderlist.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="d8ed0-117">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="d8ed0-117">Connector-specific details</span></span>

<span data-ttu-id="d8ed0-118">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/wunderlist/).</span><span class="sxs-lookup"><span data-stu-id="d8ed0-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/wunderlist/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d8ed0-119">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="d8ed0-119">More connectors</span></span>
<span data-ttu-id="d8ed0-120">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d8ed0-120">Go back to the [APIs list](apis-list.md).</span></span>