---
title: messages aaaEncode AS2 - Azure Logic Apps | Documents Microsoft
description: Comment toouse hello encodeur AS2 Bonjour Enterprise Integration Pack pour Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="0fc61-103">Encoder les messages AS2 pour Azure Logic Apps avec hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="0fc61-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="0fc61-104">tooestablish sécurité et fiabilité lors de la transmission des messages, utilisez le connecteur de message AS2 d’encoder hello.</span><span class="sxs-lookup"><span data-stu-id="0fc61-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="0fc61-105">Ce connecteur fournit une signature numérique, le chiffrement et les accusés de réception par le biais des Notifications MDN (Message Disposition), ce qui entraîne également des toosupport de Non répudiation.</span><span class="sxs-lookup"><span data-stu-id="0fc61-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0fc61-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="0fc61-106">Before you start</span></span>

<span data-ttu-id="0fc61-107">Voici les éléments hello que vous devez :</span><span class="sxs-lookup"><span data-stu-id="0fc61-107">Here's hello items you need:</span></span>

* <span data-ttu-id="0fc61-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="0fc61-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="0fc61-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc61-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="0fc61-110">Vous devez disposer d’un connecteur de message AS2 d’encoder hello intégration compte toouse.</span><span class="sxs-lookup"><span data-stu-id="0fc61-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="0fc61-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="0fc61-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="0fc61-112">Un [contrat AS2](logic-apps-enterprise-integration-as2.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="0fc61-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="0fc61-113">Encoder des messages AS2</span><span class="sxs-lookup"><span data-stu-id="0fc61-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="0fc61-114">[Créer une application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0fc61-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="0fc61-115">connecteur de message AS2 d’encoder de Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande.</span><span class="sxs-lookup"><span data-stu-id="0fc61-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="0fc61-116">Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.</span><span class="sxs-lookup"><span data-stu-id="0fc61-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="0fc61-117">Dans la zone de recherche de hello, entrez « AS2 » pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="0fc61-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="0fc61-118">Sélectionnez **AS2 - Encode AS2 Message**.</span><span class="sxs-lookup"><span data-stu-id="0fc61-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Recherchez « AS2 »](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="0fc61-120">Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion.</span><span class="sxs-lookup"><span data-stu-id="0fc61-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="0fc61-121">Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect.</span><span class="sxs-lookup"><span data-stu-id="0fc61-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![créer le compte de connexion toointegration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="0fc61-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="0fc61-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="0fc61-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="0fc61-124">Property</span></span> | <span data-ttu-id="0fc61-125">Détails</span><span class="sxs-lookup"><span data-stu-id="0fc61-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="0fc61-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="0fc61-126">Connection Name *</span></span> |<span data-ttu-id="0fc61-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="0fc61-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="0fc61-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="0fc61-128">Integration Account *</span></span> |<span data-ttu-id="0fc61-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="0fc61-129">Enter a name for your integration account.</span></span> <span data-ttu-id="0fc61-130">Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="0fc61-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="0fc61-131">Lorsque vous avez terminé, les détails de votre connexion doivent ressembler exemple toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="0fc61-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="0fc61-132">toofinish création de votre connexion, choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="0fc61-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![détails de la connexion d’intégration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="0fc61-134">Une fois que votre connexion est créée, comme indiqué dans cet exemple, fournissez les informations relatives **AS2-de**, **AS2-tooidentifiers** tel que configuré dans votre contrat, et **corps**, qui est charge utile du message Hello.</span><span class="sxs-lookup"><span data-stu-id="0fc61-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![remplir les champs obligatoires](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="0fc61-136">Détails sur l’encodeur AS2</span><span class="sxs-lookup"><span data-stu-id="0fc61-136">AS2 encoder details</span></span>

<span data-ttu-id="0fc61-137">connecteur d’encoder un AS2 Hello effectue ces tâches :</span><span class="sxs-lookup"><span data-stu-id="0fc61-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="0fc61-138">Applique les en-têtes AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="0fc61-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="0fc61-139">Signe les messages sortants (si configuré)</span><span class="sxs-lookup"><span data-stu-id="0fc61-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="0fc61-140">Chiffre les messages sortants (si configuré)</span><span class="sxs-lookup"><span data-stu-id="0fc61-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="0fc61-141">Compresse le message de type hello (si configuré)</span><span class="sxs-lookup"><span data-stu-id="0fc61-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="0fc61-142">Testez cet exemple</span><span class="sxs-lookup"><span data-stu-id="0fc61-142">Try this sample</span></span>

<span data-ttu-id="0fc61-143">tootry déploiement d’un scénario de AS2 logique entièrement opérationnelle application et des exemples, consultez hello [AS2 scénario et du modèle d’application logique](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="0fc61-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="0fc61-144">Swagger hello de vue</span><span class="sxs-lookup"><span data-stu-id="0fc61-144">View hello swagger</span></span>
<span data-ttu-id="0fc61-145">Consultez hello [swagger détails](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="0fc61-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0fc61-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0fc61-146">Next steps</span></span>
[<span data-ttu-id="0fc61-147">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="0fc61-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise") 

