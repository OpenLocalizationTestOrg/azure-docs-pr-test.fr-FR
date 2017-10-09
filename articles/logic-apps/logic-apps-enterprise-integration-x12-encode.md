---
title: messages aaaEncode X12 - Azure Logic Apps | Documents Microsoft
description: "Validation EDI et convertir encodé en XML messages avec X12 message encodeur Bonjour Enterprise Integration Pack pour Azure Logic Apps"
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
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="743db-103">Encoder X12 messages pour Azure Logic Apps avec hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="743db-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="743db-104">Avec le connecteur de message hello Encode X12, vous pouvez valider EDI et des propriétés spécifiques aux partenaires, convertir des messages encodés en XML en documents informatisés dans l’échange de hello et demander un accusé de réception technique, l’accusé de réception fonctionnel ou les deux.</span><span class="sxs-lookup"><span data-stu-id="743db-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="743db-105">toouse ce connecteur, vous devez ajouter tooan de connecteur hello existant déclencheur dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="743db-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="743db-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="743db-106">Before you start</span></span>

<span data-ttu-id="743db-107">Voici les éléments hello que vous devez :</span><span class="sxs-lookup"><span data-stu-id="743db-107">Here's hello items you need:</span></span>

* <span data-ttu-id="743db-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="743db-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="743db-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="743db-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="743db-110">Vous devez disposer d’un connecteur d’intégration compte toouse hello Encode X12 message.</span><span class="sxs-lookup"><span data-stu-id="743db-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="743db-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="743db-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="743db-112">Un [contrat X12](logic-apps-enterprise-integration-x12.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="743db-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="743db-113">Encoder des messages X12</span><span class="sxs-lookup"><span data-stu-id="743db-113">Encode X12 messages</span></span>

