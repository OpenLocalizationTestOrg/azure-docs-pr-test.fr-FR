---
title: aaaAdd hello Twilio connecteur dans vos applications Azure logique | Documents Microsoft
description: "Vue d’ensemble de hello Twilio connecteur avec des paramètres de l’API REST"
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
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="a9574-103">Prise en main connecteur de Twilio hello</span><span class="sxs-lookup"><span data-stu-id="a9574-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="a9574-104">Se connecter tooTwilio toosend et recevoir des messages SMS et MMS IP globales.</span><span class="sxs-lookup"><span data-stu-id="a9574-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="a9574-105">Avec Twilio, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="a9574-105">With Twilio, you can:</span></span>

* <span data-ttu-id="a9574-106">Générer des flux de votre entreprise en fonction des données hello que vous obtenez à partir de Twilio.</span><span class="sxs-lookup"><span data-stu-id="a9574-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="a9574-107">Utiliser des actions pour obtenir un message, répertorier les messages, et plus encore.</span><span class="sxs-lookup"><span data-stu-id="a9574-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="a9574-108">Ces actions Obtient une réponse et puis disposition de sortie de hello pour d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="a9574-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="a9574-109">Par exemple, quand vous recevez un nouveau message Twilio, vous pouvez prendre ce message et l’utiliser comme flux de travail Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a9574-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="a9574-110">Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a9574-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="a9574-111">Créer un tooTwilio de connexion</span><span class="sxs-lookup"><span data-stu-id="a9574-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="a9574-112">Lorsque vous ajoutez ce connecteur tooyour les applications logique, entrez hello Twilio valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="a9574-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="a9574-113">Propriété</span><span class="sxs-lookup"><span data-stu-id="a9574-113">Property</span></span> | <span data-ttu-id="a9574-114">Requis</span><span class="sxs-lookup"><span data-stu-id="a9574-114">Required</span></span> | <span data-ttu-id="a9574-115">Description</span><span class="sxs-lookup"><span data-stu-id="a9574-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9574-116">ID de compte</span><span class="sxs-lookup"><span data-stu-id="a9574-116">Account ID</span></span> |<span data-ttu-id="a9574-117">Oui</span><span class="sxs-lookup"><span data-stu-id="a9574-117">Yes</span></span> |<span data-ttu-id="a9574-118">Entrez votre ID de compte Twilio</span><span class="sxs-lookup"><span data-stu-id="a9574-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="a9574-119">Jeton d'accès</span><span class="sxs-lookup"><span data-stu-id="a9574-119">Access Token</span></span> |<span data-ttu-id="a9574-120">Oui</span><span class="sxs-lookup"><span data-stu-id="a9574-120">Yes</span></span> |<span data-ttu-id="a9574-121">Entrez votre jeton d’accès Twilio</span><span class="sxs-lookup"><span data-stu-id="a9574-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="a9574-122">Si vous n’avez pas un jeton d’accès Twilio, consultez [Identité de l’utilisateur et jetons d’accès](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="a9574-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="a9574-123">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="a9574-123">Connector-specific details</span></span>

<span data-ttu-id="a9574-124">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="a9574-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="a9574-125">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="a9574-125">More connectors</span></span>
<span data-ttu-id="a9574-126">Revenir en arrière toohello [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a9574-126">Go back toohello [APIs list](apis-list.md).</span></span>
