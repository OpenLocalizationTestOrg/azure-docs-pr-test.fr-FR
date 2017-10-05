---
title: "Décoder des messages AS2 - Azure Logic Apps | Microsoft Docs"
description: "Comment utiliser le décodeur AS2 dans Enterprise Integration Pack pour Azure Logic Apps"
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
ms.openlocfilehash: a7920b2509fe368c6f7d55e17fe0bf0020c4562c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="87bcc-103">Décoder des messages AS2 pour Azure Logic Apps avec Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="87bcc-103">Decode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span> 

<span data-ttu-id="87bcc-104">Utilisez le connecteur Decode AS2 Message pour créer des conditions de transmission de messages à la fois sûres et fiables.</span><span class="sxs-lookup"><span data-stu-id="87bcc-104">To establish security and reliability while transmitting messages, use the Decode AS2 message connector.</span></span> <span data-ttu-id="87bcc-105">Ce connecteur fournit des fonctionnalités de signature numérique, de cryptage et d’accusés de réception par vérification des notifications de messages (Message Disposition Notifications, MDN).</span><span class="sxs-lookup"><span data-stu-id="87bcc-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="87bcc-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="87bcc-106">Before you start</span></span>

<span data-ttu-id="87bcc-107">Voici les éléments dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="87bcc-107">Here's the items you need:</span></span>

