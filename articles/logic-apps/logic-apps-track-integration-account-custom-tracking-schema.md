---
title: "aaaCustom suivi des schémas pour B2B analyse - Azure Logic Apps | Documents Microsoft"
description: "Créer des schémas de suivi personnalisé toomonitor B2B messages à partir des transactions dans votre compte de l’intégration d’Azure."
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
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="ae73f-103">Activer le suivi des toomonitor votre flux de travail terminée, bout en bout</span><span class="sxs-lookup"><span data-stu-id="ae73f-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="ae73f-104">Vous pouvez activer un suivi intégré pour les différentes parties de votre flux de travail d’entreprise à entreprise, notamment le suivi des messages AS2 ou X12.</span><span class="sxs-lookup"><span data-stu-id="ae73f-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="ae73f-105">Lorsque vous créez des workflows, qui inclut une application logique, BizTalk Server, SQL Server ou toutes les autres couches, vous pouvez activer le suivi personnalisé qui enregistre les événements à partir de hello début toohello à la fin du flux de travail.</span><span class="sxs-lookup"><span data-stu-id="ae73f-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="ae73f-106">Cette rubrique fournit un code personnalisé que vous pouvez utiliser dans les couches de hello en dehors de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="ae73f-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="ae73f-107">Schéma de suivi personnalisé</span><span class="sxs-lookup"><span data-stu-id="ae73f-107">Custom tracking schema</span></span>
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

