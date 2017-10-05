---
title: "Ajouter le connecteur Twilio à vos applications logiques Azure | Microsoft Docs"
description: "Vue d’ensemble du connecteur Twilio avec les paramètres d’API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a790ac51b0fea7e3fa379d20e0e094e7ce0d7696
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twilio-connector"></a><span data-ttu-id="3924d-103">Prise en main du connecteur Twilio</span><span class="sxs-lookup"><span data-stu-id="3924d-103">Get started with the Twilio connector</span></span>
<span data-ttu-id="3924d-104">Connectez-vous à Twilio pour envoyer et recevoir des SMS, des MMS, et des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="3924d-104">Connect to Twilio to send and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="3924d-105">Avec Twilio, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="3924d-105">With Twilio, you can:</span></span>

* <span data-ttu-id="3924d-106">Créer votre flux d'activité en fonction des données que vous obtenez de Twilio.</span><span class="sxs-lookup"><span data-stu-id="3924d-106">Build your business flow based on the data you get from Twilio.</span></span> 
* <span data-ttu-id="3924d-107">Utiliser des actions pour obtenir un message, répertorier les messages, et plus encore.</span><span class="sxs-lookup"><span data-stu-id="3924d-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="3924d-108">Ces actions obtiennent une réponse, puis mettent la sortie à la disposition d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="3924d-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="3924d-109">Par exemple, quand vous recevez un nouveau message Twilio, vous pouvez prendre ce message et l’utiliser comme flux de travail Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3924d-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="3924d-110">Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3924d-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-twilio"></a><span data-ttu-id="3924d-111">Créer une connexion à Twilio</span><span class="sxs-lookup"><span data-stu-id="3924d-111">Create a connection to Twilio</span></span>
<span data-ttu-id="3924d-112">Quand vous ajoutez ce connecteur à vos applications logiques, entrez les valeurs Twilio suivantes :</span><span class="sxs-lookup"><span data-stu-id="3924d-112">When you add this Connector to your logic apps, enter the following Twilio values:</span></span>

| <span data-ttu-id="3924d-113">Propriété</span><span class="sxs-lookup"><span data-stu-id="3924d-113">Property</span></span> | <span data-ttu-id="3924d-114">Requis</span><span class="sxs-lookup"><span data-stu-id="3924d-114">Required</span></span> | <span data-ttu-id="3924d-115">Description</span><span class="sxs-lookup"><span data-stu-id="3924d-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3924d-116">ID de compte</span><span class="sxs-lookup"><span data-stu-id="3924d-116">Account ID</span></span> |<span data-ttu-id="3924d-117">Oui</span><span class="sxs-lookup"><span data-stu-id="3924d-117">Yes</span></span> |<span data-ttu-id="3924d-118">Entrez votre ID de compte Twilio</span><span class="sxs-lookup"><span data-stu-id="3924d-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="3924d-119">Jeton d'accès</span><span class="sxs-lookup"><span data-stu-id="3924d-119">Access Token</span></span> |<span data-ttu-id="3924d-120">Oui</span><span class="sxs-lookup"><span data-stu-id="3924d-120">Yes</span></span> |<span data-ttu-id="3924d-121">Entrez votre jeton d’accès Twilio</span><span class="sxs-lookup"><span data-stu-id="3924d-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps to create a connection to Twilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="3924d-122">Si vous n’avez pas un jeton d’accès Twilio, consultez [Identité de l’utilisateur et jetons d’accès](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="3924d-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="3924d-123">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="3924d-123">Connector-specific details</span></span>

<span data-ttu-id="3924d-124">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="3924d-124">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="3924d-125">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="3924d-125">More connectors</span></span>
<span data-ttu-id="3924d-126">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="3924d-126">Go back to the [APIs list](apis-list.md).</span></span>