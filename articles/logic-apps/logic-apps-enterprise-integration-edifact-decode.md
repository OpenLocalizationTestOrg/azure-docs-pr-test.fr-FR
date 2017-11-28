---
title: les messages EDIFACT aaaDecode - Azure Logic Apps | Documents Microsoft
description: "Validation EDI et générer des accusés de réception avec un décodeur de message EDIFACT hello en hello Enterprise Integration Pack pour Azure Logic Apps"
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
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="ec138-103">Décoder les messages EDIFACT pour Azure Logic Apps avec hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="ec138-103">Decode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="ec138-104">Avec le connecteur de message EDIFACT de décoder hello, vous pouvez valider EDI et des propriétés spécifiques aux partenaires, fractionner des échanges en ensembles de transactions ou conserver les échanges entières et générer des accusés de réception pour les transactions traitées.</span><span class="sxs-lookup"><span data-stu-id="ec138-104">With hello Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="ec138-105">toouse ce connecteur, vous devez ajouter tooan de connecteur hello existant déclencheur dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="ec138-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ec138-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ec138-106">Before you start</span></span>

<span data-ttu-id="ec138-107">Voici les éléments hello que vous devez :</span><span class="sxs-lookup"><span data-stu-id="ec138-107">Here's hello items you need:</span></span>