| <span data-ttu-id="ae73f-108">Propriété</span><span class="sxs-lookup"><span data-stu-id="ae73f-108">Property</span></span> | <span data-ttu-id="ae73f-109">Type</span><span class="sxs-lookup"><span data-stu-id="ae73f-109">Type</span></span> | <span data-ttu-id="ae73f-110">Description</span><span class="sxs-lookup"><span data-stu-id="ae73f-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ae73f-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="ae73f-111">sourceType</span></span> |   | <span data-ttu-id="ae73f-112">Type de source de hello exécuter.</span><span class="sxs-lookup"><span data-stu-id="ae73f-112">Type of hello run source.</span></span> <span data-ttu-id="ae73f-113">Les valeurs autorisées sont **Microsoft.Logic/workflows** et **custom**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="ae73f-114">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-114">(Mandatory)</span></span> |
| <span data-ttu-id="ae73f-115">Source</span><span class="sxs-lookup"><span data-stu-id="ae73f-115">Source</span></span> |   | <span data-ttu-id="ae73f-116">Si le type de source de hello est **Microsoft.Logic/workflows**, informations de source de hello doivent toofollow ce schéma.</span><span class="sxs-lookup"><span data-stu-id="ae73f-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="ae73f-117">Si le type de source de hello est **personnalisé**, schéma de hello est un JToken.</span><span class="sxs-lookup"><span data-stu-id="ae73f-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="ae73f-118">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-118">(Mandatory)</span></span> |
| <span data-ttu-id="ae73f-119">systemId</span><span class="sxs-lookup"><span data-stu-id="ae73f-119">systemId</span></span> | <span data-ttu-id="ae73f-120">String</span><span class="sxs-lookup"><span data-stu-id="ae73f-120">String</span></span> | <span data-ttu-id="ae73f-121">ID système d’application logique.</span><span class="sxs-lookup"><span data-stu-id="ae73f-121">Logic app system ID.</span></span> <span data-ttu-id="ae73f-122">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-122">(Mandatory)</span></span> |
| <span data-ttu-id="ae73f-123">runId</span><span class="sxs-lookup"><span data-stu-id="ae73f-123">runId</span></span> | <span data-ttu-id="ae73f-124">String</span><span class="sxs-lookup"><span data-stu-id="ae73f-124">String</span></span> | <span data-ttu-id="ae73f-125">ID d’exécution d’application logique.</span><span class="sxs-lookup"><span data-stu-id="ae73f-125">Logic app run ID.</span></span> <span data-ttu-id="ae73f-126">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-126">(Mandatory)</span></span> |
| <span data-ttu-id="ae73f-127">operationName</span><span class="sxs-lookup"><span data-stu-id="ae73f-127">operationName</span></span> | <span data-ttu-id="ae73f-128">String</span><span class="sxs-lookup"><span data-stu-id="ae73f-128">String</span></span> | <span data-ttu-id="ae73f-129">Nom de l’opération hello (par exemple, action ou déclencheur).</span><span class="sxs-lookup"><span data-stu-id="ae73f-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="ae73f-130">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-130">(Mandatory)</span></span> |
| <span data-ttu-id="ae73f-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="ae73f-131">repeatItemScopeName</span></span> | <span data-ttu-id="ae73f-132">String</span><span class="sxs-lookup"><span data-stu-id="ae73f-132">String</span></span> | <span data-ttu-id="ae73f-133">Répétez le nom de l’élément si l’action de hello est à l’intérieur d’un `foreach` / `until` boucle.</span><span class="sxs-lookup"><span data-stu-id="ae73f-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="ae73f-134">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-134">(Mandatory)</span></span> |
| <span data-ttu-id="ae73f-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="ae73f-135">repeatItemIndex</span></span> | <span data-ttu-id="ae73f-136">Entier </span><span class="sxs-lookup"><span data-stu-id="ae73f-136">Integer</span></span> | <span data-ttu-id="ae73f-137">Si l’action de hello est à l’intérieur d’un `foreach` / `until` boucle.</span><span class="sxs-lookup"><span data-stu-id="ae73f-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="ae73f-138">Indique l’index de l’élément répété hello.</span><span class="sxs-lookup"><span data-stu-id="ae73f-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="ae73f-139">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-139">(Mandatory)</span></span> |
| <span data-ttu-id="ae73f-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="ae73f-140">trackingId</span></span> | <span data-ttu-id="ae73f-141">String</span><span class="sxs-lookup"><span data-stu-id="ae73f-141">String</span></span> | <span data-ttu-id="ae73f-142">ID de suivi de messages de type hello toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="ae73f-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="ae73f-143">(facultatif)</span><span class="sxs-lookup"><span data-stu-id="ae73f-143">(Optional)</span></span> |
| <span data-ttu-id="ae73f-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="ae73f-144">correlationId</span></span> | <span data-ttu-id="ae73f-145">String</span><span class="sxs-lookup"><span data-stu-id="ae73f-145">String</span></span> | <span data-ttu-id="ae73f-146">ID de corrélation de messages de type hello toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="ae73f-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="ae73f-147">(facultatif)</span><span class="sxs-lookup"><span data-stu-id="ae73f-147">(Optional)</span></span> |
| <span data-ttu-id="ae73f-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="ae73f-148">clientRequestId</span></span> | <span data-ttu-id="ae73f-149">String</span><span class="sxs-lookup"><span data-stu-id="ae73f-149">String</span></span> | <span data-ttu-id="ae73f-150">Client peut remplir toocorrelate messages.</span><span class="sxs-lookup"><span data-stu-id="ae73f-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="ae73f-151">(facultatif)</span><span class="sxs-lookup"><span data-stu-id="ae73f-151">(Optional)</span></span> |
| <span data-ttu-id="ae73f-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="ae73f-152">eventLevel</span></span> |   | <span data-ttu-id="ae73f-153">Niveau d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="ae73f-153">Level of hello event.</span></span> <span data-ttu-id="ae73f-154">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-154">(Mandatory)</span></span> |
| <span data-ttu-id="ae73f-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="ae73f-155">eventTime</span></span> |   | <span data-ttu-id="ae73f-156">Heure de l’événement hello, dans le format UTC AAAA-MM-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="ae73f-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="ae73f-157">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-157">(Mandatory)</span></span> |
| <span data-ttu-id="ae73f-158">recordType</span><span class="sxs-lookup"><span data-stu-id="ae73f-158">recordType</span></span> |   | <span data-ttu-id="ae73f-159">Type d’enregistrement de suivi hello.</span><span class="sxs-lookup"><span data-stu-id="ae73f-159">Type of hello track record.</span></span> <span data-ttu-id="ae73f-160">La valeur autorisée est **Custom**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-160">Allowed value is **custom**.</span></span> <span data-ttu-id="ae73f-161">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-161">(Mandatory)</span></span> |
| <span data-ttu-id="ae73f-162">record</span><span class="sxs-lookup"><span data-stu-id="ae73f-162">record</span></span> |   | <span data-ttu-id="ae73f-163">Type d'enregistrement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="ae73f-163">Custom record type.</span></span> <span data-ttu-id="ae73f-164">Le format autorisé est JToken.</span><span class="sxs-lookup"><span data-stu-id="ae73f-164">Allowed format is JToken.</span></span> <span data-ttu-id="ae73f-165">(obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ae73f-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="ae73f-166">Schémas de suivi de protocole B2B</span><span class="sxs-lookup"><span data-stu-id="ae73f-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="ae73f-167">Pour plus d’informations sur les schémas de suivi de protocole B2B, consultez :</span><span class="sxs-lookup"><span data-stu-id="ae73f-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="ae73f-168">Schémas de suivi AS2</span><span class="sxs-lookup"><span data-stu-id="ae73f-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="ae73f-169">Schémas de suivi X12</span><span class="sxs-lookup"><span data-stu-id="ae73f-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="ae73f-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae73f-170">Next steps</span></span>
* <span data-ttu-id="ae73f-171">En savoir plus sur le [suivi des messages B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="ae73f-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="ae73f-172">En savoir plus sur [le suivi des messages B2B dans le portail Operations Management Suite de hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="ae73f-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="ae73f-173">En savoir plus sur hello [Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae73f-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
