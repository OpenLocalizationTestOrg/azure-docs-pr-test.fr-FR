---
title: Encoder des messages AS2 - Azure Logic Apps | Microsoft Docs
description: "Comment utiliser l’encodeur AS2 dans Enterprise Integration Pack pour Azure Logic Apps"
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
ms.openlocfilehash: 7889bf9e4e02143b6bb4c797531afa54f8647ce5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="88fc3-103">Encodez des messages AS2 pour Azure Logic Apps avec Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="88fc3-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="88fc3-104">Utilisez le connecteur Encode AS2 Message pour créer des conditions de transmission de messages à la fois sûres et fiables.</span><span class="sxs-lookup"><span data-stu-id="88fc3-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span></span> <span data-ttu-id="88fc3-105">Ce connecteur fournit des fonctionnalités de signature numérique, de cryptage et d’accusés de réception par vérification des notifications de messages (Message Disposition Notifications, MDN), ce qui renforce par ailleurs la non-répudiation.</span><span class="sxs-lookup"><span data-stu-id="88fc3-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="88fc3-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="88fc3-106">Before you start</span></span>

<span data-ttu-id="88fc3-107">Voici les éléments dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="88fc3-107">Here's the items you need:</span></span>

* <span data-ttu-id="88fc3-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="88fc3-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="88fc3-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="88fc3-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="88fc3-110">Vous devez disposer d’un compte d’intégration pour pouvoir utiliser le connecteur Encode AS2 Message.</span><span class="sxs-lookup"><span data-stu-id="88fc3-110">You must have an integration account to use the Encode AS2 message connector.</span></span>
* <span data-ttu-id="88fc3-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="88fc3-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="88fc3-112">Un [contrat AS2](logic-apps-enterprise-integration-as2.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="88fc3-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="88fc3-113">Encoder des messages AS2</span><span class="sxs-lookup"><span data-stu-id="88fc3-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="88fc3-114">[Créer une application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="88fc3-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="88fc3-115">Le connecteur Encode AS2 Message ne possède aucun déclencheur, ce qui signifie que vous devez ajouter un déclencheur pour le démarrage de votre application logique, par exemple un déclencheur de requête.</span><span class="sxs-lookup"><span data-stu-id="88fc3-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="88fc3-116">Dans le concepteur d’applications logiques, ajoutez un déclencheur, puis ajoutez une action à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="88fc3-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="88fc3-117">Dans la zone de recherche, entrez le filtre « AS2 ».</span><span class="sxs-lookup"><span data-stu-id="88fc3-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="88fc3-118">Sélectionnez **AS2 - Encode AS2 Message**.</span><span class="sxs-lookup"><span data-stu-id="88fc3-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Recherchez « AS2 »](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="88fc3-120">Si vous n’avez pas encore créé de connexions à votre compte d’intégration, vous êtes invité à le faire à cette étape.</span><span class="sxs-lookup"><span data-stu-id="88fc3-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="88fc3-121">Donnez un nom à votre connexion, puis sélectionnez le compte d’intégration auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="88fc3-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![Créer une connexion de compte d’intégration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="88fc3-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="88fc3-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="88fc3-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="88fc3-124">Property</span></span> | <span data-ttu-id="88fc3-125">Détails</span><span class="sxs-lookup"><span data-stu-id="88fc3-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="88fc3-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="88fc3-126">Connection Name *</span></span> |<span data-ttu-id="88fc3-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="88fc3-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="88fc3-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="88fc3-128">Integration Account *</span></span> |<span data-ttu-id="88fc3-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="88fc3-129">Enter a name for your integration account.</span></span> <span data-ttu-id="88fc3-130">Vérifiez que votre compte d’intégration et votre application logique se trouvent dans le même emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="88fc3-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="88fc3-131">Lorsque vous avez terminé, les détails de votre connexion doivent apparaître tels qu’indiqués dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="88fc3-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="88fc3-132">Pour terminer la création de votre connexion, sélectionnez l’option **Créer**.</span><span class="sxs-lookup"><span data-stu-id="88fc3-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![détails de la connexion d’intégration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="88fc3-134">Une fois que votre connexion est créée, comme indiqué dans cet exemple, renseignez les informations des champs **AS2-From**, **AS2-To** (comme configuré dans votre contrat) et **Corps**, qui correspond à la charge utile du message.</span><span class="sxs-lookup"><span data-stu-id="88fc3-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span></span>
   
    ![remplir les champs obligatoires](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="88fc3-136">Détails sur l’encodeur AS2</span><span class="sxs-lookup"><span data-stu-id="88fc3-136">AS2 encoder details</span></span>

<span data-ttu-id="88fc3-137">Le connecteur Encode AS2 effectue les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="88fc3-137">The Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="88fc3-138">Applique les en-têtes AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="88fc3-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="88fc3-139">Signe les messages sortants (si configuré)</span><span class="sxs-lookup"><span data-stu-id="88fc3-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="88fc3-140">Chiffre les messages sortants (si configuré)</span><span class="sxs-lookup"><span data-stu-id="88fc3-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="88fc3-141">Compresse le message (si configuré)</span><span class="sxs-lookup"><span data-stu-id="88fc3-141">Compresses the message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="88fc3-142">Testez cet exemple</span><span class="sxs-lookup"><span data-stu-id="88fc3-142">Try this sample</span></span>

<span data-ttu-id="88fc3-143">Pour déployer une application logique totalement opérationnelle dans le cadre d’un exemple de scénario AS2, consultez le [scénario et le modèle d’application logique AS2](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="88fc3-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="88fc3-144">Afficher Swagger</span><span class="sxs-lookup"><span data-stu-id="88fc3-144">View the swagger</span></span>
<span data-ttu-id="88fc3-145">Consultez les [détails sur Swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="88fc3-145">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="88fc3-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="88fc3-146">Next steps</span></span>
[<span data-ttu-id="88fc3-147">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="88fc3-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack") 