1. <span data-ttu-id="743db-114">[Créer une application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="743db-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="743db-115">connecteur de message d’encodage X12 Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande.</span><span class="sxs-lookup"><span data-stu-id="743db-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="743db-116">Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.</span><span class="sxs-lookup"><span data-stu-id="743db-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="743db-117">Dans la zone de recherche de hello, entrez « x12 » pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="743db-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="743db-118">Sélectionnez **X12-Encoder tooX12 message par le nom de l’accord** ou **X12-Encoder tooX12 message par identités**.</span><span class="sxs-lookup"><span data-stu-id="743db-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    ![Recherchez « x12 »](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="743db-120">Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion.</span><span class="sxs-lookup"><span data-stu-id="743db-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="743db-121">Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect.</span><span class="sxs-lookup"><span data-stu-id="743db-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![connexion de compte d’intégration](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="743db-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="743db-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="743db-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="743db-124">Property</span></span> | <span data-ttu-id="743db-125">Détails</span><span class="sxs-lookup"><span data-stu-id="743db-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="743db-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="743db-126">Connection Name *</span></span> |<span data-ttu-id="743db-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="743db-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="743db-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="743db-128">Integration Account *</span></span> |<span data-ttu-id="743db-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="743db-129">Enter a name for your integration account.</span></span> <span data-ttu-id="743db-130">Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="743db-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="743db-131">Lorsque vous avez terminé, les détails de votre connexion doivent ressembler exemple toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="743db-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="743db-132">toofinish création de votre connexion, choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="743db-132">toofinish creating your connection, choose **Create**.</span></span>

    ![connexion de compte d’intégration créée](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="743db-134">Votre connexion est maintenant créée.</span><span class="sxs-lookup"><span data-stu-id="743db-134">Your connection is now created.</span></span>

    ![détails de connexion de compte d’intégration](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="743db-136">Encode X12 message par nom de contrat</span><span class="sxs-lookup"><span data-stu-id="743db-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="743db-137">Si vous avez choisi de messages de tooencode X12 par le nom de l’accord, ouvrez hello **nom de X12 accord** liste, entrez ou sélectionnez votre X12 existant accord.</span><span class="sxs-lookup"><span data-stu-id="743db-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="743db-138">Entrez tooencode de message XML hello.</span><span class="sxs-lookup"><span data-stu-id="743db-138">Enter hello XML message tooencode.</span></span>

![Entrez X12 tooencode de message XML et le nom de contrat](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="743db-140">Encode X12 message par identités</span><span class="sxs-lookup"><span data-stu-id="743db-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="743db-141">Si vous choisissez les messages tooencode X12 d’identités, entrez identificateur de l’expéditeur hello, qualificateur de l’expéditeur, identificateur du récepteur et qualificateur du récepteur tel que configuré dans votre X12 accord.</span><span class="sxs-lookup"><span data-stu-id="743db-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="743db-142">Sélectionnez tooencode de message XML hello.</span><span class="sxs-lookup"><span data-stu-id="743db-142">Select hello XML message tooencode.</span></span>
   
![Fournir des identités d’expéditeur et récepteur, sélectionnez tooencode de message XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="743db-144">Détails sur X12 Encode</span><span class="sxs-lookup"><span data-stu-id="743db-144">X12 Encode details</span></span>

<span data-ttu-id="743db-145">connecteur d’encodage Hello X12 effectue ces tâches :</span><span class="sxs-lookup"><span data-stu-id="743db-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="743db-146">Résolution du contrat en faisant correspondre les propriétés de contexte de l’expéditeur et du récepteur.</span><span class="sxs-lookup"><span data-stu-id="743db-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="743db-147">Sérialise l’échange EDI de hello, convertir des messages encodés en XML dans les documents informatisés dans l’échange de hello.</span><span class="sxs-lookup"><span data-stu-id="743db-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="743db-148">Applique les segments d’en-tête et de code de fin du document informatisé</span><span class="sxs-lookup"><span data-stu-id="743db-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="743db-149">Génère un numéro de contrôle d’échange, un numéro de contrôle de groupe et un numéro de contrôle de document informatisé pour chaque échange sortant</span><span class="sxs-lookup"><span data-stu-id="743db-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="743db-150">Remplace les séparateurs dans les données de charge utile de hello</span><span class="sxs-lookup"><span data-stu-id="743db-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="743db-151">Valide l’EDI et les propriétés spécifiques au partenaire</span><span class="sxs-lookup"><span data-stu-id="743db-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="743db-152">Validation du schéma des éléments de données de document informatisé hello contre le schéma de message de type hello</span><span class="sxs-lookup"><span data-stu-id="743db-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="743db-153">Validation EDI effectuée sur les éléments de données du document informatisé.</span><span class="sxs-lookup"><span data-stu-id="743db-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="743db-154">Validation étendue effectuée sur les éléments de données du document informatisé</span><span class="sxs-lookup"><span data-stu-id="743db-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="743db-155">Demande un accusé de réception fonctionnel et/ou technique (si configuré).</span><span class="sxs-lookup"><span data-stu-id="743db-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="743db-156">Suite à la validation de l’en-tête, un accusé de réception technique est généré.</span><span class="sxs-lookup"><span data-stu-id="743db-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="743db-157">accusé de réception technique Hello signale les États hello du traitement hello d’un en-tête de l’échange et le code de fin par le récepteur d’adresse hello</span><span class="sxs-lookup"><span data-stu-id="743db-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="743db-158">Suite à la validation du corps, un accusé de réception fonctionnel est généré.</span><span class="sxs-lookup"><span data-stu-id="743db-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="743db-159">Hello accusé de réception fonctionnel signale chaque erreur rencontrée lors du traitement hello a reçu de document</span><span class="sxs-lookup"><span data-stu-id="743db-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="743db-160">Swagger hello de vue</span><span class="sxs-lookup"><span data-stu-id="743db-160">View hello swagger</span></span>
<span data-ttu-id="743db-161">Consultez hello [swagger détails](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="743db-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="743db-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="743db-162">Next steps</span></span>
[<span data-ttu-id="743db-163">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="743db-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise") 

