---
title: "Comprendre le schéma Webhook utilisé dans les alertes du journal d’activité | Microsoft Docs"
description: "Découvrez le schéma du JSON publié sur une URL de Webhook en cas d’activation d’une alerte du journal d’activité."
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
ms.openlocfilehash: 75c71bcd16573d4f4dd3377c623aa9b414aa3906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="2b7b4-103">Webhook des alertes du journal d’activité Azure</span><span class="sxs-lookup"><span data-stu-id="2b7b4-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="2b7b4-104">Dans le cadre de la définition d’un groupe d’actions, vous pouvez configurer des points de terminaison Webhook pour qu’ils reçoivent des notifications d’alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span></span> <span data-ttu-id="2b7b4-105">Grâce aux Webhooks, vous pouvez acheminer ces notifications vers d’autres systèmes à des fins de post-traitement ou d’exécution d’actions personnalisées.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="2b7b4-106">Cet article montre également à quoi ressemble la charge utile d’une requête HTTP POST pour un webhook.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="2b7b4-107">Pour plus d’informations sur les alertes du journal d’activité, découvrez comment [créer des alertes du journal d’activité Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="2b7b4-108">Pour plus d’informations sur les groupes d’actions, découvrez comment [créer des groupes d’actions](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-the-webhook"></a><span data-ttu-id="2b7b4-109">Authentifier le Webhook</span><span class="sxs-lookup"><span data-stu-id="2b7b4-109">Authenticate the webhook</span></span>
<span data-ttu-id="2b7b4-110">Le Webhook peut éventuellement utiliser l’autorisation par jeton à des fins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-110">The webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="2b7b4-111">L’URI du Webhook est enregistrée avec un ID de jeton, par exemple, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="2b7b4-112">Schéma de la charge utile</span><span class="sxs-lookup"><span data-stu-id="2b7b4-112">Payload schema</span></span>
<span data-ttu-id="2b7b4-113">La charge utile JSON contenue dans l’opération POST varie en fonction de champ data.context.activityLog.eventSource de la charge utile.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="2b7b4-114">Courant</span><span class="sxs-lookup"><span data-stu-id="2b7b4-114">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="2b7b4-115">Administratif</span><span class="sxs-lookup"><span data-stu-id="2b7b4-115">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="2b7b4-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="2b7b4-116">ServiceHealth</span></span>
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

