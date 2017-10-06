---
title: messages aaaDecode AS2 - Azure Logic Apps | Documents Microsoft
description: "Comment toouse hello décodeur AS2 dans hello Enterprise Integration Pack pour Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="d0d11-103">Décoder les messages AS2 pour Azure Logic Apps avec hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="d0d11-103">Decode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span> 

<span data-ttu-id="d0d11-104">tooestablish sécurité et fiabilité lors de la transmission des messages, utilisez le connecteur de message AS2 de décoder hello.</span><span class="sxs-lookup"><span data-stu-id="d0d11-104">tooestablish security and reliability while transmitting messages, use hello Decode AS2 message connector.</span></span> <span data-ttu-id="d0d11-105">Ce connecteur fournit des fonctionnalités de signature numérique, de cryptage et d’accusés de réception par vérification des notifications de messages (Message Disposition Notifications, MDN).</span><span class="sxs-lookup"><span data-stu-id="d0d11-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d0d11-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d0d11-106">Before you start</span></span>

<span data-ttu-id="d0d11-107">Voici les éléments hello que vous devez :</span><span class="sxs-lookup"><span data-stu-id="d0d11-107">Here's hello items you need:</span></span>

* <span data-ttu-id="d0d11-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="d0d11-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="d0d11-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d11-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="d0d11-110">Vous devez disposer d’un connecteur de message AS2 de décoder hello intégration compte toouse.</span><span class="sxs-lookup"><span data-stu-id="d0d11-110">You must have an integration account toouse hello Decode AS2 message connector.</span></span>
* <span data-ttu-id="d0d11-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="d0d11-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="d0d11-112">Un [contrat AS2](logic-apps-enterprise-integration-as2.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="d0d11-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="d0d11-113">Décoder des messages AS2</span><span class="sxs-lookup"><span data-stu-id="d0d11-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="d0d11-114">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d0d11-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="d0d11-115">connecteur de message AS2 de décoder de Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande.</span><span class="sxs-lookup"><span data-stu-id="d0d11-115">hello Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="d0d11-116">Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.</span><span class="sxs-lookup"><span data-stu-id="d0d11-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="d0d11-117">Dans la zone de recherche de hello, entrez « AS2 » pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="d0d11-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="d0d11-118">Sélectionnez **AS2 - Decode AS2 Message**.</span><span class="sxs-lookup"><span data-stu-id="d0d11-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Recherchez « AS2 »](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="d0d11-120">Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion.</span><span class="sxs-lookup"><span data-stu-id="d0d11-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="d0d11-121">Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d0d11-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Créer une connexion d’intégration](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="d0d11-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="d0d11-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="d0d11-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="d0d11-124">Property</span></span> | <span data-ttu-id="d0d11-125">Détails</span><span class="sxs-lookup"><span data-stu-id="d0d11-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="d0d11-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="d0d11-126">Connection Name *</span></span> |<span data-ttu-id="d0d11-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="d0d11-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="d0d11-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="d0d11-128">Integration Account *</span></span> |<span data-ttu-id="d0d11-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="d0d11-129">Enter a name for your integration account.</span></span> <span data-ttu-id="d0d11-130">Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="d0d11-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="d0d11-131">Lorsque vous avez terminé, les détails de votre connexion doivent ressembler exemple toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="d0d11-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="d0d11-132">toofinish création de votre connexion, choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="d0d11-132">toofinish creating your connection, choose **Create**.</span></span>

    ![détails de la connexion d’intégration](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="d0d11-134">Une fois que votre connexion est créée, comme indiqué dans cet exemple, sélectionnez **corps** et **en-têtes** à partir de hello demander des sorties.</span><span class="sxs-lookup"><span data-stu-id="d0d11-134">After your connection is created, as shown in this example, select **Body** and **Headers** from hello Request outputs.</span></span>
   
    ![connexion d’intégration créée](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="d0d11-136">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d0d11-136">For example:</span></span>

    ![Sélectionnez le corps et les en-têtes à partir des sorties de requête.](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="d0d11-138">Détails sur le décodeur AS2</span><span class="sxs-lookup"><span data-stu-id="d0d11-138">AS2 decoder details</span></span>

<span data-ttu-id="d0d11-139">connecteur de décoder les AS2 Hello effectue ces tâches :</span><span class="sxs-lookup"><span data-stu-id="d0d11-139">hello Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="d0d11-140">Traite les en-têtes AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="d0d11-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="d0d11-141">Vérifie la signature de hello (si configuré)</span><span class="sxs-lookup"><span data-stu-id="d0d11-141">Verifies hello signature (if configured)</span></span>
* <span data-ttu-id="d0d11-142">Déchiffre les messages de type hello (si configuré)</span><span class="sxs-lookup"><span data-stu-id="d0d11-142">Decrypts hello messages (if configured)</span></span>
* <span data-ttu-id="d0d11-143">Décompresse le message de type hello (si configuré)</span><span class="sxs-lookup"><span data-stu-id="d0d11-143">Decompresses hello message (if configured)</span></span>
* <span data-ttu-id="d0d11-144">Rapproche un MDN reçu avec le message sortant original de hello</span><span class="sxs-lookup"><span data-stu-id="d0d11-144">Reconciles a received MDN with hello original outbound message</span></span>
* <span data-ttu-id="d0d11-145">Met à jour et met en corrélation les enregistrements dans la base de données de non-répudiation hello</span><span class="sxs-lookup"><span data-stu-id="d0d11-145">Updates and correlates records in hello non-repudiation database</span></span>
* <span data-ttu-id="d0d11-146">Écrit les enregistrements pour le rapport d’état AS2</span><span class="sxs-lookup"><span data-stu-id="d0d11-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="d0d11-147">contenu de charge utile de sortie Hello est codées en base64</span><span class="sxs-lookup"><span data-stu-id="d0d11-147">hello output payload contents are base64 encoded</span></span>
* <span data-ttu-id="d0d11-148">Détermine si un MDN est requis et si hello MDN doit être synchrone ou asynchrone basée sur la configuration dans l’accord AS2</span><span class="sxs-lookup"><span data-stu-id="d0d11-148">Determines whether an MDN is required, and whether hello MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="d0d11-149">Génère un MDN synchrone ou asynchrone (basé sur les configurations de l’accord)</span><span class="sxs-lookup"><span data-stu-id="d0d11-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="d0d11-150">Définit les propriétés et les jetons de corrélation hello sur hello MDN</span><span class="sxs-lookup"><span data-stu-id="d0d11-150">Sets hello correlation tokens and properties on hello MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="d0d11-151">Testez cet exemple</span><span class="sxs-lookup"><span data-stu-id="d0d11-151">Try this sample</span></span>

<span data-ttu-id="d0d11-152">tootry déploiement d’un scénario de AS2 logique entièrement opérationnelle application et des exemples, consultez hello [AS2 scénario et du modèle d’application logique](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="d0d11-152">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="d0d11-153">Swagger hello de vue</span><span class="sxs-lookup"><span data-stu-id="d0d11-153">View hello swagger</span></span>
<span data-ttu-id="d0d11-154">Consultez hello [swagger détails](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="d0d11-154">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d0d11-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d0d11-155">Next steps</span></span>
[<span data-ttu-id="d0d11-156">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="d0d11-156">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

