---
title: "Schémas de suivi personnalisé pour la surveillance B2B - Azure Logic Apps | Microsoft Docs"
description: "Créez des schémas de suivi personnalisé pour surveiller les messages B2B des transactions de votre compte d’intégration Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b71a4938dde2a71f1ce29403af7aa9101358d64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-tracking-to-monitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="1fc7d-103">Activation du suivi pour surveiller votre flux de travail complet, de bout en bout</span><span class="sxs-lookup"><span data-stu-id="1fc7d-103">Enable tracking to monitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="1fc7d-104">Vous pouvez activer un suivi intégré pour les différentes parties de votre flux de travail d’entreprise à entreprise, notamment le suivi des messages AS2 ou X12.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="1fc7d-105">Lorsque vous créez des flux de travail qui incluent une application logique, BizTalk Server, SQL Server ou n’importe quelle autre couche, vous pouvez activer un suivi personnalisé qui consigne les événements du début à la fin de votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span></span> 

<span data-ttu-id="1fc7d-106">Cette rubrique fournit un code personnalisé que vous pouvez utiliser dans les couches en dehors de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-106">This topic provides custom code that you can use in the layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="1fc7d-107">Schéma de suivi personnalisé</span><span class="sxs-lookup"><span data-stu-id="1fc7d-107">Custom tracking schema</span></span>
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| <span data-ttu-id="1fc7d-108">Propriété</span><span class="sxs-lookup"><span data-stu-id="1fc7d-108">Property</span></span> | <span data-ttu-id="1fc7d-109">Type</span><span class="sxs-lookup"><span data-stu-id="1fc7d-109">Type</span></span> | <span data-ttu-id="1fc7d-110">Description</span><span class="sxs-lookup"><span data-stu-id="1fc7d-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1fc7d-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="1fc7d-111">sourceType</span></span> |   | <span data-ttu-id="1fc7d-112">Type de source d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-112">Type of the run source.</span></span> <span data-ttu-id="1fc7d-113">Les valeurs autorisées sont **Microsoft.Logic/workflows** et **custom**.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="1fc7d-114">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-114">(Mandatory)</span></span> |
| <span data-ttu-id="1fc7d-115">Source</span><span class="sxs-lookup"><span data-stu-id="1fc7d-115">Source</span></span> |   | <span data-ttu-id="1fc7d-116">Si le type de source est **Microsoft.Logic/workflows**, les informations source doivent suivre ce schéma.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span></span> <span data-ttu-id="1fc7d-117">Si le type de source est **custom**, le schéma est un JToken.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-117">If the source type is **custom**, the schema is a JToken.</span></span> <span data-ttu-id="1fc7d-118">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-118">(Mandatory)</span></span> |
| <span data-ttu-id="1fc7d-119">systemId</span><span class="sxs-lookup"><span data-stu-id="1fc7d-119">systemId</span></span> | <span data-ttu-id="1fc7d-120">String</span><span class="sxs-lookup"><span data-stu-id="1fc7d-120">String</span></span> | <span data-ttu-id="1fc7d-121">ID système d’application logique.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-121">Logic app system ID.</span></span> <span data-ttu-id="1fc7d-122">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-122">(Mandatory)</span></span> |
| <span data-ttu-id="1fc7d-123">runId</span><span class="sxs-lookup"><span data-stu-id="1fc7d-123">runId</span></span> | <span data-ttu-id="1fc7d-124">String</span><span class="sxs-lookup"><span data-stu-id="1fc7d-124">String</span></span> | <span data-ttu-id="1fc7d-125">ID d’exécution d’application logique.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-125">Logic app run ID.</span></span> <span data-ttu-id="1fc7d-126">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-126">(Mandatory)</span></span> |
| <span data-ttu-id="1fc7d-127">operationName</span><span class="sxs-lookup"><span data-stu-id="1fc7d-127">operationName</span></span> | <span data-ttu-id="1fc7d-128">String</span><span class="sxs-lookup"><span data-stu-id="1fc7d-128">String</span></span> | <span data-ttu-id="1fc7d-129">Nom de l’opération (par exemple action ou déclencheur).</span><span class="sxs-lookup"><span data-stu-id="1fc7d-129">Name of the operation (for example, action or trigger).</span></span> <span data-ttu-id="1fc7d-130">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-130">(Mandatory)</span></span> |
| <span data-ttu-id="1fc7d-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="1fc7d-131">repeatItemScopeName</span></span> | <span data-ttu-id="1fc7d-132">String</span><span class="sxs-lookup"><span data-stu-id="1fc7d-132">String</span></span> | <span data-ttu-id="1fc7d-133">Répéter le nom de l’élément si l’action se trouve au sein d’une boucle `foreach`/`until`.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="1fc7d-134">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-134">(Mandatory)</span></span> |
| <span data-ttu-id="1fc7d-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="1fc7d-135">repeatItemIndex</span></span> | <span data-ttu-id="1fc7d-136">Entier </span><span class="sxs-lookup"><span data-stu-id="1fc7d-136">Integer</span></span> | <span data-ttu-id="1fc7d-137">Indique si l’action se trouve au sein d’une boucle `foreach`/`until`.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-137">Whether the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="1fc7d-138">Indique l’index de l’élément répété.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-138">Indicates the repeated item index.</span></span> <span data-ttu-id="1fc7d-139">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-139">(Mandatory)</span></span> |
| <span data-ttu-id="1fc7d-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="1fc7d-140">trackingId</span></span> | <span data-ttu-id="1fc7d-141">String</span><span class="sxs-lookup"><span data-stu-id="1fc7d-141">String</span></span> | <span data-ttu-id="1fc7d-142">ID de suivi permettant de corréler les messages.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-142">Tracking ID, to correlate the messages.</span></span> <span data-ttu-id="1fc7d-143">(facultatif)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-143">(Optional)</span></span> |
| <span data-ttu-id="1fc7d-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="1fc7d-144">correlationId</span></span> | <span data-ttu-id="1fc7d-145">String</span><span class="sxs-lookup"><span data-stu-id="1fc7d-145">String</span></span> | <span data-ttu-id="1fc7d-146">ID de corrélation permettant de corréler les messages.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-146">Correlation ID, to correlate the messages.</span></span> <span data-ttu-id="1fc7d-147">(facultatif)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-147">(Optional)</span></span> |
| <span data-ttu-id="1fc7d-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="1fc7d-148">clientRequestId</span></span> | <span data-ttu-id="1fc7d-149">String</span><span class="sxs-lookup"><span data-stu-id="1fc7d-149">String</span></span> | <span data-ttu-id="1fc7d-150">Le client peut remplir ce champ pour corréler les messages.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-150">Client can populate it to correlate messages.</span></span> <span data-ttu-id="1fc7d-151">(facultatif)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-151">(Optional)</span></span> |
| <span data-ttu-id="1fc7d-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="1fc7d-152">eventLevel</span></span> |   | <span data-ttu-id="1fc7d-153">Niveau de l’événement.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-153">Level of the event.</span></span> <span data-ttu-id="1fc7d-154">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-154">(Mandatory)</span></span> |
| <span data-ttu-id="1fc7d-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="1fc7d-155">eventTime</span></span> |   | <span data-ttu-id="1fc7d-156">Heure de l’événement au format UTC AAAA-MM-JJTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="1fc7d-157">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-157">(Mandatory)</span></span> |
| <span data-ttu-id="1fc7d-158">recordType</span><span class="sxs-lookup"><span data-stu-id="1fc7d-158">recordType</span></span> |   | <span data-ttu-id="1fc7d-159">Type de l’enregistrement de suivi.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-159">Type of the track record.</span></span> <span data-ttu-id="1fc7d-160">La valeur autorisée est **Custom**.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-160">Allowed value is **custom**.</span></span> <span data-ttu-id="1fc7d-161">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-161">(Mandatory)</span></span> |
| <span data-ttu-id="1fc7d-162">record</span><span class="sxs-lookup"><span data-stu-id="1fc7d-162">record</span></span> |   | <span data-ttu-id="1fc7d-163">Type d'enregistrement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-163">Custom record type.</span></span> <span data-ttu-id="1fc7d-164">Le format autorisé est JToken.</span><span class="sxs-lookup"><span data-stu-id="1fc7d-164">Allowed format is JToken.</span></span> <span data-ttu-id="1fc7d-165">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1fc7d-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="1fc7d-166">Schémas de suivi de protocole B2B</span><span class="sxs-lookup"><span data-stu-id="1fc7d-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="1fc7d-167">Pour plus d’informations sur les schémas de suivi de protocole B2B, consultez :</span><span class="sxs-lookup"><span data-stu-id="1fc7d-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="1fc7d-168">Schémas de suivi AS2</span><span class="sxs-lookup"><span data-stu-id="1fc7d-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="1fc7d-169">Schémas de suivi X12</span><span class="sxs-lookup"><span data-stu-id="1fc7d-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="1fc7d-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1fc7d-170">Next steps</span></span>
* <span data-ttu-id="1fc7d-171">En savoir plus sur le [suivi des messages B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="1fc7d-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="1fc7d-172">En savoir plus sur le [suivi de messages B2B dans le portail Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="1fc7d-172">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="1fc7d-173">En savoir plus sur [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1fc7d-173">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