<span data-ttu-id="2b7b4-117">Pour obtenir des informations spécifiques au sujet des schémas des alertes du journal d’activité sur les notifications d’intégrité du service, consultez la page [Notifications d’intégrité du service](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="2b7b4-118">Pour obtenir des informations spécifiques au sujet des schémas de toutes les autres alertes du journal d’activité, consultez la page [Vue d’ensemble du journal d’activité Azure](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-118">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="2b7b4-119">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="2b7b4-119">Element name</span></span> | <span data-ttu-id="2b7b4-120">Description</span><span class="sxs-lookup"><span data-stu-id="2b7b4-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b7b4-121">status</span><span class="sxs-lookup"><span data-stu-id="2b7b4-121">status</span></span> |<span data-ttu-id="2b7b4-122">Utilisé pour les alertes de métrique.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-122">Used for metric alerts.</span></span> <span data-ttu-id="2b7b4-123">Toujours défini sur « activé » pour les alertes du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-123">Always set to "activated" for activity log alerts.</span></span> |
| <span data-ttu-id="2b7b4-124">context</span><span class="sxs-lookup"><span data-stu-id="2b7b4-124">context</span></span> |<span data-ttu-id="2b7b4-125">Contexte de l’événement.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-125">Context of the event.</span></span> |
| <span data-ttu-id="2b7b4-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="2b7b4-126">resourceProviderName</span></span> |<span data-ttu-id="2b7b4-127">Fournisseur de la ressource affectée.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-127">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="2b7b4-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="2b7b4-128">conditionType</span></span> |<span data-ttu-id="2b7b4-129">Toujours défini sur « Event ».</span><span class="sxs-lookup"><span data-stu-id="2b7b4-129">Always "Event."</span></span> |
| <span data-ttu-id="2b7b4-130">name</span><span class="sxs-lookup"><span data-stu-id="2b7b4-130">name</span></span> |<span data-ttu-id="2b7b4-131">Nom de la règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-131">Name of the alert rule.</span></span> |
| <span data-ttu-id="2b7b4-132">id</span><span class="sxs-lookup"><span data-stu-id="2b7b4-132">id</span></span> |<span data-ttu-id="2b7b4-133">ID de ressource de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-133">Resource ID of the alert.</span></span> |
| <span data-ttu-id="2b7b4-134">description</span><span class="sxs-lookup"><span data-stu-id="2b7b4-134">description</span></span> |<span data-ttu-id="2b7b4-135">Description de l’alerte définie à la création de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-135">Alert description set when the alert is created.</span></span> |
| <span data-ttu-id="2b7b4-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="2b7b4-136">subscriptionId</span></span> |<span data-ttu-id="2b7b4-137">ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="2b7b4-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="2b7b4-138">timestamp</span></span> |<span data-ttu-id="2b7b4-139">Heure à laquelle l’événement a été généré par le service Azure qui a traité la demande.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-139">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="2b7b4-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="2b7b4-140">resourceId</span></span> |<span data-ttu-id="2b7b4-141">ID de ressource de la ressource affectée.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-141">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="2b7b4-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2b7b4-142">resourceGroupName</span></span> |<span data-ttu-id="2b7b4-143">Nom du groupe de ressources de la ressource affectée.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-143">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="2b7b4-144">properties</span><span class="sxs-lookup"><span data-stu-id="2b7b4-144">properties</span></span> |<span data-ttu-id="2b7b4-145">Ensemble de paires `<Key, Value>` (c’est-à-dire, `Dictionary<String, String>`) incluant des détails sur l’événement.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="2b7b4-146">event</span><span class="sxs-lookup"><span data-stu-id="2b7b4-146">event</span></span> |<span data-ttu-id="2b7b4-147">Élément contenant des métadonnées relatives à l’événement.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-147">Element that contains metadata about the event.</span></span> |
| <span data-ttu-id="2b7b4-148">autorisation</span><span class="sxs-lookup"><span data-stu-id="2b7b4-148">authorization</span></span> |<span data-ttu-id="2b7b4-149">Propriétés de contrôle d’accès en fonction du rôle de l’événement.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-149">The Role-Based Access Control properties of the event.</span></span> <span data-ttu-id="2b7b4-150">Il s’agit généralement de l’action, du rôle et de l’étendue.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-150">These properties usually include the action, the role, and the scope.</span></span> |
| <span data-ttu-id="2b7b4-151">category</span><span class="sxs-lookup"><span data-stu-id="2b7b4-151">category</span></span> |<span data-ttu-id="2b7b4-152">Catégorie de l’événement.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-152">Category of the event.</span></span> <span data-ttu-id="2b7b4-153">Les valeurs prises en charge sont : Administrative, Alert, Security, ServiceHealth et Recommendation.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="2b7b4-154">caller</span><span class="sxs-lookup"><span data-stu-id="2b7b4-154">caller</span></span> |<span data-ttu-id="2b7b4-155">Adresse e-mail de l’utilisateur ayant effectué l’opération, la revendication de nom d’utilisateur principal (UPN) ou la revendication de nom de principal du service (SPN) basée sur la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-155">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="2b7b4-156">Peut être null pour certains appels système.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="2b7b4-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="2b7b4-157">correlationId</span></span> |<span data-ttu-id="2b7b4-158">Généralement un GUID au format chaîne.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-158">Usually a GUID in string format.</span></span> <span data-ttu-id="2b7b4-159">Les événements avec correlationId appartiennent à la même action et partagent généralement un correlationId.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-159">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="2b7b4-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="2b7b4-160">eventDescription</span></span> |<span data-ttu-id="2b7b4-161">Description textuelle statique de l’événement.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-161">Static text description of the event.</span></span> |
| <span data-ttu-id="2b7b4-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="2b7b4-162">eventDataId</span></span> |<span data-ttu-id="2b7b4-163">Identificateur unique de l’événement.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-163">Unique identifier for the event.</span></span> |
| <span data-ttu-id="2b7b4-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="2b7b4-164">eventSource</span></span> |<span data-ttu-id="2b7b4-165">Nom de l’infrastructure ou du service Azure ayant généré l’événement.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-165">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="2b7b4-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="2b7b4-166">httpRequest</span></span> |<span data-ttu-id="2b7b4-167">Il s’agit généralement des requêtes clientRequestId, clientIpAddress et de la méthode HTTP (PUT, par exemple).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-167">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="2b7b4-168">level</span><span class="sxs-lookup"><span data-stu-id="2b7b4-168">level</span></span> |<span data-ttu-id="2b7b4-169">L’une des valeurs suivantes : Critical, Error, Warning, Informational et Verbose.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-169">One of the following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="2b7b4-170">operationId</span><span class="sxs-lookup"><span data-stu-id="2b7b4-170">operationId</span></span> |<span data-ttu-id="2b7b4-171">Généralement, GUID partagé par les événements correspondant à une opération unique.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-171">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="2b7b4-172">operationName</span><span class="sxs-lookup"><span data-stu-id="2b7b4-172">operationName</span></span> |<span data-ttu-id="2b7b4-173">Nom de l’opération.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-173">Name of the operation.</span></span> |
| <span data-ttu-id="2b7b4-174">properties</span><span class="sxs-lookup"><span data-stu-id="2b7b4-174">properties</span></span> |<span data-ttu-id="2b7b4-175">Les propriétés de l’événement.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-175">Properties of the event.</span></span> |
| <span data-ttu-id="2b7b4-176">status</span><span class="sxs-lookup"><span data-stu-id="2b7b4-176">status</span></span> |<span data-ttu-id="2b7b4-177">Chaîne.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-177">String.</span></span> <span data-ttu-id="2b7b4-178">État de l’opération.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-178">Status of the operation.</span></span> <span data-ttu-id="2b7b4-179">Les valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active et Resolved.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="2b7b4-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="2b7b4-180">subStatus</span></span> |<span data-ttu-id="2b7b4-181">Inclut généralement le code d’état HTTP de l’appel REST correspondant.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-181">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="2b7b4-182">Peut également inclure d’autres chaînes décrivant un sous-état.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="2b7b4-183">Les valeurs courantes sont : OK (Code d’état HTTP : 200), Created (Code d’état HTTP : 201), Accepted (Code d’état HTTP : 202), No Content (Code d’état HTTP : 204), Bad Request (Code d’état HTTP : 400), Not Found (Code d’état HTTP : 404), Conflict (Code d’état HTTP : 409), Internal Server Error (Code d’état HTTP : 500), Service Unavailable (Code d’état HTTP : 503) et Gateway Timeout (Code d’état HTTP : 504).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2b7b4-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2b7b4-184">Next steps</span></span>
* <span data-ttu-id="2b7b4-185">[En savoir plus sur le journal d’activité](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-185">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="2b7b4-186">[Exécuter des scripts Azure Automation (Runbooks) sur des alertes Azure](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="2b7b4-187">[Utiliser une application logique pour envoyer un SMS par le biais de Twilio à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-187">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="2b7b4-188">Cet exemple s’applique aux alertes de métrique, mais il peut être modifié pour fonctionner avec une alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-188">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="2b7b4-189">[Utiliser une application logique pour envoyer un message Slack à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-189">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="2b7b4-190">Cet exemple s’applique aux alertes de métrique, mais il peut être modifié pour fonctionner avec une alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-190">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="2b7b4-191">[Utiliser une application logique pour envoyer un message à une file d’attente Azure à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="2b7b4-191">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="2b7b4-192">Cet exemple s’applique aux alertes de métrique, mais il peut être modifié pour fonctionner avec une alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="2b7b4-192">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