* <span data-ttu-id="ec138-108">Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="ec138-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="ec138-109">Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ec138-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="ec138-110">Vous devez disposer d’un connecteur de message intégration compte toouse hello EDIFACT de décoder.</span><span class="sxs-lookup"><span data-stu-id="ec138-110">You must have an integration account toouse hello Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="ec138-111">Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="ec138-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="ec138-112">Un [contrat EDIFACT](logic-apps-enterprise-integration-edifact.md) déjà défini dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="ec138-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="ec138-113">Messages Decode EDIFACT</span><span class="sxs-lookup"><span data-stu-id="ec138-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="ec138-114">[Créer une application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ec138-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="ec138-115">connecteur de message de décoder les EDIFACT Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande.</span><span class="sxs-lookup"><span data-stu-id="ec138-115">hello Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="ec138-116">Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.</span><span class="sxs-lookup"><span data-stu-id="ec138-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3. <span data-ttu-id="ec138-117">Dans la zone de recherche de hello, entrez « EDIFACT » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="ec138-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="ec138-118">Sélectionnez **Decode EDIFACT Message**.</span><span class="sxs-lookup"><span data-stu-id="ec138-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![recherche EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="ec138-120">Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion.</span><span class="sxs-lookup"><span data-stu-id="ec138-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="ec138-121">Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect.</span><span class="sxs-lookup"><span data-stu-id="ec138-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![créer un compte d’intégration](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="ec138-123">Les propriétés marquées d’un astérisque sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="ec138-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="ec138-124">Propriété</span><span class="sxs-lookup"><span data-stu-id="ec138-124">Property</span></span> | <span data-ttu-id="ec138-125">Détails</span><span class="sxs-lookup"><span data-stu-id="ec138-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="ec138-126">Nom de connexion *</span><span class="sxs-lookup"><span data-stu-id="ec138-126">Connection Name *</span></span> |<span data-ttu-id="ec138-127">Entrez un nom pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="ec138-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="ec138-128">Compte d’intégration *</span><span class="sxs-lookup"><span data-stu-id="ec138-128">Integration Account *</span></span> |<span data-ttu-id="ec138-129">Entrez un nom pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="ec138-129">Enter a name for your integration account.</span></span> <span data-ttu-id="ec138-130">Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="ec138-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

4. <span data-ttu-id="ec138-131">Lorsque vous avez terminé la création de votre connexion de toofinish, choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="ec138-131">When you're done toofinish creating your connection, choose **Create**.</span></span> <span data-ttu-id="ec138-132">Détails de votre connexion doivent ressembler exemple toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="ec138-132">Your connection details should look similar toothis example:</span></span>

    ![détails du compte d’intégration](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="ec138-134">Une fois que votre connexion est créée, comme indiqué dans cet exemple, sélectionnez toodecode de message de fichier plat de EDIFACT hello.</span><span class="sxs-lookup"><span data-stu-id="ec138-134">After your connection is created, as shown in this example, select hello EDIFACT flat file message toodecode.</span></span>

    ![connexion de compte d’intégration créée](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="ec138-136">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ec138-136">For example:</span></span>

    ![Sélectionner le message de fichier plat EDIFACT à décoder](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="ec138-138">Détails sur le décodeur EDIFACT</span><span class="sxs-lookup"><span data-stu-id="ec138-138">EDIFACT decoder details</span></span>

<span data-ttu-id="ec138-139">connecteur de décoder les EDIFACT Hello effectue ces tâches :</span><span class="sxs-lookup"><span data-stu-id="ec138-139">hello Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="ec138-140">Valide l’enveloppe hello par rapport à l’accord de partenariat commercial.</span><span class="sxs-lookup"><span data-stu-id="ec138-140">Validates hello envelope against trading partner agreement.</span></span>
* <span data-ttu-id="ec138-141">Résout l’accord de hello en mettant en correspondance le qualificateur de l’expéditeur hello et identificateur et qualificateur du récepteur et identificateur.</span><span class="sxs-lookup"><span data-stu-id="ec138-141">Resolves hello agreement by matching hello sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="ec138-142">Fractionne un échange en plusieurs transactions lors de l’échange de hello a plus d’une transaction en fonction de l’accord hello configuration des paramètres de réception.</span><span class="sxs-lookup"><span data-stu-id="ec138-142">Splits an interchange into multiple transactions when hello interchange has more than one transaction based on hello agreement's receive settings configuration.</span></span>
* <span data-ttu-id="ec138-143">Désassemble l’échange de hello.</span><span class="sxs-lookup"><span data-stu-id="ec138-143">Disassembles hello interchange.</span></span>
* <span data-ttu-id="ec138-144">Valide l’EDI et les propriétés spécifiques du partenaire, y compris :</span><span class="sxs-lookup"><span data-stu-id="ec138-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="ec138-145">Validation de la structure de l’enveloppe échange hello</span><span class="sxs-lookup"><span data-stu-id="ec138-145">Validation of hello interchange envelope structure</span></span>
  * <span data-ttu-id="ec138-146">Validation du schéma d’enveloppe hello contre le schéma de contrôle hello</span><span class="sxs-lookup"><span data-stu-id="ec138-146">Schema validation of hello envelope against hello control schema</span></span>
  * <span data-ttu-id="ec138-147">Validation du schéma des éléments de données de document informatisé hello contre le schéma de message hello</span><span class="sxs-lookup"><span data-stu-id="ec138-147">Schema validation of hello transaction-set data elements against hello message schema</span></span>
  * <span data-ttu-id="ec138-148">Validation EDI effectuée sur les éléments de données du document informatisé.</span><span class="sxs-lookup"><span data-stu-id="ec138-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="ec138-149">Vérifie que hello échange, groupe et transaction numéros de contrôle ne sont pas les doublons (si configuré)</span><span class="sxs-lookup"><span data-stu-id="ec138-149">Verifies that hello interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="ec138-150">Vérifie le numéro de contrôle d’échange hello par rapport aux échanges reçus précédemment.</span><span class="sxs-lookup"><span data-stu-id="ec138-150">Checks hello interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="ec138-151">Vérifie le numéro de contrôle de groupe hello par rapport à d’autres numéros de contrôle de groupe dans l’échange de hello.</span><span class="sxs-lookup"><span data-stu-id="ec138-151">Checks hello group control number against other group control numbers in hello interchange.</span></span> 
  * <span data-ttu-id="ec138-152">Vérifie les transactions hello définit le numéro de contrôle par rapport à d’autres numéros de contrôle de transaction de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="ec138-152">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="ec138-153">Fractionne échange hello en documents informatisés ou conserve l’ensemble de l’échange hello :</span><span class="sxs-lookup"><span data-stu-id="ec138-153">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="ec138-154">Scinder l’échange en documents informatisés : suspendre les documents informatisés en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé.</span><span class="sxs-lookup"><span data-stu-id="ec138-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="ec138-155">action de décodage Hello X12 génère uniquement ces documents informatisés dont la validation échouent trop`badMessages`et fournit en sortie hello transactions restantes définit trop`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="ec138-155">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="ec138-156">Scinder l’échange en documents informatisés : suspendre l’échange en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé.</span><span class="sxs-lookup"><span data-stu-id="ec138-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="ec138-157">Si une ou plusieurs transactions définit dans la validation a échoué échange hello, action de décodage hello X12 génère toutes les transactions hello définit dans cet échange trop`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="ec138-157">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="ec138-158">Préserver l’échange : suspendre les documents informatisés en cas d’erreur : échange de hello Preserve et processus hello tout échange par lot.</span><span class="sxs-lookup"><span data-stu-id="ec138-158">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="ec138-159">action de décodage Hello X12 génère uniquement ces documents informatisés dont la validation échouent trop`badMessages`et fournit en sortie hello transactions restantes définit trop`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="ec138-159">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="ec138-160">Préserver l’échange : suspendre l’échange en cas d’erreur : échange de hello Preserve et processus hello tout échange par lot.</span><span class="sxs-lookup"><span data-stu-id="ec138-160">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="ec138-161">Si une ou plusieurs transactions définit dans la validation a échoué échange hello, action de décodage hello X12 génère toutes les transactions hello définit dans cet échange trop`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="ec138-161">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
* <span data-ttu-id="ec138-162">Génère un accusé de réception fonctionnel et/ou technique (contrôle) (si configuré).</span><span class="sxs-lookup"><span data-stu-id="ec138-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="ec138-163">Un accusé de réception technique ou le hello CONTRL ACK signale les résultats de hello d’une vérification syntaxique d’échange de hello complet reçu.</span><span class="sxs-lookup"><span data-stu-id="ec138-163">A Technical Acknowledgment or hello CONTRL ACK reports hello results of a syntactical check of hello complete received interchange.</span></span>
  * <span data-ttu-id="ec138-164">Un accusé de réception fonctionnel accuse réception de l’acceptation ou du refus d’un groupe ou d’un échange reçu</span><span class="sxs-lookup"><span data-stu-id="ec138-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="ec138-165">Afficher le fichier Swagger</span><span class="sxs-lookup"><span data-stu-id="ec138-165">View Swagger file</span></span>
<span data-ttu-id="ec138-166">Détails de Swagger tooview hello pour le connecteur d’EDIFACT hello, consultez [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="ec138-166">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec138-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec138-167">Next steps</span></span>
[<span data-ttu-id="ec138-168">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="ec138-168">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise") 

