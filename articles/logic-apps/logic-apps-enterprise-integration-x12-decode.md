---
title: messages aaaDecode X12 - Azure Logic Apps | Documents Microsoft
description: "Valider EDI et de générer des accusés de réception avec un décodeur de message hello X12 Bonjour Enterprise Integration Pack pour Azure Logic Apps"
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
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="31c0d-103">Décoder X12 messages pour Azure Logic Apps avec hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="31c0d-103">Decode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="31c0d-104">Avec le connecteur de message hello Decode X12, vous pouvez valider l’enveloppe hello par rapport à un accord de partenariat commercial, valider EDI et des propriétés spécifiques au partenaire, fractionner des échanges en ensembles de transactions ou conserver les échanges entières et générer accusés de réception pour les transactions traitées.</span><span class="sxs-lookup"><span data-stu-id="31c0d-104">With hello Decode X12 message connector, you can validate hello envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="31c0d-105">toouse ce connecteur, vous devez ajouter tooan de connecteur hello existant déclencheur dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="31c0d-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="31c0d-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="31c0d-106">Before you start</span></span>

<span data-ttu-id="31c0d-107">Voici les éléments hello que vous devez :</span><span class="sxs-lookup"><span data-stu-id="31c0d-107">Here's hello items you need:</span></span>

