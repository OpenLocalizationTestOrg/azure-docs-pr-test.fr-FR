---
title: Encoder des messages X12 - Azure Logic Apps | Microsoft Docs
description: "Valider des documents EDI et convertir des messages encodés en XML avec l’encodeur de messages X12 dans Enterprise Integration Pack pour Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 29d19364b9a98e351c95f13e68a2e63b9f6439f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="bb9cf-103">Encodez des messages X12 pour Azure Logic Apps avec Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="bb9cf-103">Encode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="bb9cf-104">Avec le connecteur Encode X12 Message, vous pouvez valider l’EDI et les propriétés spécifiques au partenaire, convertir des messages codés au format XML en documents informatisés EDI au sein de l’échange, et demander un accusé de réception technique et/ou fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="bb9cf-105">Pour utiliser ce connecteur, vous devez ajouter le connecteur à un déclencheur existant dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="bb9cf-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="bb9cf-106">Before you start</span></span>

<span data-ttu-id="bb9cf-107">Voici les éléments dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="bb9cf-107">Here's the items you need:</span></span>

* <span data-ttu-id="bb9cf-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="bb9cf-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="bb9cf-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="bb9cf-110">Vous devez disposer d’un compte d’intégration pour pouvoir utiliser le connecteur Encode X12 Message.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-110">You must have an integration account to use the Encode X12 message connector.</span></span>
* <span data-ttu-id="bb9cf-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="bb9cf-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="bb9cf-112">Un [contrat X12](logic-apps-enterprise-integration-x12.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="bb9cf-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="bb9cf-113">Encoder des messages X12</span><span class="sxs-lookup"><span data-stu-id="bb9cf-113">Encode X12 messages</span></span>

1. <span data-ttu-id="bb9cf-114">[Créer une application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="bb9cf-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="bb9cf-115">Le connecteur Encode X12 Message ne possède aucun déclencheur, ce qui signifie que vous devez ajouter un déclencheur pour le démarrage de votre application logique, par exemple un déclencheur de requête.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="bb9cf-116">Dans le concepteur d’applications logiques, ajoutez un déclencheur, puis ajoutez une action à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="bb9cf-117">Dans la zone de recherche, entrez le filtre « x12 ».</span><span class="sxs-lookup"><span data-stu-id="bb9cf-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="bb9cf-118">Sélectionnez **X12 - Encode X12 Message par nom de contrat** ou **X12 - Encode to X 12 message par identités**.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span></span>
   
    ![Recherchez « x12 »](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="bb9cf-120">Si vous n’avez pas encore créé de connexions à votre compte d’intégration, vous êtes invité à le faire à cette étape.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="bb9cf-121">Donnez un nom à votre connexion, puis sélectionnez le compte d’intégration auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![connexion de compte d’intégration](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="bb9cf-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="bb9cf-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="bb9cf-124">Property</span></span> | <span data-ttu-id="bb9cf-125">Détails</span><span class="sxs-lookup"><span data-stu-id="bb9cf-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="bb9cf-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="bb9cf-126">Connection Name *</span></span> |<span data-ttu-id="bb9cf-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="bb9cf-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="bb9cf-128">Integration Account *</span></span> |<span data-ttu-id="bb9cf-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-129">Enter a name for your integration account.</span></span> <span data-ttu-id="bb9cf-130">Vérifiez que votre compte d’intégration et votre application logique se trouvent dans le même emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="bb9cf-131">Lorsque vous avez terminé, les détails de votre connexion doivent apparaître tels qu’indiqués dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="bb9cf-132">Pour terminer la création de votre connexion, sélectionnez l’option **Créer**.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-132">To finish creating your connection, choose **Create**.</span></span>

    ![connexion de compte d’intégration créée](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="bb9cf-134">Votre connexion est maintenant créée.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-134">Your connection is now created.</span></span>

    ![détails de connexion de compte d’intégration](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="bb9cf-136">Encode X12 message par nom de contrat</span><span class="sxs-lookup"><span data-stu-id="bb9cf-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="bb9cf-137">Si vous choisissez d’encoder des messages X12 par nom du contrat, ouvrez la liste **Nom de l’accord X12**, entrez ou sélectionnez votre contrat X12 existant.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="bb9cf-138">Saisissez le message XML à encoder.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-138">Enter the XML message to encode.</span></span>

![Entrez le nom du contrat X12 et le nom du message XML à encoder](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="bb9cf-140">Encode X12 message par identités</span><span class="sxs-lookup"><span data-stu-id="bb9cf-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="bb9cf-141">Si vous choisissez d’encoder des messages X12 par identités, indiquez l’identificateur et le qualificateur de l’expéditeur ainsi que l’identificateur et le qualificateur du récepteur tels que configurés dans votre contrat X12.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="bb9cf-142">Sélectionnez le message XML à encoder.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-142">Select the XML message to encode.</span></span>
   
![Renseigner les identités de l’expéditeur et du destinataire, sélectionner le message XML à encoder](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="bb9cf-144">Détails sur X12 Encode</span><span class="sxs-lookup"><span data-stu-id="bb9cf-144">X12 Encode details</span></span>

<span data-ttu-id="bb9cf-145">Le connecteur X12 Encode effectue les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb9cf-145">The X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="bb9cf-146">Résolution du contrat en faisant correspondre les propriétés de contexte de l’expéditeur et du récepteur.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="bb9cf-147">Sérialise l’échange EDI en convertissant les messages codés au format XML en documents informatisés EDI au sein de l’échange.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="bb9cf-148">Applique les segments d’en-tête et de code de fin du document informatisé</span><span class="sxs-lookup"><span data-stu-id="bb9cf-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="bb9cf-149">Génère un numéro de contrôle d’échange, un numéro de contrôle de groupe et un numéro de contrôle de document informatisé pour chaque échange sortant</span><span class="sxs-lookup"><span data-stu-id="bb9cf-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="bb9cf-150">Remplace les séparateurs dans les données de charge utile</span><span class="sxs-lookup"><span data-stu-id="bb9cf-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="bb9cf-151">Valide l’EDI et les propriétés spécifiques au partenaire</span><span class="sxs-lookup"><span data-stu-id="bb9cf-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="bb9cf-152">Validation de schéma des éléments de données du document informatisé par rapport au schéma de message</span><span class="sxs-lookup"><span data-stu-id="bb9cf-152">Schema validation of the transaction-set data elements against the message Schema</span></span>
  * <span data-ttu-id="bb9cf-153">Validation EDI effectuée sur les éléments de données du document informatisé.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="bb9cf-154">Validation étendue effectuée sur les éléments de données du document informatisé</span><span class="sxs-lookup"><span data-stu-id="bb9cf-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="bb9cf-155">Demande un accusé de réception fonctionnel et/ou technique (si configuré).</span><span class="sxs-lookup"><span data-stu-id="bb9cf-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="bb9cf-156">Suite à la validation de l’en-tête, un accusé de réception technique est généré.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="bb9cf-157">L’accusé de réception technique renvoie l’état du traitement de l’en-tête et du code de fin d’un échange par le récepteur de l’adresse</span><span class="sxs-lookup"><span data-stu-id="bb9cf-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span></span>
  * <span data-ttu-id="bb9cf-158">Suite à la validation du corps, un accusé de réception fonctionnel est généré.</span><span class="sxs-lookup"><span data-stu-id="bb9cf-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="bb9cf-159">L’accusé de réception fonctionnel signale chaque erreur rencontrée lors du traitement du document reçu</span><span class="sxs-lookup"><span data-stu-id="bb9cf-159">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="bb9cf-160">Afficher Swagger</span><span class="sxs-lookup"><span data-stu-id="bb9cf-160">View the swagger</span></span>
<span data-ttu-id="bb9cf-161">Consultez les [détails sur Swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="bb9cf-161">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bb9cf-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bb9cf-162">Next steps</span></span>
[<span data-ttu-id="bb9cf-163">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="bb9cf-163">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack") 