* <span data-ttu-id="87bcc-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="87bcc-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="87bcc-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="87bcc-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="87bcc-110">Vous devez disposer d’un compte d’intégration pour pouvoir utiliser le connecteur Decode AS2 Message.</span><span class="sxs-lookup"><span data-stu-id="87bcc-110">You must have an integration account to use the Decode AS2 message connector.</span></span>
* <span data-ttu-id="87bcc-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="87bcc-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="87bcc-112">Un [contrat AS2](logic-apps-enterprise-integration-as2.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="87bcc-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="87bcc-113">Décoder des messages AS2</span><span class="sxs-lookup"><span data-stu-id="87bcc-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="87bcc-114">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="87bcc-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="87bcc-115">Le connecteur Decode AS2 Message ne possède aucun déclencheur, ce qui signifie que vous devez ajouter un déclencheur pour le démarrage de votre application logique, par exemple un déclencheur de requête.</span><span class="sxs-lookup"><span data-stu-id="87bcc-115">The Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="87bcc-116">Dans le concepteur d’applications logiques, ajoutez un déclencheur, puis ajoutez une action à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="87bcc-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="87bcc-117">Dans la zone de recherche, entrez le filtre « AS2 ».</span><span class="sxs-lookup"><span data-stu-id="87bcc-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="87bcc-118">Sélectionnez **AS2 - Decode AS2 Message**.</span><span class="sxs-lookup"><span data-stu-id="87bcc-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Recherchez « AS2 »](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="87bcc-120">Si vous n’avez pas encore créé de connexions à votre compte d’intégration, vous êtes invité à le faire à cette étape.</span><span class="sxs-lookup"><span data-stu-id="87bcc-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="87bcc-121">Donnez un nom à votre connexion, puis sélectionnez le compte d’intégration auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="87bcc-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![Créer une connexion d’intégration](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="87bcc-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="87bcc-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="87bcc-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="87bcc-124">Property</span></span> | <span data-ttu-id="87bcc-125">Détails</span><span class="sxs-lookup"><span data-stu-id="87bcc-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="87bcc-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="87bcc-126">Connection Name *</span></span> |<span data-ttu-id="87bcc-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="87bcc-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="87bcc-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="87bcc-128">Integration Account *</span></span> |<span data-ttu-id="87bcc-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="87bcc-129">Enter a name for your integration account.</span></span> <span data-ttu-id="87bcc-130">Vérifiez que votre compte d’intégration et votre application logique se trouvent dans le même emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="87bcc-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="87bcc-131">Lorsque vous avez terminé, les détails de votre connexion doivent apparaître tels qu’indiqués dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="87bcc-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="87bcc-132">Pour terminer la création de votre connexion, sélectionnez l’option **Créer**.</span><span class="sxs-lookup"><span data-stu-id="87bcc-132">To finish creating your connection, choose **Create**.</span></span>

    ![détails de la connexion d’intégration](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="87bcc-134">Une fois votre connexion créée, comme indiqué dans cet exemple, sélectionnez le **corps** et les **en-têtes** des sorties de requête.</span><span class="sxs-lookup"><span data-stu-id="87bcc-134">After your connection is created, as shown in this example, select **Body** and **Headers** from the Request outputs.</span></span>
   
    ![connexion d’intégration créée](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="87bcc-136">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="87bcc-136">For example:</span></span>

    ![Sélectionnez le corps et les en-têtes à partir des sorties de requête.](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="87bcc-138">Détails sur le décodeur AS2</span><span class="sxs-lookup"><span data-stu-id="87bcc-138">AS2 decoder details</span></span>

<span data-ttu-id="87bcc-139">Le connecteur Decode AS2 effectue les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="87bcc-139">The Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="87bcc-140">Traite les en-têtes AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="87bcc-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="87bcc-141">Vérifie la signature (si configuré)</span><span class="sxs-lookup"><span data-stu-id="87bcc-141">Verifies the signature (if configured)</span></span>
* <span data-ttu-id="87bcc-142">Déchiffre les messages (si configuré)</span><span class="sxs-lookup"><span data-stu-id="87bcc-142">Decrypts the messages (if configured)</span></span>
* <span data-ttu-id="87bcc-143">Compresse le message (si configuré)</span><span class="sxs-lookup"><span data-stu-id="87bcc-143">Decompresses the message (if configured)</span></span>
* <span data-ttu-id="87bcc-144">Rapproche un MDN reçu avec le message sortant d’origine</span><span class="sxs-lookup"><span data-stu-id="87bcc-144">Reconciles a received MDN with the original outbound message</span></span>
* <span data-ttu-id="87bcc-145">Met à jour et met en corrélation les enregistrements dans la base de données de non-répudiation</span><span class="sxs-lookup"><span data-stu-id="87bcc-145">Updates and correlates records in the non-repudiation database</span></span>
* <span data-ttu-id="87bcc-146">Écrit les enregistrements pour le rapport d’état AS2</span><span class="sxs-lookup"><span data-stu-id="87bcc-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="87bcc-147">Les contenus de charge utile de sortie sont codés en base64</span><span class="sxs-lookup"><span data-stu-id="87bcc-147">The output payload contents are base64 encoded</span></span>
* <span data-ttu-id="87bcc-148">Détermine si un MDN est requis et si le MDN doit être synchrone ou asynchrone d’après la configuration dans l’accord AS2</span><span class="sxs-lookup"><span data-stu-id="87bcc-148">Determines whether an MDN is required, and whether the MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="87bcc-149">Génère un MDN synchrone ou asynchrone (basé sur les configurations de l’accord)</span><span class="sxs-lookup"><span data-stu-id="87bcc-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="87bcc-150">Définit les propriétés et les jetons de corrélation sur le MDN</span><span class="sxs-lookup"><span data-stu-id="87bcc-150">Sets the correlation tokens and properties on the MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="87bcc-151">Testez cet exemple</span><span class="sxs-lookup"><span data-stu-id="87bcc-151">Try this sample</span></span>

<span data-ttu-id="87bcc-152">Pour déployer une application logique totalement opérationnelle dans le cadre d’un exemple de scénario AS2, consultez le [scénario et le modèle d’application logique AS2](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="87bcc-152">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="87bcc-153">Afficher Swagger</span><span class="sxs-lookup"><span data-stu-id="87bcc-153">View the swagger</span></span>
<span data-ttu-id="87bcc-154">Consultez les [détails sur Swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="87bcc-154">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="87bcc-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87bcc-155">Next steps</span></span>
[<span data-ttu-id="87bcc-156">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="87bcc-156">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

