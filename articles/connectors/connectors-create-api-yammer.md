---
title: "Ajouter le connecteur Yammer à vos applications logiques Azure | Microsoft Docs"
description: "Vue d’ensemble du connecteur Yammer avec les paramètres d’API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c7a213343b4fb2b5a89a5052a459061b404a431c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-yammer-connector"></a><span data-ttu-id="e1948-103">Prise en main du connecteur Yammer</span><span class="sxs-lookup"><span data-stu-id="e1948-103">Get started with the Yammer connector</span></span>
<span data-ttu-id="e1948-104">Connectez-vous à Yammer pour accéder aux conversations dans votre réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="e1948-104">Connect to Yammer to access conversations in your enterprise network.</span></span> <span data-ttu-id="e1948-105">Avec Yammer, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1948-105">With Yammer, you can:</span></span>

* <span data-ttu-id="e1948-106">Créer votre flux d’activité en fonction des données que vous obtenez de Yammer.</span><span class="sxs-lookup"><span data-stu-id="e1948-106">Build your business flow based on the data you get from Yammer.</span></span> 
* <span data-ttu-id="e1948-107">Utiliser des déclencheurs quand un nouveau message arrive dans un groupe ou un flux que vous suivez.</span><span class="sxs-lookup"><span data-stu-id="e1948-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="e1948-108">Utiliser des actions pour publier un message, obtenir tous les messages et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="e1948-108">Use actions to post a message, get all messages, and more.</span></span> <span data-ttu-id="e1948-109">Ces actions obtiennent une réponse, puis mettent la sortie à la disposition d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="e1948-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="e1948-110">Par exemple, quand un nouveau message apparaît, vous pouvez envoyer un message électronique à l’aide d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="e1948-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="e1948-111">Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e1948-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-yammer"></a><span data-ttu-id="e1948-112">Créer une connexion à Yammer</span><span class="sxs-lookup"><span data-stu-id="e1948-112">Create a connection to Yammer</span></span>
<span data-ttu-id="e1948-113">Pour utiliser le connecteur Yammer, vous devez créer une **connexion**, puis fournir les détails de ces propriétés :</span><span class="sxs-lookup"><span data-stu-id="e1948-113">To use the Yammer connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="e1948-114">Propriété</span><span class="sxs-lookup"><span data-stu-id="e1948-114">Property</span></span> | <span data-ttu-id="e1948-115">Requis</span><span class="sxs-lookup"><span data-stu-id="e1948-115">Required</span></span> | <span data-ttu-id="e1948-116">Description</span><span class="sxs-lookup"><span data-stu-id="e1948-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1948-117">Jeton</span><span class="sxs-lookup"><span data-stu-id="e1948-117">Token</span></span> |<span data-ttu-id="e1948-118">Oui</span><span class="sxs-lookup"><span data-stu-id="e1948-118">Yes</span></span> |<span data-ttu-id="e1948-119">Indiquez les informations d’identification Yammer.</span><span class="sxs-lookup"><span data-stu-id="e1948-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to Yammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="e1948-120">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="e1948-120">Connector-specific details</span></span>

<span data-ttu-id="e1948-121">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/yammer/).</span><span class="sxs-lookup"><span data-stu-id="e1948-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e1948-122">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="e1948-122">More connectors</span></span>
<span data-ttu-id="e1948-123">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e1948-123">Go back to the [APIs list](apis-list.md).</span></span>