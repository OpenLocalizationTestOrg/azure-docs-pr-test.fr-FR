---
title: "Décoder des messages X12 - Azure Logic Apps | Microsoft Docs"
description: "Valider l’EDI et générer les acquittements avec le décodeur de messages X12 dans Enterprise Integration Pack pour Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 18719a8f49c74973947517161f7306c233a9323f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="a77c4-103">Décodez des messages X12 pour Azure Logic Apps avec Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a77c4-103">Decode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="a77c4-104">Avec le connecteur de messages Decode X12, vous pouvez valider l’enveloppe en fonction d’un accord de partenariat commercial, valider l’EDI et les propriétés spécifiques du partenaire, fractionner des échanges en documents informatisés ou conserver les échanges entiers et générer des acquittements pour les transactions traitées.</span><span class="sxs-lookup"><span data-stu-id="a77c4-104">With the Decode X12 message connector, you can validate the envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="a77c4-105">Pour utiliser ce connecteur, vous devez ajouter le connecteur à un déclencheur existant dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="a77c4-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a77c4-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a77c4-106">Before you start</span></span>

<span data-ttu-id="a77c4-107">Voici les éléments dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="a77c4-107">Here's the items you need:</span></span>

* <span data-ttu-id="a77c4-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="a77c4-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="a77c4-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a77c4-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="a77c4-110">Vous devez disposer d’un compte d’intégration pour pouvoir utiliser le connecteur Decode X12 Message.</span><span class="sxs-lookup"><span data-stu-id="a77c4-110">You must have an integration account to use the Decode X12 message connector.</span></span>
* <span data-ttu-id="a77c4-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="a77c4-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="a77c4-112">Un [contrat X12](logic-apps-enterprise-integration-x12.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="a77c4-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="a77c4-113">Décoder des messages X12</span><span class="sxs-lookup"><span data-stu-id="a77c4-113">Decode X12 messages</span></span>

1. <span data-ttu-id="a77c4-114">[Créer une application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a77c4-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="a77c4-115">Le connecteur Decode X12 Message ne possède aucun déclencheur, ce qui signifie que vous devez ajouter un déclencheur pour le démarrage de votre application logique, par exemple un déclencheur de requête.</span><span class="sxs-lookup"><span data-stu-id="a77c4-115">The Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="a77c4-116">Dans le concepteur d’applications logiques, ajoutez un déclencheur, puis ajoutez une action à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="a77c4-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="a77c4-117">Dans la zone de recherche, entrez le filtre « x12 ».</span><span class="sxs-lookup"><span data-stu-id="a77c4-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="a77c4-118">Sélectionnez **X12 – Decode X12 Message**.</span><span class="sxs-lookup"><span data-stu-id="a77c4-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Recherchez « x12 »](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="a77c4-120">Si vous n’avez pas encore créé de connexions à votre compte d’intégration, vous êtes invité à le faire à cette étape.</span><span class="sxs-lookup"><span data-stu-id="a77c4-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="a77c4-121">Donnez un nom à votre connexion, puis sélectionnez le compte d’intégration auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="a77c4-121">Name your connection, and select the integration account that you want to connect.</span></span> 

    ![Fournir les détails de connexion de compte d’intégration](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="a77c4-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="a77c4-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="a77c4-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="a77c4-124">Property</span></span> | <span data-ttu-id="a77c4-125">Détails</span><span class="sxs-lookup"><span data-stu-id="a77c4-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="a77c4-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="a77c4-126">Connection Name *</span></span> |<span data-ttu-id="a77c4-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="a77c4-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="a77c4-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="a77c4-128">Integration Account *</span></span> |<span data-ttu-id="a77c4-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="a77c4-129">Enter a name for your integration account.</span></span> <span data-ttu-id="a77c4-130">Vérifiez que votre compte d’intégration et votre application logique se trouvent dans le même emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="a77c4-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="a77c4-131">Lorsque vous avez terminé, les détails de votre connexion doivent apparaître tels qu’indiqués dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="a77c4-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="a77c4-132">Pour terminer la création de votre connexion, sélectionnez l’option **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a77c4-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![détails de connexion de compte d’intégration](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="a77c4-134">Une fois votre connexion est créée, comme indiqué dans cet exemple, sélectionnez le message de fichier plat X12 à décoder.</span><span class="sxs-lookup"><span data-stu-id="a77c4-134">After your connection is created, as shown in this example, select the X12 flat file message to decode.</span></span>

    ![connexion de compte d’intégration créée](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="a77c4-136">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a77c4-136">For example:</span></span>

    ![Sélectionner le message de fichier plat X12 à décoder](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="a77c4-138">Informations sur X12 Decode</span><span class="sxs-lookup"><span data-stu-id="a77c4-138">X12 Decode details</span></span>

<span data-ttu-id="a77c4-139">Le connecteur X12 Decode effectue les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="a77c4-139">The X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="a77c4-140">Valide l’enveloppe par rapport au contrat de partenariat commercial</span><span class="sxs-lookup"><span data-stu-id="a77c4-140">Validates the envelope against trading partner agreement</span></span>
* <span data-ttu-id="a77c4-141">Valide l’EDI et les propriétés spécifiques au partenaire</span><span class="sxs-lookup"><span data-stu-id="a77c4-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="a77c4-142">Validation de la structure EDI et validation du schéma étendue</span><span class="sxs-lookup"><span data-stu-id="a77c4-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="a77c4-143">Validation de la structure de l’enveloppe d’échange.</span><span class="sxs-lookup"><span data-stu-id="a77c4-143">Validation of the structure of the interchange envelope.</span></span>
  * <span data-ttu-id="a77c4-144">Validation de schéma de l’enveloppe par rapport au schéma de contrôle.</span><span class="sxs-lookup"><span data-stu-id="a77c4-144">Schema validation of the envelope against the control schema.</span></span>
  * <span data-ttu-id="a77c4-145">Validation de schéma des éléments de données du document informatisé par rapport au schéma de message.</span><span class="sxs-lookup"><span data-stu-id="a77c4-145">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="a77c4-146">Validation EDI effectuée sur les éléments de données du document informatisé.</span><span class="sxs-lookup"><span data-stu-id="a77c4-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="a77c4-147">Vérifie que les numéros de contrôle de l’échange, du groupe et du document informatisé ne sont pas des doublons.</span><span class="sxs-lookup"><span data-stu-id="a77c4-147">Verifies that the interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="a77c4-148">Vérifie le numéro de contrôle de l’échange par rapport aux échanges reçus précédemment.</span><span class="sxs-lookup"><span data-stu-id="a77c4-148">Checks the interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="a77c4-149">Vérifie le numéro de contrôle du groupe par rapport aux autres numéros de contrôle de groupe dans l’échange.</span><span class="sxs-lookup"><span data-stu-id="a77c4-149">Checks the group control number against other group control numbers in the interchange.</span></span>
  * <span data-ttu-id="a77c4-150">Vérifie le numéro de contrôle du document informatisé par rapport aux autres numéros de contrôle de document informatisé dans ce groupe.</span><span class="sxs-lookup"><span data-stu-id="a77c4-150">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="a77c4-151">Fractionne l’échange en documents informatisés ou conserve l’échange entier :</span><span class="sxs-lookup"><span data-stu-id="a77c4-151">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="a77c4-152">Scinder l’échange en documents informatisés : suspendre les documents informatisés en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé.</span><span class="sxs-lookup"><span data-stu-id="a77c4-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="a77c4-153">L’action X12 Decode ne génère que les documents informatisés qui échouent à la validation `badMessages` et produit les documents informatisés restants en tant que `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="a77c4-153">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="a77c4-154">Scinder l’échange en documents informatisés : suspendre l’échange en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé.</span><span class="sxs-lookup"><span data-stu-id="a77c4-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="a77c4-155">Si la validation d’un ou de plusieurs documents informatisés de l’échange échoue, l’action X12 Decode génère tous les documents informatisés dans cet échange en tant que `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="a77c4-155">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="a77c4-156">Préserver l'échange : suspendre les documents informatisés en cas d'erreur : conserve l’échange et traite l’intégralité de l’échange par lot.</span><span class="sxs-lookup"><span data-stu-id="a77c4-156">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="a77c4-157">L’action X12 Decode ne génère que les documents informatisés qui échouent à la validation `badMessages` et produit les documents informatisés restants en tant que `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="a77c4-157">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="a77c4-158">Préserver l’échange : suspendre l’échange en cas d’erreur : conserve l’échange et traite l’intégralité de l’échange par lot.</span><span class="sxs-lookup"><span data-stu-id="a77c4-158">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="a77c4-159">Si la validation d’un ou de plusieurs documents informatisés de l’échange échoue, l’action X12 Decode génère tous les documents informatisés dans cet échange en tant que `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="a77c4-159">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span> 
* <span data-ttu-id="a77c4-160">Génère un accusé de réception fonctionnel et/ou technique (si configuré).</span><span class="sxs-lookup"><span data-stu-id="a77c4-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="a77c4-161">Suite à la validation de l’en-tête, un accusé de réception technique est généré.</span><span class="sxs-lookup"><span data-stu-id="a77c4-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="a77c4-162">L’accusé de réception technique renvoie l’état du traitement de l’en-tête et du code de fin d’un échange par le récepteur de l’adresse.</span><span class="sxs-lookup"><span data-stu-id="a77c4-162">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver.</span></span>
  * <span data-ttu-id="a77c4-163">Suite à la validation du corps, un accusé de réception fonctionnel est généré.</span><span class="sxs-lookup"><span data-stu-id="a77c4-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="a77c4-164">L’accusé de réception fonctionnel signale chaque erreur rencontrée lors du traitement du document reçu</span><span class="sxs-lookup"><span data-stu-id="a77c4-164">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="a77c4-165">Afficher Swagger</span><span class="sxs-lookup"><span data-stu-id="a77c4-165">View the swagger</span></span>
<span data-ttu-id="a77c4-166">Consultez les [détails sur Swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="a77c4-166">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a77c4-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a77c4-167">Next steps</span></span>
[<span data-ttu-id="a77c4-168">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a77c4-168">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack") 

