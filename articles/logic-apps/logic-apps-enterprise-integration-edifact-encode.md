---
title: Encoder des messages EDIFACT - Azure Logic Apps | Microsoft Docs
description: "Validation EDI et génération du code XML avec l’encodeur EDIFACT Message dans Enterprise Integration Pack pour Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b8d577326d23ec45cb4a9ec0e450ebf7afd945f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="283e7-103">Encoder des messages EDIFACT pour Azure Logic Apps avec Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="283e7-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="283e7-104">Avec le connecteur Encode EDIFACT Message, vous pouvez valider l’EDI et les propriétés spécifiques au partenaire, générer un document XML pour chaque document informatisé et demander un accusé de réception technique ou fonctionnel, ou les deux.</span><span class="sxs-lookup"><span data-stu-id="283e7-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="283e7-105">Pour utiliser ce connecteur, vous devez ajouter le connecteur à un déclencheur existant dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="283e7-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="283e7-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="283e7-106">Before you start</span></span>

<span data-ttu-id="283e7-107">Voici les éléments dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="283e7-107">Here's the items you need:</span></span>

* <span data-ttu-id="283e7-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="283e7-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="283e7-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="283e7-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="283e7-110">Vous devez disposer d’un compte d’intégration pour pouvoir utiliser le connecteur Encode EDIFACT Message.</span><span class="sxs-lookup"><span data-stu-id="283e7-110">You must have an integration account to use the Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="283e7-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="283e7-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="283e7-112">Un [contrat EDIFACT](logic-apps-enterprise-integration-edifact.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="283e7-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="283e7-113">Encoder des messages EDIFACT</span><span class="sxs-lookup"><span data-stu-id="283e7-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="283e7-114">[Créer une application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="283e7-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="283e7-115">Le connecteur Encode EDIFACT Message ne possède aucun déclencheur, ce qui signifie que vous devez ajouter un déclencheur pour le démarrage de votre application logique, par exemple un déclencheur de requête.</span><span class="sxs-lookup"><span data-stu-id="283e7-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="283e7-116">Dans le concepteur d’applications logiques, ajoutez un déclencheur, puis ajoutez une action à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="283e7-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="283e7-117">Dans la zone de recherche, entrez « EDIFACT » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="283e7-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="283e7-118">Sélectionnez **Encode EDIFACT Message par nom de contrat** ou **Encode to EDIFACT message par identités**.</span><span class="sxs-lookup"><span data-stu-id="283e7-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span></span>
   
    ![recherche EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="283e7-120">Si vous n’avez pas encore créé de connexions à votre compte d’intégration, vous êtes invité à le faire à cette étape.</span><span class="sxs-lookup"><span data-stu-id="283e7-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="283e7-121">Donnez un nom à votre connexion, puis sélectionnez le compte d’intégration auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="283e7-121">Name your connection, and select the integration account that you want to connect.</span></span>

    ![créer une connexion de compte d’intégration](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="283e7-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="283e7-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="283e7-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="283e7-124">Property</span></span> | <span data-ttu-id="283e7-125">Détails</span><span class="sxs-lookup"><span data-stu-id="283e7-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="283e7-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="283e7-126">Connection Name *</span></span> |<span data-ttu-id="283e7-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="283e7-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="283e7-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="283e7-128">Integration Account *</span></span> |<span data-ttu-id="283e7-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="283e7-129">Enter a name for your integration account.</span></span> <span data-ttu-id="283e7-130">Vérifiez que votre compte d’intégration et votre application logique se trouvent dans le même emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="283e7-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="283e7-131">Lorsque vous avez terminé, les détails de votre connexion doivent apparaître tels qu’indiqués dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="283e7-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="283e7-132">Pour terminer la création de votre connexion, sélectionnez l’option **Créer**.</span><span class="sxs-lookup"><span data-stu-id="283e7-132">To finish creating your connection, choose **Create**.</span></span>

    ![détails de connexion de compte d’intégration](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="283e7-134">Votre connexion est maintenant créée.</span><span class="sxs-lookup"><span data-stu-id="283e7-134">Your connection is now created.</span></span>

    ![connexion de compte d’intégration créée](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="283e7-136">Encode EDIFACT Message par nom de contrat</span><span class="sxs-lookup"><span data-stu-id="283e7-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="283e7-137">Si vous choisissez d’encoder des messages EDIFACT par nom du contrat, ouvrez la liste **Nom de l’accord EDIF**, et entrez ou sélectionnez votre nom de contrat EDIFACT existant.</span><span class="sxs-lookup"><span data-stu-id="283e7-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="283e7-138">Saisissez le message XML à encoder.</span><span class="sxs-lookup"><span data-stu-id="283e7-138">Enter the XML message to encode.</span></span>

![Indiquez le nom du contrat EDIFACT et le nom du message XML à encoder](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="283e7-140">Encode EDIFACT Message par identités</span><span class="sxs-lookup"><span data-stu-id="283e7-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="283e7-141">Si vous choisissez d’encoder des messages EDIFAC par identités, indiquez l’identificateur et le qualificateur de l’expéditeur ainsi que l’identificateur et le qualificateur du récepteur tels que configurés dans votre contrat EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="283e7-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="283e7-142">Sélectionnez le message XML à encoder.</span><span class="sxs-lookup"><span data-stu-id="283e7-142">Select the XML message to encode.</span></span>

![Renseigner les identités de l’expéditeur et du destinataire, sélectionner le message XML à encoder](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="283e7-144">Détails sur l’encodage EDIFACT</span><span class="sxs-lookup"><span data-stu-id="283e7-144">EDIFACT Encode details</span></span>

<span data-ttu-id="283e7-145">Le connecteur Encode EDIFACT effectue les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="283e7-145">The Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="283e7-146">Résout le contrat en mettant en correspondance les identificateurs et les qualificateurs de l’expéditeur et du récepteur</span><span class="sxs-lookup"><span data-stu-id="283e7-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="283e7-147">Sérialise l’échange EDI en convertissant les messages codés au format XML en documents informatisés EDI au sein de l’échange.</span><span class="sxs-lookup"><span data-stu-id="283e7-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="283e7-148">Applique les segments d’en-tête et de code de fin du document informatisé</span><span class="sxs-lookup"><span data-stu-id="283e7-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="283e7-149">Génère un numéro de contrôle d’échange, un numéro de contrôle de groupe et un numéro de contrôle de document informatisé pour chaque échange sortant</span><span class="sxs-lookup"><span data-stu-id="283e7-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="283e7-150">Remplace les séparateurs dans les données de charge utile</span><span class="sxs-lookup"><span data-stu-id="283e7-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="283e7-151">Valide l’EDI et les propriétés spécifiques au partenaire</span><span class="sxs-lookup"><span data-stu-id="283e7-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="283e7-152">Validation de schéma des éléments de données du document informatisé par rapport au schéma de message.</span><span class="sxs-lookup"><span data-stu-id="283e7-152">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="283e7-153">Validation EDI effectuée sur les éléments de données du document informatisé.</span><span class="sxs-lookup"><span data-stu-id="283e7-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="283e7-154">Validation étendue effectuée sur les éléments de données du document informatisé</span><span class="sxs-lookup"><span data-stu-id="283e7-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="283e7-155">Génère un document XML pour chaque document informatisé.</span><span class="sxs-lookup"><span data-stu-id="283e7-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="283e7-156">Demande un accusé de réception fonctionnel et/ou technique (si configuré).</span><span class="sxs-lookup"><span data-stu-id="283e7-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="283e7-157">En tant qu’accusé de réception technique, le message CONTRL indique la réception d’un échange.</span><span class="sxs-lookup"><span data-stu-id="283e7-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="283e7-158">En tant qu’accusé de réception fonctionnel, le message CONTRL indique l’acceptation ou le rejet du message, du groupe ou de l’échange reçu, en fournissant une liste des erreurs ou des fonctionnalités non prises en charge</span><span class="sxs-lookup"><span data-stu-id="283e7-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="283e7-159">Afficher le fichier Swagger</span><span class="sxs-lookup"><span data-stu-id="283e7-159">View Swagger file</span></span>
<span data-ttu-id="283e7-160">Pour afficher les détails Swagger du connecteur EDIFACT, consultez [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="283e7-160">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="283e7-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="283e7-161">Next steps</span></span>
[<span data-ttu-id="283e7-162">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="283e7-162">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack") 

