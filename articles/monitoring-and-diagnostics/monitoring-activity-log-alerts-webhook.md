---
title: "schéma de webhook aaaUnderstand hello utilisée dans les alertes de journal d’activité | Documents Microsoft"
description: "En savoir plus sur le schéma hello Hello JSON est validé l’URL du webhook tooa lorsqu’une alerte de journal d’activité active."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="19bad-103">Webhook des alertes du journal d’activité Azure</span><span class="sxs-lookup"><span data-stu-id="19bad-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="19bad-104">Dans le cadre de définition de hello d’un groupe d’actions, vous pouvez configurer webhook points de terminaison tooreceive activité journal des notifications d’alerte.</span><span class="sxs-lookup"><span data-stu-id="19bad-104">As part of hello definition of an action group, you can configure webhook endpoints tooreceive activity log alert notifications.</span></span> <span data-ttu-id="19bad-105">Avec le webhooks, vous pouvez acheminer ces systèmes de tooother des notifications pour les actions de post-traitement ou personnalisées.</span><span class="sxs-lookup"><span data-stu-id="19bad-105">With webhooks, you can route these notifications tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="19bad-106">Cet article explique le charge hello hello HTTP POST tooa webhook ressemble à.</span><span class="sxs-lookup"><span data-stu-id="19bad-106">This article shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span>

