---
title: "Décoder des messages EDIFACT - Azure Logic Apps | Microsoft Docs"
description: "Valider l’EDI et générer les accusés de réception avec le décodeur de messages EDIFACT dans Enterprise Integration Pack pour Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e3787b48037360bf6066ddce2bacba6842213b2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="bc21c-103">Décodez des messages EDIFACT pour Azure Logic Apps avec Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="bc21c-103">Decode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="bc21c-104">Avec le connecteur de messages Decode EDIFACT, vous pouvez valider l’EDI et les propriétés spécifiques du partenaire, fractionner des échanges en documents informatisés ou conserver les échanges entiers et générer des accusés de réception pour les transactions traitées.</span><span class="sxs-lookup"><span data-stu-id="bc21c-104">With the Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="bc21c-105">Pour utiliser ce connecteur, vous devez ajouter le connecteur à un déclencheur existant dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="bc21c-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="bc21c-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="bc21c-106">Before you start</span></span>

<span data-ttu-id="bc21c-107">Voici les éléments dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="bc21c-107">Here's the items you need:</span></span>

* <span data-ttu-id="bc21c-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="bc21c-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="bc21c-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="bc21c-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="bc21c-110">Vous devez disposer d’un compte d’intégration pour pouvoir utiliser le connecteur Decode EDIFACT Message.</span><span class="sxs-lookup"><span data-stu-id="bc21c-110">You must have an integration account to use the Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="bc21c-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="bc21c-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="bc21c-112">Un [contrat EDIFACT](logic-apps-enterprise-integration-edifact.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="bc21c-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="bc21c-113">Messages Decode EDIFACT</span><span class="sxs-lookup"><span data-stu-id="bc21c-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="bc21c-114">[Créer une application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="bc21c-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="bc21c-115">Le connecteur Decode EDIFACT Message ne possède aucun déclencheur, ce qui signifie que vous devez ajouter un déclencheur pour le démarrage de votre application logique, par exemple un déclencheur de requête.</span><span class="sxs-lookup"><span data-stu-id="bc21c-115">The Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="bc21c-116">Dans le concepteur d’applications logiques, ajoutez un déclencheur, puis ajoutez une action à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="bc21c-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3. <span data-ttu-id="bc21c-117">Dans la zone de recherche, entrez « EDIFACT » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="bc21c-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="bc21c-118">Sélectionnez **Decode EDIFACT Message**.</span><span class="sxs-lookup"><span data-stu-id="bc21c-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![recherche EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="bc21c-120">Si vous n’avez pas encore créé de connexions à votre compte d’intégration, vous êtes invité à le faire à cette étape.</span><span class="sxs-lookup"><span data-stu-id="bc21c-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="bc21c-121">Donnez un nom à votre connexion, puis sélectionnez le compte d’intégration auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="bc21c-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![créer un compte d’intégration](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="bc21c-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="bc21c-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="bc21c-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="bc21c-124">Property</span></span> | <span data-ttu-id="bc21c-125">Détails</span><span class="sxs-lookup"><span data-stu-id="bc21c-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="bc21c-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="bc21c-126">Connection Name *</span></span> |<span data-ttu-id="bc21c-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="bc21c-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="bc21c-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="bc21c-128">Integration Account *</span></span> |<span data-ttu-id="bc21c-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="bc21c-129">Enter a name for your integration account.</span></span> <span data-ttu-id="bc21c-130">Vérifiez que votre compte d’intégration et votre application logique se trouvent dans le même emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="bc21c-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

4. <span data-ttu-id="bc21c-131">Pour terminer la création de votre connexion, sélectionnez l’option **Créer**.</span><span class="sxs-lookup"><span data-stu-id="bc21c-131">When you're done to finish creating your connection, choose **Create**.</span></span> <span data-ttu-id="bc21c-132">Les détails de votre connexion doivent apparaître tels qu’indiqués dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bc21c-132">Your connection details should look similar to this example:</span></span>

    ![détails du compte d’intégration](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="bc21c-134">Une fois votre connexion est créée, comme indiqué dans cet exemple, sélectionnez le message de fichier plat EDIFACT à décoder.</span><span class="sxs-lookup"><span data-stu-id="bc21c-134">After your connection is created, as shown in this example, select the EDIFACT flat file message to decode.</span></span>

    ![connexion de compte d’intégration créée](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="bc21c-136">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="bc21c-136">For example:</span></span>

    ![Sélectionner le message de fichier plat EDIFACT à décoder](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="bc21c-138">Détails sur le décodeur EDIFACT</span><span class="sxs-lookup"><span data-stu-id="bc21c-138">EDIFACT decoder details</span></span>

<span data-ttu-id="bc21c-139">Le connecteur Decode EDIFACT effectue les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="bc21c-139">The Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="bc21c-140">Valide l’enveloppe par rapport à l’accord de partenariat commercial.</span><span class="sxs-lookup"><span data-stu-id="bc21c-140">Validates the envelope against trading partner agreement.</span></span>
* <span data-ttu-id="bc21c-141">Résout l’accord en mettant en correspondance les identificateurs et les qualificateurs de l’expéditeur et du récepteur.</span><span class="sxs-lookup"><span data-stu-id="bc21c-141">Resolves the agreement by matching the sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="bc21c-142">Fractionne un échange en plusieurs transactions lorsque l’échange a plusieurs transactions basées sur la configuration des paramètres de réception de l’accord.</span><span class="sxs-lookup"><span data-stu-id="bc21c-142">Splits an interchange into multiple transactions when the interchange has more than one transaction based on the agreement's receive settings configuration.</span></span>
* <span data-ttu-id="bc21c-143">Désassemble l’échange.</span><span class="sxs-lookup"><span data-stu-id="bc21c-143">Disassembles the interchange.</span></span>
* <span data-ttu-id="bc21c-144">Valide l’EDI et les propriétés spécifiques du partenaire, y compris :</span><span class="sxs-lookup"><span data-stu-id="bc21c-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="bc21c-145">Validation de la structure de l’enveloppe d’échange</span><span class="sxs-lookup"><span data-stu-id="bc21c-145">Validation of the interchange envelope structure</span></span>
  * <span data-ttu-id="bc21c-146">Validation de schéma de l’enveloppe par rapport au schéma de contrôle</span><span class="sxs-lookup"><span data-stu-id="bc21c-146">Schema validation of the envelope against the control schema</span></span>
  * <span data-ttu-id="bc21c-147">Validation de schéma des éléments de données du document informatisé par rapport au schéma de message</span><span class="sxs-lookup"><span data-stu-id="bc21c-147">Schema validation of the transaction-set data elements against the message schema</span></span>
  * <span data-ttu-id="bc21c-148">Validation EDI effectuée sur les éléments de données du document informatisé.</span><span class="sxs-lookup"><span data-stu-id="bc21c-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="bc21c-149">Vérifie que les numéros de contrôle de l’échange, du groupe et du document informatisé ne sont pas des doublons (si configuré)</span><span class="sxs-lookup"><span data-stu-id="bc21c-149">Verifies that the interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="bc21c-150">Vérifie le numéro de contrôle de l’échange par rapport aux échanges reçus précédemment.</span><span class="sxs-lookup"><span data-stu-id="bc21c-150">Checks the interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="bc21c-151">Vérifie le numéro de contrôle du groupe par rapport aux autres numéros de contrôle de groupe dans l’échange.</span><span class="sxs-lookup"><span data-stu-id="bc21c-151">Checks the group control number against other group control numbers in the interchange.</span></span> 
  * <span data-ttu-id="bc21c-152">Vérifie le numéro de contrôle du document informatisé par rapport aux autres numéros de contrôle de document informatisé dans ce groupe.</span><span class="sxs-lookup"><span data-stu-id="bc21c-152">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="bc21c-153">Fractionne l’échange en documents informatisés ou conserve l’échange entier :</span><span class="sxs-lookup"><span data-stu-id="bc21c-153">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="bc21c-154">Scinder l’échange en documents informatisés : suspendre les documents informatisés en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé.</span><span class="sxs-lookup"><span data-stu-id="bc21c-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="bc21c-155">L’action X12 Decode ne génère que les documents informatisés qui échouent à la validation `badMessages` et produit les documents informatisés restants en tant que `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="bc21c-155">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="bc21c-156">Scinder l’échange en documents informatisés : suspendre l’échange en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé.</span><span class="sxs-lookup"><span data-stu-id="bc21c-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="bc21c-157">Si la validation d’un ou de plusieurs documents informatisés de l’échange échoue, l’action X12 Decode génère tous les documents informatisés dans cet échange en tant que `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="bc21c-157">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="bc21c-158">Préserver l'échange : suspendre les documents informatisés en cas d'erreur : conserve l’échange et traite l’intégralité de l’échange par lot.</span><span class="sxs-lookup"><span data-stu-id="bc21c-158">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="bc21c-159">L’action X12 Decode ne génère que les documents informatisés qui échouent à la validation `badMessages` et produit les documents informatisés restants en tant que `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="bc21c-159">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="bc21c-160">Préserver l’échange : suspendre l’échange en cas d’erreur : conserve l’échange et traite l’intégralité de l’échange par lot.</span><span class="sxs-lookup"><span data-stu-id="bc21c-160">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="bc21c-161">Si la validation d’un ou de plusieurs documents informatisés de l’échange échoue, l’action X12 Decode génère tous les documents informatisés dans cet échange en tant que `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="bc21c-161">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
* <span data-ttu-id="bc21c-162">Génère un accusé de réception fonctionnel et/ou technique (contrôle) (si configuré).</span><span class="sxs-lookup"><span data-stu-id="bc21c-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="bc21c-163">Un accusé de réception technique ou l’ACK CONTRL renvoie les résultats d’une vérification syntaxique de tout l’échange reçu.</span><span class="sxs-lookup"><span data-stu-id="bc21c-163">A Technical Acknowledgment or the CONTRL ACK reports the results of a syntactical check of the complete received interchange.</span></span>
  * <span data-ttu-id="bc21c-164">Un accusé de réception fonctionnel accuse réception de l’acceptation ou du refus d’un groupe ou d’un échange reçu</span><span class="sxs-lookup"><span data-stu-id="bc21c-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="bc21c-165">Afficher le fichier Swagger</span><span class="sxs-lookup"><span data-stu-id="bc21c-165">View Swagger file</span></span>
<span data-ttu-id="bc21c-166">Pour afficher les détails Swagger du connecteur EDIFACT, consultez [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="bc21c-166">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc21c-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc21c-167">Next steps</span></span>
[<span data-ttu-id="bc21c-168">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="bc21c-168">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack") 

