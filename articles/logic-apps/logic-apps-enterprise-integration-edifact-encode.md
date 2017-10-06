---
title: les messages EDIFACT aaaEncode - Azure Logic Apps | Documents Microsoft
description: "Valider EDI et de générer du code XML avec l’encodeur de message EDIFACT Bonjour Enterprise Integration Pack pour Azure Logic Apps"
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
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="4978a-103">Encoder les messages EDIFACT pour Azure Logic Apps avec hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="4978a-103">Encode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="4978a-104">Avec le connecteur de message EDIFACT d’encoder hello, vous pouvez valider EDI et des propriétés spécifiques aux partenaires, générer un document XML pour chaque document informatisé et demander un accusé de réception technique, l’accusé de réception fonctionnel ou les deux.</span><span class="sxs-lookup"><span data-stu-id="4978a-104">With hello Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="4978a-105">toouse ce connecteur, vous devez ajouter tooan de connecteur hello existant déclencheur dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="4978a-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4978a-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4978a-106">Before you start</span></span>

<span data-ttu-id="4978a-107">Voici les éléments hello que vous devez :</span><span class="sxs-lookup"><span data-stu-id="4978a-107">Here's hello items you need:</span></span>

* <span data-ttu-id="4978a-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="4978a-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="4978a-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4978a-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="4978a-110">Vous devez disposer d’un connecteur de message EDIFACT d’encoder hello intégration compte toouse.</span><span class="sxs-lookup"><span data-stu-id="4978a-110">You must have an integration account toouse hello Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="4978a-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="4978a-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="4978a-112">Un [contrat EDIFACT](logic-apps-enterprise-integration-edifact.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="4978a-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="4978a-113">Encoder des messages EDIFACT</span><span class="sxs-lookup"><span data-stu-id="4978a-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="4978a-114">[Créer une application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4978a-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="4978a-115">connecteur de message EDIFACT d’encoder de Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande.</span><span class="sxs-lookup"><span data-stu-id="4978a-115">hello Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="4978a-116">Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.</span><span class="sxs-lookup"><span data-stu-id="4978a-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="4978a-117">Dans la zone de recherche de hello, entrez « EDIFACT » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="4978a-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="4978a-118">Sélectionnez **encoder le Message EDIFACT par nom de l’accord** ou **Encode tooEDIFACT message identités**.</span><span class="sxs-lookup"><span data-stu-id="4978a-118">Select either **Encode EDIFACT Message by agreement name** or **Encode tooEDIFACT message by identities**.</span></span>
   
    ![recherche EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="4978a-120">Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion.</span><span class="sxs-lookup"><span data-stu-id="4978a-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="4978a-121">Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4978a-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>

    ![créer une connexion de compte d’intégration](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="4978a-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="4978a-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="4978a-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="4978a-124">Property</span></span> | <span data-ttu-id="4978a-125">Détails</span><span class="sxs-lookup"><span data-stu-id="4978a-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="4978a-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="4978a-126">Connection Name *</span></span> |<span data-ttu-id="4978a-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="4978a-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="4978a-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="4978a-128">Integration Account *</span></span> |<span data-ttu-id="4978a-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="4978a-129">Enter a name for your integration account.</span></span> <span data-ttu-id="4978a-130">Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="4978a-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="4978a-131">Lorsque vous avez terminé, les détails de votre connexion doivent ressembler exemple toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="4978a-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="4978a-132">toofinish création de votre connexion, choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="4978a-132">toofinish creating your connection, choose **Create**.</span></span>

    ![détails de connexion de compte d’intégration](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="4978a-134">Votre connexion est maintenant créée.</span><span class="sxs-lookup"><span data-stu-id="4978a-134">Your connection is now created.</span></span>

    ![connexion de compte d’intégration créée](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="4978a-136">Encode EDIFACT Message par nom de contrat</span><span class="sxs-lookup"><span data-stu-id="4978a-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="4978a-137">Si vous choisissez des messages EDIFACT tooencode par le nom de l’accord, ouvrez hello **accord nom de EDIFACT** liste, entrez ou sélectionnez le nom de votre accord EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="4978a-137">If you chose tooencode EDIFACT messages by agreement name, open hello **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="4978a-138">Entrez tooencode de message XML hello.</span><span class="sxs-lookup"><span data-stu-id="4978a-138">Enter hello XML message tooencode.</span></span>

![Entrez le nom de l’accord EDIFACT et tooencode de message XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="4978a-140">Encode EDIFACT Message par identités</span><span class="sxs-lookup"><span data-stu-id="4978a-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="4978a-141">Si vous choisissez des messages EDIFACT tooencode par des identités, entrez l’identificateur de l’expéditeur hello, qualificateur de l’expéditeur, identificateur du récepteur et qualificateur du récepteur tel que configuré dans votre accord EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="4978a-141">If you choose tooencode EDIFACT messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="4978a-142">Sélectionnez tooencode de message XML hello.</span><span class="sxs-lookup"><span data-stu-id="4978a-142">Select hello XML message tooencode.</span></span>

![Fournir des identités d’expéditeur et récepteur, sélectionnez tooencode de message XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="4978a-144">Détails sur l’encodage EDIFACT</span><span class="sxs-lookup"><span data-stu-id="4978a-144">EDIFACT Encode details</span></span>

<span data-ttu-id="4978a-145">connecteur d’encoder un EDIFACT Hello effectue ces tâches :</span><span class="sxs-lookup"><span data-stu-id="4978a-145">hello Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="4978a-146">Accord de hello en hello expéditeur qualificateur et identificateur et qualificateur du récepteur et l’identificateur de correspondance</span><span class="sxs-lookup"><span data-stu-id="4978a-146">Resolve hello agreement by matching hello sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="4978a-147">Sérialise l’échange EDI de hello, convertir des messages encodés en XML dans les documents informatisés dans l’échange de hello.</span><span class="sxs-lookup"><span data-stu-id="4978a-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="4978a-148">Applique les segments d’en-tête et de code de fin du document informatisé</span><span class="sxs-lookup"><span data-stu-id="4978a-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="4978a-149">Génère un numéro de contrôle d’échange, un numéro de contrôle de groupe et un numéro de contrôle de document informatisé pour chaque échange sortant</span><span class="sxs-lookup"><span data-stu-id="4978a-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="4978a-150">Remplace les séparateurs dans les données de charge utile de hello</span><span class="sxs-lookup"><span data-stu-id="4978a-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="4978a-151">Valide l’EDI et les propriétés spécifiques au partenaire</span><span class="sxs-lookup"><span data-stu-id="4978a-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="4978a-152">Validation du schéma des éléments de données de document informatisé hello contre le schéma de message hello.</span><span class="sxs-lookup"><span data-stu-id="4978a-152">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="4978a-153">Validation EDI effectuée sur les éléments de données du document informatisé.</span><span class="sxs-lookup"><span data-stu-id="4978a-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="4978a-154">Validation étendue effectuée sur les éléments de données du document informatisé</span><span class="sxs-lookup"><span data-stu-id="4978a-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="4978a-155">Génère un document XML pour chaque document informatisé.</span><span class="sxs-lookup"><span data-stu-id="4978a-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="4978a-156">Demande un accusé de réception fonctionnel et/ou technique (si configuré).</span><span class="sxs-lookup"><span data-stu-id="4978a-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="4978a-157">En tant qu’un accusé de réception technique, message de type hello CONTRL indique la réception d’un échange.</span><span class="sxs-lookup"><span data-stu-id="4978a-157">As a technical acknowledgment, hello CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="4978a-158">Comme un accusé de réception fonctionnel, message de type hello CONTRL indique l’acceptation ou rejet de l’échange de salutation reçue, groupe ou les messages, avec une liste d’erreurs ou des fonctionnalités non prises en charge</span><span class="sxs-lookup"><span data-stu-id="4978a-158">As a functional acknowledgment, hello CONTRL message indicates acceptance or rejection of hello received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="4978a-159">Afficher le fichier Swagger</span><span class="sxs-lookup"><span data-stu-id="4978a-159">View Swagger file</span></span>
<span data-ttu-id="4978a-160">Détails de Swagger tooview hello pour le connecteur d’EDIFACT hello, consultez [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="4978a-160">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4978a-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4978a-161">Next steps</span></span>
[<span data-ttu-id="4978a-162">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="4978a-162">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise") 