<span data-ttu-id="19bad-107">Pour plus d’informations sur les alertes de journal d’activité, consultez Comment trop[créer des alertes de journal des activités Windows Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="19bad-107">For more information on activity log alerts, see how too[create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="19bad-108">Pour plus d’informations sur les groupes d’actions, consultez Comment trop[créer des groupes d’actions](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="19bad-108">For information on action groups, see how too[create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-hello-webhook"></a><span data-ttu-id="19bad-109">Authentifier hello webhook</span><span class="sxs-lookup"><span data-stu-id="19bad-109">Authenticate hello webhook</span></span>
<span data-ttu-id="19bad-110">Hello webhook peut éventuellement utiliser d’autorisation basée sur un jeton pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="19bad-110">hello webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="19bad-111">Hello webhook URI est enregistré avec un ID de jeton, par exemple, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="19bad-111">hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="19bad-112">Schéma de la charge utile</span><span class="sxs-lookup"><span data-stu-id="19bad-112">Payload schema</span></span>
<span data-ttu-id="19bad-113">charge utile JSON de Hello contenue dans hello opération POST diffère en fonction de champ de data.context.activityLog.eventSource de charge utile de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-113">hello JSON payload contained in hello POST operation differs based on hello payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="19bad-114">Courant</span><span class="sxs-lookup"><span data-stu-id="19bad-114">Common</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a><span data-ttu-id="19bad-115">Administratif</span><span class="sxs-lookup"><span data-stu-id="19bad-115">Administrative</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a><span data-ttu-id="19bad-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="19bad-116">ServiceHealth</span></span>
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

<span data-ttu-id="19bad-117">Pour obtenir des informations spécifiques au sujet des schémas des alertes du journal d’activité sur les notifications d’intégrité du service, consultez la page [Notifications d’intégrité du service](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="19bad-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="19bad-118">Pour plus d’informations de schéma spécifique sur toutes les autres alertes de journal d’activité, consultez [vue d’ensemble du journal des activités Windows Azure hello](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="19bad-118">For specific schema details on all other activity log alerts, see [Overview of hello Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="19bad-119">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="19bad-119">Element name</span></span> | <span data-ttu-id="19bad-120">Description</span><span class="sxs-lookup"><span data-stu-id="19bad-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19bad-121">status</span><span class="sxs-lookup"><span data-stu-id="19bad-121">status</span></span> |<span data-ttu-id="19bad-122">Utilisé pour les alertes de métrique.</span><span class="sxs-lookup"><span data-stu-id="19bad-122">Used for metric alerts.</span></span> <span data-ttu-id="19bad-123">Toujours défini trop « activé » pour les alertes de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="19bad-123">Always set too"activated" for activity log alerts.</span></span> |
| <span data-ttu-id="19bad-124">context</span><span class="sxs-lookup"><span data-stu-id="19bad-124">context</span></span> |<span data-ttu-id="19bad-125">Contexte d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-125">Context of hello event.</span></span> |
| <span data-ttu-id="19bad-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="19bad-126">resourceProviderName</span></span> |<span data-ttu-id="19bad-127">le fournisseur de ressources Hello Hello incidence sur la ressource.</span><span class="sxs-lookup"><span data-stu-id="19bad-127">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="19bad-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="19bad-128">conditionType</span></span> |<span data-ttu-id="19bad-129">Toujours défini sur « Event ».</span><span class="sxs-lookup"><span data-stu-id="19bad-129">Always "Event."</span></span> |
| <span data-ttu-id="19bad-130">name</span><span class="sxs-lookup"><span data-stu-id="19bad-130">name</span></span> |<span data-ttu-id="19bad-131">Nom de règle d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-131">Name of hello alert rule.</span></span> |
| <span data-ttu-id="19bad-132">id</span><span class="sxs-lookup"><span data-stu-id="19bad-132">id</span></span> |<span data-ttu-id="19bad-133">ID de ressource d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-133">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="19bad-134">description</span><span class="sxs-lookup"><span data-stu-id="19bad-134">description</span></span> |<span data-ttu-id="19bad-135">Description de l’alerte définie lors de l’alerte de hello est créée.</span><span class="sxs-lookup"><span data-stu-id="19bad-135">Alert description set when hello alert is created.</span></span> |
| <span data-ttu-id="19bad-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="19bad-136">subscriptionId</span></span> |<span data-ttu-id="19bad-137">ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="19bad-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="19bad-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="19bad-138">timestamp</span></span> |<span data-ttu-id="19bad-139">Heure à quels hello événement a été généré par hello service Azure qui a traité la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-139">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="19bad-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="19bad-140">resourceId</span></span> |<span data-ttu-id="19bad-141">ID de ressource de hello affectées les ressources.</span><span class="sxs-lookup"><span data-stu-id="19bad-141">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="19bad-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="19bad-142">resourceGroupName</span></span> |<span data-ttu-id="19bad-143">Nom du groupe de ressources hello pour hello incidence sur la ressource.</span><span class="sxs-lookup"><span data-stu-id="19bad-143">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="19bad-144">properties</span><span class="sxs-lookup"><span data-stu-id="19bad-144">properties</span></span> |<span data-ttu-id="19bad-145">Jeu de `<Key, Value>` paires (autrement dit, `Dictionary<String, String>`) qui inclut des détails sur l’événement hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="19bad-146">event</span><span class="sxs-lookup"><span data-stu-id="19bad-146">event</span></span> |<span data-ttu-id="19bad-147">Élément qui contient des métadonnées sur l’événement hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-147">Element that contains metadata about hello event.</span></span> |
| <span data-ttu-id="19bad-148">autorisation</span><span class="sxs-lookup"><span data-stu-id="19bad-148">authorization</span></span> |<span data-ttu-id="19bad-149">propriétés de contrôle d’accès en fonction du rôle Hello d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-149">hello Role-Based Access Control properties of hello event.</span></span> <span data-ttu-id="19bad-150">Ces propriétés incluent généralement l’action de hello, le rôle de hello et étendue de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-150">These properties usually include hello action, hello role, and hello scope.</span></span> |
| <span data-ttu-id="19bad-151">category</span><span class="sxs-lookup"><span data-stu-id="19bad-151">category</span></span> |<span data-ttu-id="19bad-152">Catégorie d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-152">Category of hello event.</span></span> <span data-ttu-id="19bad-153">Les valeurs prises en charge sont : Administrative, Alert, Security, ServiceHealth et Recommendation.</span><span class="sxs-lookup"><span data-stu-id="19bad-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="19bad-154">caller</span><span class="sxs-lookup"><span data-stu-id="19bad-154">caller</span></span> |<span data-ttu-id="19bad-155">Adresse de messagerie de l’utilisateur hello qui a effectué l’opération de hello, revendication UPN ou revendication SPN basée sur la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="19bad-155">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="19bad-156">Peut être null pour certains appels système.</span><span class="sxs-lookup"><span data-stu-id="19bad-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="19bad-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="19bad-157">correlationId</span></span> |<span data-ttu-id="19bad-158">Généralement un GUID au format chaîne.</span><span class="sxs-lookup"><span data-stu-id="19bad-158">Usually a GUID in string format.</span></span> <span data-ttu-id="19bad-159">Les événements avec l’ID de corrélation appartiennent toohello même action plus importante et partagent généralement un ID de corrélation.</span><span class="sxs-lookup"><span data-stu-id="19bad-159">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="19bad-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="19bad-160">eventDescription</span></span> |<span data-ttu-id="19bad-161">Description de texte statique de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-161">Static text description of hello event.</span></span> |
| <span data-ttu-id="19bad-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="19bad-162">eventDataId</span></span> |<span data-ttu-id="19bad-163">Identificateur unique de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-163">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="19bad-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="19bad-164">eventSource</span></span> |<span data-ttu-id="19bad-165">Nom de hello service Azure ou infrastructure que l’événement hello généré.</span><span class="sxs-lookup"><span data-stu-id="19bad-165">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="19bad-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="19bad-166">httpRequest</span></span> |<span data-ttu-id="19bad-167">Hello demande inclut généralement hello clientRequestId clientIpAddress et la méthode HTTP (par exemple, PUT).</span><span class="sxs-lookup"><span data-stu-id="19bad-167">hello request usually includes hello clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="19bad-168">level</span><span class="sxs-lookup"><span data-stu-id="19bad-168">level</span></span> |<span data-ttu-id="19bad-169">Une des valeurs suivantes de hello : critique, erreur, avertissement, information et Verbose.</span><span class="sxs-lookup"><span data-stu-id="19bad-169">One of hello following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="19bad-170">operationId</span><span class="sxs-lookup"><span data-stu-id="19bad-170">operationId</span></span> |<span data-ttu-id="19bad-171">Généralement GUID partagé entre les événements hello correspondant toosingle opération.</span><span class="sxs-lookup"><span data-stu-id="19bad-171">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="19bad-172">operationName</span><span class="sxs-lookup"><span data-stu-id="19bad-172">operationName</span></span> |<span data-ttu-id="19bad-173">Nom de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-173">Name of hello operation.</span></span> |
| <span data-ttu-id="19bad-174">properties</span><span class="sxs-lookup"><span data-stu-id="19bad-174">properties</span></span> |<span data-ttu-id="19bad-175">Propriétés d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-175">Properties of hello event.</span></span> |
| <span data-ttu-id="19bad-176">status</span><span class="sxs-lookup"><span data-stu-id="19bad-176">status</span></span> |<span data-ttu-id="19bad-177">Chaîne.</span><span class="sxs-lookup"><span data-stu-id="19bad-177">String.</span></span> <span data-ttu-id="19bad-178">État de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="19bad-178">Status of hello operation.</span></span> <span data-ttu-id="19bad-179">Les valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active et Resolved.</span><span class="sxs-lookup"><span data-stu-id="19bad-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="19bad-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="19bad-180">subStatus</span></span> |<span data-ttu-id="19bad-181">Inclut généralement le code d’état HTTP hello d’appel REST hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="19bad-181">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="19bad-182">Peut également inclure d’autres chaînes décrivant un sous-état.</span><span class="sxs-lookup"><span data-stu-id="19bad-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="19bad-183">Les valeurs courantes sont : OK (Code d’état HTTP : 200), Created (Code d’état HTTP : 201), Accepted (Code d’état HTTP : 202), No Content (Code d’état HTTP : 204), Bad Request (Code d’état HTTP : 400), Not Found (Code d’état HTTP : 404), Conflict (Code d’état HTTP : 409), Internal Server Error (Code d’état HTTP : 500), Service Unavailable (Code d’état HTTP : 503) et Gateway Timeout (Code d’état HTTP : 504).</span><span class="sxs-lookup"><span data-stu-id="19bad-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="19bad-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19bad-184">Next steps</span></span>
* <span data-ttu-id="19bad-185">[En savoir plus sur le journal d’activité hello](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="19bad-185">[Learn more about hello activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="19bad-186">[Exécuter des scripts Azure Automation (Runbooks) sur des alertes Azure](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="19bad-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="19bad-187">[Utiliser un toosend d’application logique SMS via Twilio à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="19bad-187">[Use a logic app toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="19bad-188">Cet exemple est pour les alertes de métriques, mais il peut être modifié toowork avec une alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="19bad-188">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="19bad-189">[Utiliser un toosend d’application logique un message de marge d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="19bad-189">[Use a logic app toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="19bad-190">Cet exemple est pour les alertes de métriques, mais il peut être modifié toowork avec une alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="19bad-190">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="19bad-191">[Utiliser un toosend d’application logique de file d’attente un message de tooan Azure à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="19bad-191">[Use a logic app toosend a message tooan Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="19bad-192">Cet exemple est pour les alertes de métriques, mais il peut être modifié toowork avec une alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="19bad-192">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
