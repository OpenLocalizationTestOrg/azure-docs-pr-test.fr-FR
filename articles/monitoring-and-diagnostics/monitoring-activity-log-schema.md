---
title: "Schéma d’événements du journal d’activité Azure | Documents Microsoft"
description: "Comprendre le schéma d’événement pour les données émises dans le journal d’activité"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: a4ceb822e0ec3e1c1dc31ece1db761834e795f6c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="6718e-103">Schéma d’événements du journal d’activité</span><span class="sxs-lookup"><span data-stu-id="6718e-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="6718e-104">Le **Journal d’activité Azure** est un journal qui fournit un aperçu de tous les événements de niveau d’abonnement qui se sont produits dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6718e-104">The **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="6718e-105">Cet article décrit le schéma d’événements par catégorie de données.</span><span class="sxs-lookup"><span data-stu-id="6718e-105">This article describes the event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="6718e-106">Administratif</span><span class="sxs-lookup"><span data-stu-id="6718e-106">Administrative</span></span>
<span data-ttu-id="6718e-107">Cette catégorie contient l’enregistrement de toutes les opérations de création, mise à jour, suppression et action effectuées par le biais du gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="6718e-107">This category contains the record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="6718e-108">Les exemples de types d’événements que vous pouvez voir dans cette catégorie incluent « créer une machine virtuelle » et « supprimer un groupe de sécurité réseau ». Toute mesure prise par un utilisateur ou une application utilisant le gestionnaire de ressources est modélisée comme une opération sur un type de ressources en particulier.</span><span class="sxs-lookup"><span data-stu-id="6718e-108">Examples of the types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="6718e-109">Si le type d’opération est Écrire, Supprimer ou Action, les enregistrements de début et de réussite ou d’échec de cette opération sont enregistrés dans la catégorie Administrative.</span><span class="sxs-lookup"><span data-stu-id="6718e-109">If the operation type is Write, Delete, or Action, the records of both the start and success or fail of that operation are recorded in the Administrative category.</span></span> <span data-ttu-id="6718e-110">La catégorie Administrative inclut également toute modification apportée à un contrôle d’accès basé sur un rôle dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="6718e-110">The Administrative category also includes any changes to role-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="6718e-111">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="6718e-111">Sample event</span></span>
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="6718e-112">Description des propriétés</span><span class="sxs-lookup"><span data-stu-id="6718e-112">Property descriptions</span></span>
| <span data-ttu-id="6718e-113">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="6718e-113">Element Name</span></span> | <span data-ttu-id="6718e-114">Description</span><span class="sxs-lookup"><span data-stu-id="6718e-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6718e-115">autorisation</span><span class="sxs-lookup"><span data-stu-id="6718e-115">authorization</span></span> |<span data-ttu-id="6718e-116">Objet blob des propriétés RBAC de l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-116">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="6718e-117">Inclut généralement les propriétés « action », « role » et « scope ».</span><span class="sxs-lookup"><span data-stu-id="6718e-117">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="6718e-118">caller</span><span class="sxs-lookup"><span data-stu-id="6718e-118">caller</span></span> |<span data-ttu-id="6718e-119">Adresse e-mail de l’utilisateur qui a effectué l’opération, la revendication UPN ou la revendication SPN basée sur la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="6718e-119">Email address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="6718e-120">channels</span><span class="sxs-lookup"><span data-stu-id="6718e-120">channels</span></span> |<span data-ttu-id="6718e-121">L’une des valeurs suivantes : « Admin », « Operation ».</span><span class="sxs-lookup"><span data-stu-id="6718e-121">One of the following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="6718e-122">réclamations</span><span class="sxs-lookup"><span data-stu-id="6718e-122">claims</span></span> |<span data-ttu-id="6718e-123">Le jeton JWT utilisé par Active Directory pour authentifier l’utilisateur ou l’application afin d’effectuer cette opération dans le gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="6718e-123">The JWT token used by Active Directory to authenticate the user or application to perform this operation in resource manager.</span></span> |
| <span data-ttu-id="6718e-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="6718e-124">correlationId</span></span> |<span data-ttu-id="6718e-125">Généralement un GUID au format chaîne.</span><span class="sxs-lookup"><span data-stu-id="6718e-125">Usually a GUID in the string format.</span></span> <span data-ttu-id="6718e-126">Les événements qui partagent un correlationId appartiennent à la même action uber.</span><span class="sxs-lookup"><span data-stu-id="6718e-126">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="6718e-127">description</span><span class="sxs-lookup"><span data-stu-id="6718e-127">description</span></span> |<span data-ttu-id="6718e-128">Description textuelle statique d’un événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-128">Static text description of an event.</span></span> |
| <span data-ttu-id="6718e-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="6718e-129">eventDataId</span></span> |<span data-ttu-id="6718e-130">Identificateur unique d’un événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="6718e-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="6718e-131">httpRequest</span></span> |<span data-ttu-id="6718e-132">Objet blob décrivant la requête Http.</span><span class="sxs-lookup"><span data-stu-id="6718e-132">Blob describing the Http Request.</span></span> <span data-ttu-id="6718e-133">Inclut généralement clientRequestId, clientIpAddress et la méthode (méthode HTTP.</span><span class="sxs-lookup"><span data-stu-id="6718e-133">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="6718e-134">Par exemple, PUT).</span><span class="sxs-lookup"><span data-stu-id="6718e-134">For example, PUT).</span></span> |
| <span data-ttu-id="6718e-135">minimal</span><span class="sxs-lookup"><span data-stu-id="6718e-135">level</span></span> |<span data-ttu-id="6718e-136">Niveau de l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-136">Level of the event.</span></span> <span data-ttu-id="6718e-137">Une des valeurs suivantes : Critical, Error, Warning, Informational et Verbose</span><span class="sxs-lookup"><span data-stu-id="6718e-137">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="6718e-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="6718e-138">resourceGroupName</span></span> |<span data-ttu-id="6718e-139">Nom du groupe de ressources de la ressource affectée.</span><span class="sxs-lookup"><span data-stu-id="6718e-139">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="6718e-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="6718e-140">resourceProviderName</span></span> |<span data-ttu-id="6718e-141">Nom du fournisseur de ressources de la ressource affectée.</span><span class="sxs-lookup"><span data-stu-id="6718e-141">Name of the resource provider for the impacted resource</span></span> |
| <span data-ttu-id="6718e-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="6718e-142">resourceId</span></span> |<span data-ttu-id="6718e-143">ID de ressource de la ressource affectée.</span><span class="sxs-lookup"><span data-stu-id="6718e-143">Resource id of the impacted resource.</span></span> |
| <span data-ttu-id="6718e-144">operationId</span><span class="sxs-lookup"><span data-stu-id="6718e-144">operationId</span></span> |<span data-ttu-id="6718e-145">Un GUID partagé par les événements correspondant à une opération unique.</span><span class="sxs-lookup"><span data-stu-id="6718e-145">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="6718e-146">operationName</span><span class="sxs-lookup"><span data-stu-id="6718e-146">operationName</span></span> |<span data-ttu-id="6718e-147">Nom de l’opération.</span><span class="sxs-lookup"><span data-stu-id="6718e-147">Name of the operation.</span></span> |
| <span data-ttu-id="6718e-148">properties</span><span class="sxs-lookup"><span data-stu-id="6718e-148">properties</span></span> |<span data-ttu-id="6718e-149">Jeu de paires `<Key, Value>` (c’est-à-dire Dictionary) décrivant les détails de l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="6718e-150">status</span><span class="sxs-lookup"><span data-stu-id="6718e-150">status</span></span> |<span data-ttu-id="6718e-151">Chaîne décrivant l’état de l’opération.</span><span class="sxs-lookup"><span data-stu-id="6718e-151">String describing the status of the operation.</span></span> <span data-ttu-id="6718e-152">Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="6718e-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="6718e-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="6718e-153">subStatus</span></span> |<span data-ttu-id="6718e-154">Il s’agit généralement du code d’état HHTP de l’appel REST correspondant, mais également d’autres chaînes décrivant un sous-état, comme ces valeurs courantes : OK (Code d’état HTTP : 200), Created (Code d’état HTTP : 201), Accepted (Code d’état HTTP : 202), No content (Code d’état HTTP : 204), Bad Request (Code d’état HTTP : 400), Not found (Code d’état HTTP : 404), Conflict (Code d’état HTTP : 409), Internal Server Error (Code d’état HTTP : 500), Service Unavailable (Code d’état HTTP : 503), Gateway Timeout (Code d’état HTTP : 504).</span><span class="sxs-lookup"><span data-stu-id="6718e-154">Usually the HTTP status code of the corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="6718e-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="6718e-155">eventTimestamp</span></span> |<span data-ttu-id="6718e-156">Horodatage lorsque l’événement a été généré par le service Azure traitant la demande correspondant à l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-156">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="6718e-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="6718e-157">submissionTimestamp</span></span> |<span data-ttu-id="6718e-158">Horodatage lorsque l’événement est devenu disponible pour l’interrogation.</span><span class="sxs-lookup"><span data-stu-id="6718e-158">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="6718e-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="6718e-159">subscriptionId</span></span> |<span data-ttu-id="6718e-160">ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6718e-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="6718e-161">État d’intégrité du service</span><span class="sxs-lookup"><span data-stu-id="6718e-161">Service health</span></span>
<span data-ttu-id="6718e-162">Cette catégorie contient l’enregistrement de tout incident de l’état d’intégrité du service qui se sont produits dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6718e-162">This category contains the record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="6718e-163">Un exemple du type d’événement que vous pouvez voir dans cette catégorie est « SQL Azure dans l’est des États-Unis rencontre des temps d’arrêt. »</span><span class="sxs-lookup"><span data-stu-id="6718e-163">An example of the type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="6718e-164">Les événements de l’état d’intégrité du service se présentent sous cinq variétés : action requise, récupération assistée, incident, maintenance, informations ou sécurité et n’apparaissent que si une ressource de votre abonnement est affectée par l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in the subscription that would be impacted by the event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="6718e-165">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="6718e-165">Sample event</span></span>
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="6718e-166">Description des propriétés</span><span class="sxs-lookup"><span data-stu-id="6718e-166">Property descriptions</span></span>
<span data-ttu-id="6718e-167">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="6718e-167">Element Name</span></span> | <span data-ttu-id="6718e-168">Description</span><span class="sxs-lookup"><span data-stu-id="6718e-168">Description</span></span>
-------- | -----------
<span data-ttu-id="6718e-169">channels</span><span class="sxs-lookup"><span data-stu-id="6718e-169">channels</span></span> | <span data-ttu-id="6718e-170">Est une des valeurs suivantes : « Admin », « Operation »</span><span class="sxs-lookup"><span data-stu-id="6718e-170">Is one of the following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="6718e-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="6718e-171">correlationId</span></span> | <span data-ttu-id="6718e-172">Est généralement un GUID au format chaîne.</span><span class="sxs-lookup"><span data-stu-id="6718e-172">Is usually a GUID in the string format.</span></span> <span data-ttu-id="6718e-173">Les événements qui appartiennent à la même action uber partagent généralement le même correlationId.</span><span class="sxs-lookup"><span data-stu-id="6718e-173">Events with that belong to the same uber action usually share the same correlationId.</span></span>
<span data-ttu-id="6718e-174">Description</span><span class="sxs-lookup"><span data-stu-id="6718e-174">description</span></span> | <span data-ttu-id="6718e-175">Description de l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-175">Description of the event.</span></span>
<span data-ttu-id="6718e-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="6718e-176">eventDataId</span></span> | <span data-ttu-id="6718e-177">L’identificateur unique d’un événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-177">The unique identifier of an event.</span></span>
<span data-ttu-id="6718e-178">eventName</span><span class="sxs-lookup"><span data-stu-id="6718e-178">eventName</span></span> | <span data-ttu-id="6718e-179">Le titre de l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-179">The title of the event.</span></span>
<span data-ttu-id="6718e-180">level</span><span class="sxs-lookup"><span data-stu-id="6718e-180">level</span></span> | <span data-ttu-id="6718e-181">Niveau de l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-181">Level of the event.</span></span> <span data-ttu-id="6718e-182">Une des valeurs suivantes : Critical, Error, Warning, Informational et Verbose</span><span class="sxs-lookup"><span data-stu-id="6718e-182">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="6718e-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="6718e-183">resourceProviderName</span></span> | <span data-ttu-id="6718e-184">Nom du fournisseur de ressources de la ressource affectée.</span><span class="sxs-lookup"><span data-stu-id="6718e-184">Name of the resource provider for the impacted resource.</span></span> <span data-ttu-id="6718e-185">S’il est inconnu, cette option sera nulle.</span><span class="sxs-lookup"><span data-stu-id="6718e-185">If not known, this will be null.</span></span>
<span data-ttu-id="6718e-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="6718e-186">resourceType</span></span>| <span data-ttu-id="6718e-187">Le type de ressource de la ressource affectée.</span><span class="sxs-lookup"><span data-stu-id="6718e-187">The type of resource of the impacted resource.</span></span> <span data-ttu-id="6718e-188">S’il est inconnu, cette option sera nulle.</span><span class="sxs-lookup"><span data-stu-id="6718e-188">If not known, this will be null.</span></span>
<span data-ttu-id="6718e-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="6718e-189">subStatus</span></span> | <span data-ttu-id="6718e-190">Généralement nul pour les événements de l’état d’intégrité du service.</span><span class="sxs-lookup"><span data-stu-id="6718e-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="6718e-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="6718e-191">eventTimestamp</span></span> | <span data-ttu-id="6718e-192">Horodatage lorsque l’événement du journal a été généré et envoyé au journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="6718e-192">Timestamp when the log event was generated and submitted to the Activity Log.</span></span>
<span data-ttu-id="6718e-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="6718e-193">submissionTimestamp</span></span> |   <span data-ttu-id="6718e-194">Horodatage lorsque l’événement est devenu disponible dans le journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="6718e-194">Timestamp when the event became available in the Activity Log.</span></span>
<span data-ttu-id="6718e-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="6718e-195">subscriptionId</span></span> | <span data-ttu-id="6718e-196">L’abonnement Azure dans lequel l’événement est enregistré.</span><span class="sxs-lookup"><span data-stu-id="6718e-196">The Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="6718e-197">status</span><span class="sxs-lookup"><span data-stu-id="6718e-197">status</span></span> | <span data-ttu-id="6718e-198">Chaîne décrivant l’état de l’opération.</span><span class="sxs-lookup"><span data-stu-id="6718e-198">String describing the status of the operation.</span></span> <span data-ttu-id="6718e-199">Certaines valeurs courantes sont : actif, résolu.</span><span class="sxs-lookup"><span data-stu-id="6718e-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="6718e-200">operationName</span><span class="sxs-lookup"><span data-stu-id="6718e-200">operationName</span></span> | <span data-ttu-id="6718e-201">Le nom de l’opération.</span><span class="sxs-lookup"><span data-stu-id="6718e-201">Name of the operation.</span></span> <span data-ttu-id="6718e-202">Généralement Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="6718e-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="6718e-203">category</span><span class="sxs-lookup"><span data-stu-id="6718e-203">category</span></span> | <span data-ttu-id="6718e-204">« ServiceHealth »</span><span class="sxs-lookup"><span data-stu-id="6718e-204">"ServiceHealth"</span></span>
<span data-ttu-id="6718e-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="6718e-205">resourceId</span></span> | <span data-ttu-id="6718e-206">ID ressource de la ressource affectée, s’il est connu.</span><span class="sxs-lookup"><span data-stu-id="6718e-206">Resource id of the impacted resource, if known.</span></span> <span data-ttu-id="6718e-207">L’ID d’abonnement est fourni dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="6718e-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="6718e-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="6718e-208">Properties.title</span></span> | <span data-ttu-id="6718e-209">Le titre localisé pour cette communication.</span><span class="sxs-lookup"><span data-stu-id="6718e-209">The localized title for this communication.</span></span> <span data-ttu-id="6718e-210">La langue par défaut est l’anglais.</span><span class="sxs-lookup"><span data-stu-id="6718e-210">English is the default language.</span></span>
<span data-ttu-id="6718e-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="6718e-211">Properties.communication</span></span> | <span data-ttu-id="6718e-212">Les détails localisés de la communication avec le balisage HTML.</span><span class="sxs-lookup"><span data-stu-id="6718e-212">The localized details of the communication with HTML markup.</span></span> <span data-ttu-id="6718e-213">L’anglais est la langue par défaut.</span><span class="sxs-lookup"><span data-stu-id="6718e-213">English is the default.</span></span>
<span data-ttu-id="6718e-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="6718e-214">Properties.incidentType</span></span> | <span data-ttu-id="6718e-215">valeurs possibles : AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span><span class="sxs-lookup"><span data-stu-id="6718e-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="6718e-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="6718e-216">Properties.trackingId</span></span> | <span data-ttu-id="6718e-217">Identifie l’incident associé à cet événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-217">Identifies the incident this event is associated with.</span></span> <span data-ttu-id="6718e-218">Cela permet de mettre en corrélation les événements liés à un incident.</span><span class="sxs-lookup"><span data-stu-id="6718e-218">Use this to correlate the events related to an incident.</span></span>
<span data-ttu-id="6718e-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="6718e-219">Properties.impactedServices</span></span> | <span data-ttu-id="6718e-220">Un échappement blob JSON qui décrit les services et régions qui sont affectés par l’incident.</span><span class="sxs-lookup"><span data-stu-id="6718e-220">An escaped JSON blob which describes the services and regions that are impacted by the incident.</span></span> <span data-ttu-id="6718e-221">Une liste de services, chacun possédant un ServiceName et une liste d’ImpactedRegions, chacune ayant un RegionName.</span><span class="sxs-lookup"><span data-stu-id="6718e-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="6718e-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="6718e-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="6718e-223">La communication en anglais</span><span class="sxs-lookup"><span data-stu-id="6718e-223">The communication in English</span></span>
<span data-ttu-id="6718e-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="6718e-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="6718e-225">La communication en anglais en tant que HTML ou texte brut</span><span class="sxs-lookup"><span data-stu-id="6718e-225">The communication in English as either html markup or plain text</span></span>
<span data-ttu-id="6718e-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="6718e-226">Properties.stage</span></span> | <span data-ttu-id="6718e-227">Les valeurs possibles pour AssistedRecovery, ActionRequired, Information, Incident et Security sont Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="6718e-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="6718e-228">Pour Maintenance, les valeurs possibles sont Active, Planned, InProgress, Canceled, Rescheduled, Resolved et Complete</span><span class="sxs-lookup"><span data-stu-id="6718e-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="6718e-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="6718e-229">Properties.communicationId</span></span> | <span data-ttu-id="6718e-230">La communication associée à cet événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-230">The communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="6718e-231">Alerte</span><span class="sxs-lookup"><span data-stu-id="6718e-231">Alert</span></span>
<span data-ttu-id="6718e-232">Cette catégorie contient l’enregistrement de toutes les activations des alertes Azure.</span><span class="sxs-lookup"><span data-stu-id="6718e-232">This category contains the record of all activations of Azure alerts.</span></span> <span data-ttu-id="6718e-233">Un exemple du type d’événement que vous pouvez voir dans cette catégorie est « % du processeur sur myVM a été supérieur à 80 pour les 5 dernières minutes. »</span><span class="sxs-lookup"><span data-stu-id="6718e-233">An example of the type of event you would see in this category is "CPU % on myVM has been over 80 for the past 5 minutes."</span></span> <span data-ttu-id="6718e-234">Une variété de systèmes Azure possèdent un concept d’alertes : vous pouvez définir une règle quelconque et recevoir une notification lorsque les conditions correspondent à cette règle.</span><span class="sxs-lookup"><span data-stu-id="6718e-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="6718e-235">Chaque fois qu’un type d’alerte Azure pris en charge « s’active » ou si les conditions sont remplies pour générer une notification, un enregistrement de l’activation est également envoyé à cette catégorie du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="6718e-235">Each time a supported Azure alert type 'activates,' or the conditions are met to generate a notification, a record of the activation is also pushed to this category of the Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="6718e-236">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="6718e-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in the last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="6718e-237">Description des propriétés</span><span class="sxs-lookup"><span data-stu-id="6718e-237">Property descriptions</span></span>
| <span data-ttu-id="6718e-238">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="6718e-238">Element Name</span></span> | <span data-ttu-id="6718e-239">Description</span><span class="sxs-lookup"><span data-stu-id="6718e-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6718e-240">caller</span><span class="sxs-lookup"><span data-stu-id="6718e-240">caller</span></span> | <span data-ttu-id="6718e-241">Toujours Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="6718e-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="6718e-242">channels</span><span class="sxs-lookup"><span data-stu-id="6718e-242">channels</span></span> | <span data-ttu-id="6718e-243">Toujours « Admin, opération »</span><span class="sxs-lookup"><span data-stu-id="6718e-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="6718e-244">réclamations</span><span class="sxs-lookup"><span data-stu-id="6718e-244">claims</span></span> | <span data-ttu-id="6718e-245">Objet blob JSON avec le type de SPN (nom principal de service) ou de ressource du moteur d’alertes.</span><span class="sxs-lookup"><span data-stu-id="6718e-245">JSON blob with the SPN (service principal name), or resource type, of the alert engine.</span></span> |
| <span data-ttu-id="6718e-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="6718e-246">correlationId</span></span> | <span data-ttu-id="6718e-247">Un GUID au format chaîne.</span><span class="sxs-lookup"><span data-stu-id="6718e-247">A GUID in the string format.</span></span> |
| <span data-ttu-id="6718e-248">Description</span><span class="sxs-lookup"><span data-stu-id="6718e-248">description</span></span> |<span data-ttu-id="6718e-249">Description textuelle statique de l’événement d’alerte.</span><span class="sxs-lookup"><span data-stu-id="6718e-249">Static text description of the alert event.</span></span> |
| <span data-ttu-id="6718e-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="6718e-250">eventDataId</span></span> |<span data-ttu-id="6718e-251">Identificateur unique de l'événement d’alerte.</span><span class="sxs-lookup"><span data-stu-id="6718e-251">Unique identifier of the alert event.</span></span> |
| <span data-ttu-id="6718e-252">level</span><span class="sxs-lookup"><span data-stu-id="6718e-252">level</span></span> |<span data-ttu-id="6718e-253">Niveau de l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-253">Level of the event.</span></span> <span data-ttu-id="6718e-254">Une des valeurs suivantes : Critical, Error, Warning, Informational et Verbose</span><span class="sxs-lookup"><span data-stu-id="6718e-254">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="6718e-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="6718e-255">resourceGroupName</span></span> |<span data-ttu-id="6718e-256">Nom du groupe de ressources de la ressource affectée s’il s’agit d’une alerte métrique.</span><span class="sxs-lookup"><span data-stu-id="6718e-256">Name of the resource group for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="6718e-257">Pour les autres types d’alertes, ceci est le nom du groupe de ressources qui contient l’alerte elle-même.</span><span class="sxs-lookup"><span data-stu-id="6718e-257">For other alert types, this is the name of the resource group that contains the alert itself.</span></span> |
| <span data-ttu-id="6718e-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="6718e-258">resourceProviderName</span></span> |<span data-ttu-id="6718e-259">Nom du fournisseur de ressources de la ressource affectée s’il s’agit d’une alerte métrique.</span><span class="sxs-lookup"><span data-stu-id="6718e-259">Name of the resource provider for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="6718e-260">Pour les autres types d’alertes, ceci est le nom du fournisseur de ressources pour l’alerte elle-même.</span><span class="sxs-lookup"><span data-stu-id="6718e-260">For other alert types, this is the name of the resource provider for the alert itself.</span></span> |
| <span data-ttu-id="6718e-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="6718e-261">resourceId</span></span> | <span data-ttu-id="6718e-262">Nom de l’ID de ressource de la ressource affectée s’il s’agit d’une alerte métrique.</span><span class="sxs-lookup"><span data-stu-id="6718e-262">Name of the resource ID for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="6718e-263">Pour les autres types d’alertes, ceci est le nom de l’ID de ressource pour l’alerte elle-même.</span><span class="sxs-lookup"><span data-stu-id="6718e-263">For other alert types, this is the resource ID of the alert resource itself.</span></span> |
| <span data-ttu-id="6718e-264">operationId</span><span class="sxs-lookup"><span data-stu-id="6718e-264">operationId</span></span> |<span data-ttu-id="6718e-265">Un GUID partagé par les événements correspondant à une opération unique.</span><span class="sxs-lookup"><span data-stu-id="6718e-265">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="6718e-266">operationName</span><span class="sxs-lookup"><span data-stu-id="6718e-266">operationName</span></span> |<span data-ttu-id="6718e-267">Nom de l’opération.</span><span class="sxs-lookup"><span data-stu-id="6718e-267">Name of the operation.</span></span> |
| <span data-ttu-id="6718e-268">properties</span><span class="sxs-lookup"><span data-stu-id="6718e-268">properties</span></span> |<span data-ttu-id="6718e-269">Jeu de paires `<Key, Value>` (c’est-à-dire Dictionary) décrivant les détails de l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="6718e-270">status</span><span class="sxs-lookup"><span data-stu-id="6718e-270">status</span></span> |<span data-ttu-id="6718e-271">Chaîne décrivant l’état de l’opération.</span><span class="sxs-lookup"><span data-stu-id="6718e-271">String describing the status of the operation.</span></span> <span data-ttu-id="6718e-272">Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="6718e-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="6718e-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="6718e-273">subStatus</span></span> | <span data-ttu-id="6718e-274">Généralement, nul pour les alertes.</span><span class="sxs-lookup"><span data-stu-id="6718e-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="6718e-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="6718e-275">eventTimestamp</span></span> |<span data-ttu-id="6718e-276">Horodatage lorsque l’événement a été généré par le service Azure traitant la demande correspondant à l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-276">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="6718e-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="6718e-277">submissionTimestamp</span></span> |<span data-ttu-id="6718e-278">Horodatage lorsque l’événement est devenu disponible pour l’interrogation.</span><span class="sxs-lookup"><span data-stu-id="6718e-278">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="6718e-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="6718e-279">subscriptionId</span></span> |<span data-ttu-id="6718e-280">ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6718e-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="6718e-281">Champ Propriétés par type d’alerte</span><span class="sxs-lookup"><span data-stu-id="6718e-281">Properties field per alert type</span></span>
<span data-ttu-id="6718e-282">Le champ Propriétés contient des valeurs différentes en fonction de la source de l’événement d’alerte.</span><span class="sxs-lookup"><span data-stu-id="6718e-282">The properties field will contain different values depending on the source of the alert event.</span></span> <span data-ttu-id="6718e-283">Deux fournisseurs d’événements d’alertes courants sont les alertes du journal d’activité et les alertes métriques.</span><span class="sxs-lookup"><span data-stu-id="6718e-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="6718e-284">Propriétés pour les alertes du journal d’activité</span><span class="sxs-lookup"><span data-stu-id="6718e-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="6718e-285">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="6718e-285">Element Name</span></span> | <span data-ttu-id="6718e-286">Description</span><span class="sxs-lookup"><span data-stu-id="6718e-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6718e-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="6718e-287">properties.subscriptionId</span></span> | <span data-ttu-id="6718e-288">L’ID d’abonnement depuis l’événement du journal d’activité qui a provoqué l’activation de cette règle d’alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="6718e-288">The subscription ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="6718e-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="6718e-289">properties.eventDataId</span></span> | <span data-ttu-id="6718e-290">L’ID des données de l’événement depuis l’événement du journal d’activité qui a provoqué l’activation de cette règle d’alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="6718e-290">The event data ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="6718e-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="6718e-291">properties.resourceGroup</span></span> | <span data-ttu-id="6718e-292">Le groupe de ressources depuis l’événement du journal d’activité qui a provoqué l’activation de cette règle d’alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="6718e-292">The resource group from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="6718e-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="6718e-293">properties.resourceId</span></span> | <span data-ttu-id="6718e-294">L’ID de ressource depuis l’événement du journal d’activité qui a provoqué l’activation de cette règle d’alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="6718e-294">The resource ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="6718e-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="6718e-295">properties.eventTimestamp</span></span> | <span data-ttu-id="6718e-296">L’horodatage des événements de l’événement du journal d’activité qui a provoqué l’activation de cette règle d’alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="6718e-296">The event timestamp of the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="6718e-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="6718e-297">properties.operationName</span></span> | <span data-ttu-id="6718e-298">Le nom de l’opération depuis l’événement du journal d’activité qui a provoqué l’activation de cette règle d’alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="6718e-298">The operation name from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="6718e-299">Properties.Status</span><span class="sxs-lookup"><span data-stu-id="6718e-299">properties.status</span></span> | <span data-ttu-id="6718e-300">L’état depuis l’événement du journal d’activité qui a provoqué l’activation de cette règle d’alerte du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="6718e-300">The status from the activity log event which caused this activity log alert rule to be activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="6718e-301">Propriétés des alertes métriques</span><span class="sxs-lookup"><span data-stu-id="6718e-301">Properties for metric alerts</span></span>
| <span data-ttu-id="6718e-302">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="6718e-302">Element Name</span></span> | <span data-ttu-id="6718e-303">Description</span><span class="sxs-lookup"><span data-stu-id="6718e-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6718e-304">Propriétés. RuleUri</span><span class="sxs-lookup"><span data-stu-id="6718e-304">properties.RuleUri</span></span> | <span data-ttu-id="6718e-305">L’ID de ressource de la règle d’alerte métrique elle-même.</span><span class="sxs-lookup"><span data-stu-id="6718e-305">Resource ID of the metric alert rule itself.</span></span> |
| <span data-ttu-id="6718e-306">Propriétés. Nom_règle</span><span class="sxs-lookup"><span data-stu-id="6718e-306">properties.RuleName</span></span> | <span data-ttu-id="6718e-307">Le nom de la règle d’alerte métrique.</span><span class="sxs-lookup"><span data-stu-id="6718e-307">The name of the metric alert rule.</span></span> |
| <span data-ttu-id="6718e-308">Propriétés. RuleDescription</span><span class="sxs-lookup"><span data-stu-id="6718e-308">properties.RuleDescription</span></span> | <span data-ttu-id="6718e-309">La description de la règle d’alerte métrique (telle que définie dans la règle d’alerte).</span><span class="sxs-lookup"><span data-stu-id="6718e-309">The description of the metric alert rule (as defined in the alert rule).</span></span> |
| <span data-ttu-id="6718e-310">Propriétés. Seuil</span><span class="sxs-lookup"><span data-stu-id="6718e-310">properties.Threshold</span></span> | <span data-ttu-id="6718e-311">La valeur de seuil utilisée dans l’évaluation de la règle d’alerte métrique.</span><span class="sxs-lookup"><span data-stu-id="6718e-311">The threshold value used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="6718e-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="6718e-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="6718e-313">La taille de la fenêtre utilisée dans l’évaluation de la règle d’alerte métrique.</span><span class="sxs-lookup"><span data-stu-id="6718e-313">The window size used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="6718e-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="6718e-314">properties.Aggregation</span></span> | <span data-ttu-id="6718e-315">Le type d’agrégation défini dans la règle d’alerte métrique.</span><span class="sxs-lookup"><span data-stu-id="6718e-315">The aggregation type defined in the metric alert rule.</span></span> |
| <span data-ttu-id="6718e-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="6718e-316">properties.Operator</span></span> | <span data-ttu-id="6718e-317">L’opérateur conditionnel utilisé dans l’évaluation de la règle d’alerte métrique.</span><span class="sxs-lookup"><span data-stu-id="6718e-317">The conditional operator used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="6718e-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="6718e-318">properties.MetricName</span></span> | <span data-ttu-id="6718e-319">Le nom métrique utilisé dans l’évaluation de la règle d’alerte métrique.</span><span class="sxs-lookup"><span data-stu-id="6718e-319">The metric name of the metric used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="6718e-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="6718e-320">properties.MetricUnit</span></span> | <span data-ttu-id="6718e-321">L’unité métrique utilisée dans l’évaluation de la règle d’alerte métrique.</span><span class="sxs-lookup"><span data-stu-id="6718e-321">The metric unit for the metric used in the evaluation of the metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="6718e-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="6718e-322">Autoscale</span></span>
<span data-ttu-id="6718e-323">Cette catégorie contient l’enregistrement de tous les événements liés au fonctionnement du moteur de mise à l’échelle automatique selon les paramètres d’échelle automatique définis dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6718e-323">This category contains the record of any events related to the operation of the autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="6718e-324">Un exemple du type d’événement que vous pouvez voir dans cette catégorie est « Échec de l’action de monter en puissance de la mise à l’échelle automatique. »</span><span class="sxs-lookup"><span data-stu-id="6718e-324">An example of the type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="6718e-325">À l’aide de la mise à l’échelle automatique, vous pouvez automatiquement augmenter ou diminuer la taille des instances dans un type de ressource pris en charge basé sur l’heure du jour et/ou les données de charge (métriques) à l’aide d’un paramètre de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-325">Using autoscale, you can automatically scale out or scale in the number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="6718e-326">Lorsque les conditions sont remplies pour monter ou descendre en puissance, les événements de démarrage réussis ou échoués sont enregistrés dans cette catégorie.</span><span class="sxs-lookup"><span data-stu-id="6718e-326">When the conditions are met to scale up or down, the start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="6718e-327">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="6718e-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a><span data-ttu-id="6718e-328">Description des propriétés</span><span class="sxs-lookup"><span data-stu-id="6718e-328">Property descriptions</span></span>
| <span data-ttu-id="6718e-329">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="6718e-329">Element Name</span></span> | <span data-ttu-id="6718e-330">Description</span><span class="sxs-lookup"><span data-stu-id="6718e-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6718e-331">caller</span><span class="sxs-lookup"><span data-stu-id="6718e-331">caller</span></span> | <span data-ttu-id="6718e-332">Always Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="6718e-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="6718e-333">channels</span><span class="sxs-lookup"><span data-stu-id="6718e-333">channels</span></span> | <span data-ttu-id="6718e-334">Toujours « Admin, opération »</span><span class="sxs-lookup"><span data-stu-id="6718e-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="6718e-335">réclamations</span><span class="sxs-lookup"><span data-stu-id="6718e-335">claims</span></span> | <span data-ttu-id="6718e-336">Objet blob JSON avec le type de SPN (nom principal de service) ou de ressource du moteur de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-336">JSON blob with the SPN (service principal name), or resource type, of the autoscale engine.</span></span> |
| <span data-ttu-id="6718e-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="6718e-337">correlationId</span></span> | <span data-ttu-id="6718e-338">Un GUID au format chaîne.</span><span class="sxs-lookup"><span data-stu-id="6718e-338">A GUID in the string format.</span></span> |
| <span data-ttu-id="6718e-339">Description</span><span class="sxs-lookup"><span data-stu-id="6718e-339">description</span></span> |<span data-ttu-id="6718e-340">Description textuelle statique de l’événement de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-340">Static text description of the autoscale event.</span></span> |
| <span data-ttu-id="6718e-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="6718e-341">eventDataId</span></span> |<span data-ttu-id="6718e-342">Identificateur unique de l'événement de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-342">Unique identifier of the autoscale event.</span></span> |
| <span data-ttu-id="6718e-343">level</span><span class="sxs-lookup"><span data-stu-id="6718e-343">level</span></span> |<span data-ttu-id="6718e-344">Niveau de l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-344">Level of the event.</span></span> <span data-ttu-id="6718e-345">Une des valeurs suivantes : Critical, Error, Warning, Informational et Verbose</span><span class="sxs-lookup"><span data-stu-id="6718e-345">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="6718e-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="6718e-346">resourceGroupName</span></span> |<span data-ttu-id="6718e-347">Nom du groupe de ressources du paramètre de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-347">Name of the resource group for the autoscale setting.</span></span> |
| <span data-ttu-id="6718e-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="6718e-348">resourceProviderName</span></span> |<span data-ttu-id="6718e-349">Nom du fournisseur de ressources du paramètre de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-349">Name of the resource provider for the autoscale setting.</span></span> |
| <span data-ttu-id="6718e-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="6718e-350">resourceId</span></span> |<span data-ttu-id="6718e-351">ID de ressource du paramètre de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-351">Resource id of the autoscale setting.</span></span> |
| <span data-ttu-id="6718e-352">operationId</span><span class="sxs-lookup"><span data-stu-id="6718e-352">operationId</span></span> |<span data-ttu-id="6718e-353">Un GUID partagé par les événements correspondant à une opération unique.</span><span class="sxs-lookup"><span data-stu-id="6718e-353">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="6718e-354">operationName</span><span class="sxs-lookup"><span data-stu-id="6718e-354">operationName</span></span> |<span data-ttu-id="6718e-355">Nom de l’opération.</span><span class="sxs-lookup"><span data-stu-id="6718e-355">Name of the operation.</span></span> |
| <span data-ttu-id="6718e-356">properties</span><span class="sxs-lookup"><span data-stu-id="6718e-356">properties</span></span> |<span data-ttu-id="6718e-357">Jeu de paires `<Key, Value>` (c’est-à-dire Dictionary) décrivant les détails de l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="6718e-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="6718e-358">properties.Description</span></span> | <span data-ttu-id="6718e-359">Description détaillée de ce que fait le moteur de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-359">Detailed description of what the autoscale engine was doing.</span></span> |
| <span data-ttu-id="6718e-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="6718e-360">properties.ResourceName</span></span> | <span data-ttu-id="6718e-361">ID de ressource de la ressource affectée (la ressource sur laquelle l’action de mise à l’échelle a été effectuée)</span><span class="sxs-lookup"><span data-stu-id="6718e-361">Resource ID of the impacted resource (the resource on which the scale action was being performed)</span></span> |
| <span data-ttu-id="6718e-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="6718e-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="6718e-363">Le nombre d’instances avant la prise d’effet de l’action de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-363">The number of instances before the autoscale action took effect.</span></span> |
| <span data-ttu-id="6718e-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="6718e-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="6718e-365">Le nombre d’instances après la prise d’effet de l’action de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-365">The number of instances after the autoscale action took effect.</span></span> |
| <span data-ttu-id="6718e-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="6718e-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="6718e-367">Horodatage de lorsque l’action de mise à l’échelle s’est produite.</span><span class="sxs-lookup"><span data-stu-id="6718e-367">The timestamp of when the autoscale action occurred.</span></span> |
| <span data-ttu-id="6718e-368">status</span><span class="sxs-lookup"><span data-stu-id="6718e-368">status</span></span> |<span data-ttu-id="6718e-369">Chaîne décrivant l’état de l’opération.</span><span class="sxs-lookup"><span data-stu-id="6718e-369">String describing the status of the operation.</span></span> <span data-ttu-id="6718e-370">Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="6718e-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="6718e-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="6718e-371">subStatus</span></span> | <span data-ttu-id="6718e-372">Généralement, nul pour la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="6718e-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="6718e-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="6718e-373">eventTimestamp</span></span> |<span data-ttu-id="6718e-374">Horodatage lorsque l’événement a été généré par le service Azure traitant la demande correspondant à l’événement.</span><span class="sxs-lookup"><span data-stu-id="6718e-374">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="6718e-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="6718e-375">submissionTimestamp</span></span> |<span data-ttu-id="6718e-376">Horodatage lorsque l’événement est devenu disponible pour l’interrogation.</span><span class="sxs-lookup"><span data-stu-id="6718e-376">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="6718e-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="6718e-377">subscriptionId</span></span> |<span data-ttu-id="6718e-378">ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6718e-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6718e-379">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6718e-379">Next steps</span></span>
* [<span data-ttu-id="6718e-380">En savoir plus sur le journal d’activité (autrefois appelé journal d’audit)</span><span class="sxs-lookup"><span data-stu-id="6718e-380">Learn more about the Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="6718e-381">Stream the Azure Activity Log to Event Hubs (Diffuser en continu le journal d’activités Azure vers Event Hubs)</span><span class="sxs-lookup"><span data-stu-id="6718e-381">Stream the Azure Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