* <span data-ttu-id="31c0d-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="31c0d-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="31c0d-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="31c0d-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="31c0d-110">Vous devez disposer d’un connecteur de message de décodage X12 intégration compte toouse hello.</span><span class="sxs-lookup"><span data-stu-id="31c0d-110">You must have an integration account toouse hello Decode X12 message connector.</span></span>
* <span data-ttu-id="31c0d-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="31c0d-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="31c0d-112">Un [contrat X12](logic-apps-enterprise-integration-x12.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="31c0d-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="31c0d-113">Décoder des messages X12</span><span class="sxs-lookup"><span data-stu-id="31c0d-113">Decode X12 messages</span></span>

1. <span data-ttu-id="31c0d-114">[Créer une application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="31c0d-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="31c0d-115">connecteur de message de décodage X12 Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande.</span><span class="sxs-lookup"><span data-stu-id="31c0d-115">hello Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="31c0d-116">Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.</span><span class="sxs-lookup"><span data-stu-id="31c0d-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="31c0d-117">Dans la zone de recherche de hello, entrez « x12 » pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="31c0d-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="31c0d-118">Sélectionnez **X12 – Decode X12 Message**.</span><span class="sxs-lookup"><span data-stu-id="31c0d-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Recherchez « x12 »](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="31c0d-120">Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion.</span><span class="sxs-lookup"><span data-stu-id="31c0d-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="31c0d-121">Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect.</span><span class="sxs-lookup"><span data-stu-id="31c0d-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 

    ![Fournir les détails de connexion de compte d’intégration](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="31c0d-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="31c0d-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="31c0d-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="31c0d-124">Property</span></span> | <span data-ttu-id="31c0d-125">Détails</span><span class="sxs-lookup"><span data-stu-id="31c0d-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="31c0d-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="31c0d-126">Connection Name *</span></span> |<span data-ttu-id="31c0d-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="31c0d-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="31c0d-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="31c0d-128">Integration Account *</span></span> |<span data-ttu-id="31c0d-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="31c0d-129">Enter a name for your integration account.</span></span> <span data-ttu-id="31c0d-130">Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="31c0d-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="31c0d-131">Lorsque vous avez terminé, les détails de votre connexion doivent ressembler exemple toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="31c0d-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="31c0d-132">toofinish création de votre connexion, choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="31c0d-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![détails de connexion de compte d’intégration](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="31c0d-134">Une fois que votre connexion est créée, comme indiqué dans cet exemple, sélectionnez toodecode de message de fichier plat hello X12.</span><span class="sxs-lookup"><span data-stu-id="31c0d-134">After your connection is created, as shown in this example, select hello X12 flat file message toodecode.</span></span>

    ![connexion de compte d’intégration créée](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="31c0d-136">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="31c0d-136">For example:</span></span>

    ![Sélectionner le message de fichier plat X12 à décoder](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="31c0d-138">Informations sur X12 Decode</span><span class="sxs-lookup"><span data-stu-id="31c0d-138">X12 Decode details</span></span>

<span data-ttu-id="31c0d-139">connecteur de décodage Hello X12 effectue ces tâches :</span><span class="sxs-lookup"><span data-stu-id="31c0d-139">hello X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="31c0d-140">Valide l’enveloppe hello par rapport à l’accord de partenariat commercial</span><span class="sxs-lookup"><span data-stu-id="31c0d-140">Validates hello envelope against trading partner agreement</span></span>
* <span data-ttu-id="31c0d-141">Valide l’EDI et les propriétés spécifiques au partenaire</span><span class="sxs-lookup"><span data-stu-id="31c0d-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="31c0d-142">Validation de la structure EDI et validation du schéma étendue</span><span class="sxs-lookup"><span data-stu-id="31c0d-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="31c0d-143">Validation de la structure hello d’enveloppe d’échange hello.</span><span class="sxs-lookup"><span data-stu-id="31c0d-143">Validation of hello structure of hello interchange envelope.</span></span>
  * <span data-ttu-id="31c0d-144">Validation du schéma d’enveloppe hello contre le schéma de contrôle hello.</span><span class="sxs-lookup"><span data-stu-id="31c0d-144">Schema validation of hello envelope against hello control schema.</span></span>
  * <span data-ttu-id="31c0d-145">Validation du schéma des éléments de données de document informatisé hello contre le schéma de message hello.</span><span class="sxs-lookup"><span data-stu-id="31c0d-145">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="31c0d-146">Validation EDI effectuée sur les éléments de données du document informatisé.</span><span class="sxs-lookup"><span data-stu-id="31c0d-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="31c0d-147">Vérifie que hello échange, groupe et transaction numéros de contrôle ne sont pas des doublons</span><span class="sxs-lookup"><span data-stu-id="31c0d-147">Verifies that hello interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="31c0d-148">Vérifie le numéro de contrôle d’échange hello par rapport aux échanges reçus précédemment.</span><span class="sxs-lookup"><span data-stu-id="31c0d-148">Checks hello interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="31c0d-149">Vérifie le numéro de contrôle de groupe hello par rapport à d’autres numéros de contrôle de groupe dans l’échange de hello.</span><span class="sxs-lookup"><span data-stu-id="31c0d-149">Checks hello group control number against other group control numbers in hello interchange.</span></span>
  * <span data-ttu-id="31c0d-150">Vérifie les transactions hello définit le numéro de contrôle par rapport à d’autres numéros de contrôle de transaction de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="31c0d-150">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="31c0d-151">Fractionne échange hello en documents informatisés ou conserve l’ensemble de l’échange hello :</span><span class="sxs-lookup"><span data-stu-id="31c0d-151">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="31c0d-152">Scinder l’échange en documents informatisés : suspendre les documents informatisés en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé.</span><span class="sxs-lookup"><span data-stu-id="31c0d-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="31c0d-153">action de décodage Hello X12 génère uniquement ces documents informatisés dont la validation échouent trop`badMessages`et fournit en sortie hello transactions restantes définit trop`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="31c0d-153">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="31c0d-154">Scinder l’échange en documents informatisés : suspendre l’échange en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé.</span><span class="sxs-lookup"><span data-stu-id="31c0d-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="31c0d-155">Si une ou plusieurs transactions définit dans la validation a échoué échange hello, action de décodage hello X12 génère toutes les transactions hello définit dans cet échange trop`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="31c0d-155">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="31c0d-156">Préserver l’échange : suspendre les documents informatisés en cas d’erreur : échange de hello Preserve et processus hello tout échange par lot.</span><span class="sxs-lookup"><span data-stu-id="31c0d-156">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="31c0d-157">action de décodage Hello X12 génère uniquement ces documents informatisés dont la validation échouent trop`badMessages`et fournit en sortie hello transactions restantes définit trop`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="31c0d-157">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="31c0d-158">Préserver l’échange : suspendre l’échange en cas d’erreur : échange de hello Preserve et processus hello tout échange par lot.</span><span class="sxs-lookup"><span data-stu-id="31c0d-158">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="31c0d-159">Si une ou plusieurs transactions définit dans la validation a échoué échange hello, action de décodage hello X12 génère toutes les transactions hello définit dans cet échange trop`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="31c0d-159">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span> 
* <span data-ttu-id="31c0d-160">Génère un accusé de réception fonctionnel et/ou technique (si configuré).</span><span class="sxs-lookup"><span data-stu-id="31c0d-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="31c0d-161">Suite à la validation de l’en-tête, un accusé de réception technique est généré.</span><span class="sxs-lookup"><span data-stu-id="31c0d-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="31c0d-162">accusé de réception technique Hello signale l’état de hello du traitement hello d’un en-tête de l’échange et le code de fin par le récepteur d’adresse hello.</span><span class="sxs-lookup"><span data-stu-id="31c0d-162">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver.</span></span>
  * <span data-ttu-id="31c0d-163">Suite à la validation du corps, un accusé de réception fonctionnel est généré.</span><span class="sxs-lookup"><span data-stu-id="31c0d-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="31c0d-164">Hello accusé de réception fonctionnel signale chaque erreur rencontrée lors du traitement hello a reçu de document</span><span class="sxs-lookup"><span data-stu-id="31c0d-164">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="31c0d-165">Swagger hello de vue</span><span class="sxs-lookup"><span data-stu-id="31c0d-165">View hello swagger</span></span>
<span data-ttu-id="31c0d-166">Consultez hello [swagger détails](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="31c0d-166">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="31c0d-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31c0d-167">Next steps</span></span>
[<span data-ttu-id="31c0d-168">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="31c0d-168">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise") 

