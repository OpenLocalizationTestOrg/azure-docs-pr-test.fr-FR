---
title: "aaaAzure schéma événements des journaux d’activité | Documents Microsoft"
description: "Comprendre le schéma d’événement hello pour les données émises dans le journal d’activité de hello"
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
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="cc09c-103">Schéma d’événements du journal d’activité</span><span class="sxs-lookup"><span data-stu-id="cc09c-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="cc09c-104">Hello **journal des activités Azure** est un journal qui fournit un aperçu de tous les événements de niveau d’abonnement qui se sont produites dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cc09c-104">hello **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="cc09c-105">Cet article décrit le schéma d’événement hello par catégorie de données.</span><span class="sxs-lookup"><span data-stu-id="cc09c-105">This article describes hello event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="cc09c-106">Administratif</span><span class="sxs-lookup"><span data-stu-id="cc09c-106">Administrative</span></span>
<span data-ttu-id="cc09c-107">Cette catégorie contient les enregistrement hello de tous les créer, les opérations de mise à jour, de suppression et d’action effectuée par le biais du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="cc09c-107">This category contains hello record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="cc09c-108">Exemples de hello les types d’événements que vous verriez dans cette catégorie incluent « créer la machine virtuelle » et « supprimer un groupe de sécurité réseau « chaque action effectuée par un utilisateur ou l’application à l’aide du Gestionnaire de ressources est modelée comme une opération sur un type particulier.</span><span class="sxs-lookup"><span data-stu-id="cc09c-108">Examples of hello types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="cc09c-109">Si le type d’opération hello est écrire, supprimer, ou Action, enregistrements hello de début de hello et réussite ou Échec de cette opération sont enregistrées dans la catégorie Administrative de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-109">If hello operation type is Write, Delete, or Action, hello records of both hello start and success or fail of that operation are recorded in hello Administrative category.</span></span> <span data-ttu-id="cc09c-110">catégorie Administrative de Hello inclut également toutes les modifications de contrôle d’accès toorole dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="cc09c-110">hello Administrative category also includes any changes toorole-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="cc09c-111">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="cc09c-111">Sample event</span></span>
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

### <a name="property-descriptions"></a><span data-ttu-id="cc09c-112">Description des propriétés</span><span class="sxs-lookup"><span data-stu-id="cc09c-112">Property descriptions</span></span>
| <span data-ttu-id="cc09c-113">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="cc09c-113">Element Name</span></span> | <span data-ttu-id="cc09c-114">Description</span><span class="sxs-lookup"><span data-stu-id="cc09c-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc09c-115">autorisation</span><span class="sxs-lookup"><span data-stu-id="cc09c-115">authorization</span></span> |<span data-ttu-id="cc09c-116">Objet BLOB de propriétés RBAC de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-116">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="cc09c-117">Inclut généralement les propriétés « action », « rôle » et « portée » hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-117">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="cc09c-118">caller</span><span class="sxs-lookup"><span data-stu-id="cc09c-118">caller</span></span> |<span data-ttu-id="cc09c-119">Adresse de messagerie de l’utilisateur de hello qui a effectué les opération hello, revendication UPN ou revendication SPN basée sur la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="cc09c-119">Email address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="cc09c-120">channels</span><span class="sxs-lookup"><span data-stu-id="cc09c-120">channels</span></span> |<span data-ttu-id="cc09c-121">Une des valeurs suivantes de hello : « Admin », « Opération »</span><span class="sxs-lookup"><span data-stu-id="cc09c-121">One of hello following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="cc09c-122">réclamations</span><span class="sxs-lookup"><span data-stu-id="cc09c-122">claims</span></span> |<span data-ttu-id="cc09c-123">un jeton JWT Hello utilisés par Active Directory tooauthenticate hello utilisateur ou l’application tooperform cette opération dans le Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="cc09c-123">hello JWT token used by Active Directory tooauthenticate hello user or application tooperform this operation in resource manager.</span></span> |
| <span data-ttu-id="cc09c-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="cc09c-124">correlationId</span></span> |<span data-ttu-id="cc09c-125">Généralement, un GUID au format de chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-125">Usually a GUID in hello string format.</span></span> <span data-ttu-id="cc09c-126">Les événements qui partagent un ID de corrélation appartiennent toohello même action uber.</span><span class="sxs-lookup"><span data-stu-id="cc09c-126">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="cc09c-127">description</span><span class="sxs-lookup"><span data-stu-id="cc09c-127">description</span></span> |<span data-ttu-id="cc09c-128">Description textuelle statique d’un événement.</span><span class="sxs-lookup"><span data-stu-id="cc09c-128">Static text description of an event.</span></span> |
| <span data-ttu-id="cc09c-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="cc09c-129">eventDataId</span></span> |<span data-ttu-id="cc09c-130">Identificateur unique d’un événement.</span><span class="sxs-lookup"><span data-stu-id="cc09c-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="cc09c-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="cc09c-131">httpRequest</span></span> |<span data-ttu-id="cc09c-132">BLOB hello décrivant requête Http.</span><span class="sxs-lookup"><span data-stu-id="cc09c-132">Blob describing hello Http Request.</span></span> <span data-ttu-id="cc09c-133">Inclut généralement hello « clientRequestId », « clientIpAddress » et « method » (méthode HTTP.</span><span class="sxs-lookup"><span data-stu-id="cc09c-133">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="cc09c-134">Par exemple, PUT).</span><span class="sxs-lookup"><span data-stu-id="cc09c-134">For example, PUT).</span></span> |
| <span data-ttu-id="cc09c-135">level</span><span class="sxs-lookup"><span data-stu-id="cc09c-135">level</span></span> |<span data-ttu-id="cc09c-136">Niveau d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-136">Level of hello event.</span></span> <span data-ttu-id="cc09c-137">Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires »</span><span class="sxs-lookup"><span data-stu-id="cc09c-137">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="cc09c-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="cc09c-138">resourceGroupName</span></span> |<span data-ttu-id="cc09c-139">Nom du groupe de ressources hello pour hello incidence sur la ressource.</span><span class="sxs-lookup"><span data-stu-id="cc09c-139">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="cc09c-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="cc09c-140">resourceProviderName</span></span> |<span data-ttu-id="cc09c-141">Nom du fournisseur de ressources hello pour hello affectées les ressources</span><span class="sxs-lookup"><span data-stu-id="cc09c-141">Name of hello resource provider for hello impacted resource</span></span> |
| <span data-ttu-id="cc09c-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="cc09c-142">resourceId</span></span> |<span data-ttu-id="cc09c-143">Id de ressource de hello affectées les ressources.</span><span class="sxs-lookup"><span data-stu-id="cc09c-143">Resource id of hello impacted resource.</span></span> |
| <span data-ttu-id="cc09c-144">operationId</span><span class="sxs-lookup"><span data-stu-id="cc09c-144">operationId</span></span> |<span data-ttu-id="cc09c-145">Un GUID est partagé entre les événements hello qui correspondent tooa une seule opération.</span><span class="sxs-lookup"><span data-stu-id="cc09c-145">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="cc09c-146">operationName</span><span class="sxs-lookup"><span data-stu-id="cc09c-146">operationName</span></span> |<span data-ttu-id="cc09c-147">Nom de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-147">Name of hello operation.</span></span> |
| <span data-ttu-id="cc09c-148">properties</span><span class="sxs-lookup"><span data-stu-id="cc09c-148">properties</span></span> |<span data-ttu-id="cc09c-149">Jeu de `<Key, Value>` paires (autrement dit, un dictionnaire) hello décrivant les événements hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="cc09c-150">status</span><span class="sxs-lookup"><span data-stu-id="cc09c-150">status</span></span> |<span data-ttu-id="cc09c-151">Chaîne décrivant l’état hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-151">String describing hello status of hello operation.</span></span> <span data-ttu-id="cc09c-152">Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="cc09c-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="cc09c-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="cc09c-153">subStatus</span></span> |<span data-ttu-id="cc09c-154">Généralement hello le code d’état HTTP de hello correspondant appel REST, mais peut également inclure d’autres chaînes décrivant un sous-état, telles que ces valeurs courantes : OK (Code d’état HTTP : 200), créé (Code d’état HTTP : 201), accepté (Code d’état HTTP : 202), aucun contenu (HTTP Code d’état : 204), demande incorrecte (Code d’état HTTP : 400), il est introuvable (Code d’état HTTP : 404), conflit (Code d’état HTTP : 409), erreur interne au serveur (Code d’état HTTP : 500), Service indisponible (Code d’état HTTP : 503), délai d’attente de la passerelle (Code d’état HTTP : 504).</span><span class="sxs-lookup"><span data-stu-id="cc09c-154">Usually hello HTTP status code of hello corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="cc09c-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="cc09c-155">eventTimestamp</span></span> |<span data-ttu-id="cc09c-156">Horodatage lors de l’événement de hello a été généré par hello du traitement du service Azure hello demande événement hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="cc09c-156">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="cc09c-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="cc09c-157">submissionTimestamp</span></span> |<span data-ttu-id="cc09c-158">Horodatage lors de l’événement de hello sont devenues disponible pour l’interrogation.</span><span class="sxs-lookup"><span data-stu-id="cc09c-158">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="cc09c-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="cc09c-159">subscriptionId</span></span> |<span data-ttu-id="cc09c-160">ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="cc09c-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="cc09c-161">État d’intégrité du service</span><span class="sxs-lookup"><span data-stu-id="cc09c-161">Service health</span></span>
<span data-ttu-id="cc09c-162">Cette catégorie contient un enregistrement hello n’importe quel contrôle d’intégrité des incidents de services qui se sont produites dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cc09c-162">This category contains hello record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="cc09c-163">Un exemple de type hello d’événement que vous verriez dans cette catégorie est « SQL Azure dans l’est des États-Unis rencontre des temps d’arrêt. »</span><span class="sxs-lookup"><span data-stu-id="cc09c-163">An example of hello type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="cc09c-164">Événements de contrôle d’intégrité de service existe cinq types : Action requise, récupération d’assistance, Incident, Maintenance, informations ou la sécurité et n’apparaissent que si vous avez une ressource dans l’abonnement hello qui est affecté par l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in hello subscription that would be impacted by hello event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="cc09c-165">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="cc09c-165">Sample event</span></span>
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
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="cc09c-166">Description des propriétés</span><span class="sxs-lookup"><span data-stu-id="cc09c-166">Property descriptions</span></span>
<span data-ttu-id="cc09c-167">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="cc09c-167">Element Name</span></span> | <span data-ttu-id="cc09c-168">Description</span><span class="sxs-lookup"><span data-stu-id="cc09c-168">Description</span></span>
-------- | -----------
<span data-ttu-id="cc09c-169">channels</span><span class="sxs-lookup"><span data-stu-id="cc09c-169">channels</span></span> | <span data-ttu-id="cc09c-170">Est une des valeurs suivantes de hello : « Admin », « Opération »</span><span class="sxs-lookup"><span data-stu-id="cc09c-170">Is one of hello following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="cc09c-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="cc09c-171">correlationId</span></span> | <span data-ttu-id="cc09c-172">Est généralement un GUID au format de chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-172">Is usually a GUID in hello string format.</span></span> <span data-ttu-id="cc09c-173">Événements appartenant toohello même action uber partagent généralement hello même correlationId.</span><span class="sxs-lookup"><span data-stu-id="cc09c-173">Events with that belong toohello same uber action usually share hello same correlationId.</span></span>
<span data-ttu-id="cc09c-174">description</span><span class="sxs-lookup"><span data-stu-id="cc09c-174">description</span></span> | <span data-ttu-id="cc09c-175">Description de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-175">Description of hello event.</span></span>
<span data-ttu-id="cc09c-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="cc09c-176">eventDataId</span></span> | <span data-ttu-id="cc09c-177">Bonjour à l’identificateur unique d’un événement.</span><span class="sxs-lookup"><span data-stu-id="cc09c-177">hello unique identifier of an event.</span></span>
<span data-ttu-id="cc09c-178">eventName</span><span class="sxs-lookup"><span data-stu-id="cc09c-178">eventName</span></span> | <span data-ttu-id="cc09c-179">titre de Hello d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-179">hello title of hello event.</span></span>
<span data-ttu-id="cc09c-180">level</span><span class="sxs-lookup"><span data-stu-id="cc09c-180">level</span></span> | <span data-ttu-id="cc09c-181">Niveau d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-181">Level of hello event.</span></span> <span data-ttu-id="cc09c-182">Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires »</span><span class="sxs-lookup"><span data-stu-id="cc09c-182">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="cc09c-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="cc09c-183">resourceProviderName</span></span> | <span data-ttu-id="cc09c-184">Nom du fournisseur de ressources hello pour hello incidence sur la ressource.</span><span class="sxs-lookup"><span data-stu-id="cc09c-184">Name of hello resource provider for hello impacted resource.</span></span> <span data-ttu-id="cc09c-185">S’il est inconnu, cette option sera nulle.</span><span class="sxs-lookup"><span data-stu-id="cc09c-185">If not known, this will be null.</span></span>
<span data-ttu-id="cc09c-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="cc09c-186">resourceType</span></span>| <span data-ttu-id="cc09c-187">type Hello de ressource de hello affectées les ressources.</span><span class="sxs-lookup"><span data-stu-id="cc09c-187">hello type of resource of hello impacted resource.</span></span> <span data-ttu-id="cc09c-188">S’il est inconnu, cette option sera nulle.</span><span class="sxs-lookup"><span data-stu-id="cc09c-188">If not known, this will be null.</span></span>
<span data-ttu-id="cc09c-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="cc09c-189">subStatus</span></span> | <span data-ttu-id="cc09c-190">Généralement nul pour les événements de l’état d’intégrité du service.</span><span class="sxs-lookup"><span data-stu-id="cc09c-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="cc09c-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="cc09c-191">eventTimestamp</span></span> | <span data-ttu-id="cc09c-192">Horodatage lors de l’événement du journal hello a été générée et envoyée toohello journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="cc09c-192">Timestamp when hello log event was generated and submitted toohello Activity Log.</span></span>
<span data-ttu-id="cc09c-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="cc09c-193">submissionTimestamp</span></span> |   <span data-ttu-id="cc09c-194">Horodatage lors de l’événement de hello est devenu disponible dans le journal d’activité de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-194">Timestamp when hello event became available in hello Activity Log.</span></span>
<span data-ttu-id="cc09c-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="cc09c-195">subscriptionId</span></span> | <span data-ttu-id="cc09c-196">Bonjour abonnement Azure dans laquelle cet événement a été enregistré.</span><span class="sxs-lookup"><span data-stu-id="cc09c-196">hello Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="cc09c-197">status</span><span class="sxs-lookup"><span data-stu-id="cc09c-197">status</span></span> | <span data-ttu-id="cc09c-198">Chaîne décrivant l’état hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-198">String describing hello status of hello operation.</span></span> <span data-ttu-id="cc09c-199">Certaines valeurs courantes sont : actif, résolu.</span><span class="sxs-lookup"><span data-stu-id="cc09c-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="cc09c-200">operationName</span><span class="sxs-lookup"><span data-stu-id="cc09c-200">operationName</span></span> | <span data-ttu-id="cc09c-201">Nom de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-201">Name of hello operation.</span></span> <span data-ttu-id="cc09c-202">Généralement Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="cc09c-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="cc09c-203">category</span><span class="sxs-lookup"><span data-stu-id="cc09c-203">category</span></span> | <span data-ttu-id="cc09c-204">« ServiceHealth »</span><span class="sxs-lookup"><span data-stu-id="cc09c-204">"ServiceHealth"</span></span>
<span data-ttu-id="cc09c-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="cc09c-205">resourceId</span></span> | <span data-ttu-id="cc09c-206">Id de ressource de hello une incidence sur la ressource, s’il est connu.</span><span class="sxs-lookup"><span data-stu-id="cc09c-206">Resource id of hello impacted resource, if known.</span></span> <span data-ttu-id="cc09c-207">L’ID d’abonnement est fourni dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="cc09c-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="cc09c-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="cc09c-208">Properties.title</span></span> | <span data-ttu-id="cc09c-209">Hello titre localisé pour cette communication.</span><span class="sxs-lookup"><span data-stu-id="cc09c-209">hello localized title for this communication.</span></span> <span data-ttu-id="cc09c-210">L’anglais est la langue par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-210">English is hello default language.</span></span>
<span data-ttu-id="cc09c-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="cc09c-211">Properties.communication</span></span> | <span data-ttu-id="cc09c-212">Hello localisées des détails de communication hello par un balisage HTML.</span><span class="sxs-lookup"><span data-stu-id="cc09c-212">hello localized details of hello communication with HTML markup.</span></span> <span data-ttu-id="cc09c-213">L’anglais est la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-213">English is hello default.</span></span>
<span data-ttu-id="cc09c-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="cc09c-214">Properties.incidentType</span></span> | <span data-ttu-id="cc09c-215">valeurs possibles : AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span><span class="sxs-lookup"><span data-stu-id="cc09c-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="cc09c-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="cc09c-216">Properties.trackingId</span></span> | <span data-ttu-id="cc09c-217">Identifie l’incident hello que cet événement est associé.</span><span class="sxs-lookup"><span data-stu-id="cc09c-217">Identifies hello incident this event is associated with.</span></span> <span data-ttu-id="cc09c-218">Utilisez cet incident de toocorrelate hello événements tooan connexes.</span><span class="sxs-lookup"><span data-stu-id="cc09c-218">Use this toocorrelate hello events related tooan incident.</span></span>
<span data-ttu-id="cc09c-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="cc09c-219">Properties.impactedServices</span></span> | <span data-ttu-id="cc09c-220">Un séquence d’échappement blob JSON qui décrit les services hello et les régions qui sont affectées par l’incident de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-220">An escaped JSON blob which describes hello services and regions that are impacted by hello incident.</span></span> <span data-ttu-id="cc09c-221">Une liste de services, chacun possédant un ServiceName et une liste d’ImpactedRegions, chacune ayant un RegionName.</span><span class="sxs-lookup"><span data-stu-id="cc09c-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="cc09c-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="cc09c-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="cc09c-223">communication Hello en anglais</span><span class="sxs-lookup"><span data-stu-id="cc09c-223">hello communication in English</span></span>
<span data-ttu-id="cc09c-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="cc09c-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="cc09c-225">communication Hello en anglais en tant que balisage html ou texte brut</span><span class="sxs-lookup"><span data-stu-id="cc09c-225">hello communication in English as either html markup or plain text</span></span>
<span data-ttu-id="cc09c-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="cc09c-226">Properties.stage</span></span> | <span data-ttu-id="cc09c-227">Les valeurs possibles pour AssistedRecovery, ActionRequired, Information, Incident et Security sont Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="cc09c-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="cc09c-228">Pour Maintenance, les valeurs possibles sont Active, Planned, InProgress, Canceled, Rescheduled, Resolved et Complete</span><span class="sxs-lookup"><span data-stu-id="cc09c-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="cc09c-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="cc09c-229">Properties.communicationId</span></span> | <span data-ttu-id="cc09c-230">communication de Hello cet événement est associé.</span><span class="sxs-lookup"><span data-stu-id="cc09c-230">hello communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="cc09c-231">Alerte</span><span class="sxs-lookup"><span data-stu-id="cc09c-231">Alert</span></span>
<span data-ttu-id="cc09c-232">Cette catégorie contient un enregistrement hello de toutes les activations d’alertes Azure.</span><span class="sxs-lookup"><span data-stu-id="cc09c-232">This category contains hello record of all activations of Azure alerts.</span></span> <span data-ttu-id="cc09c-233">Un exemple de type hello d’événement que vous verriez dans cette catégorie est « % du processeur sur myVM a été plus de 80 pour hello 5 dernières minutes. »</span><span class="sxs-lookup"><span data-stu-id="cc09c-233">An example of hello type of event you would see in this category is "CPU % on myVM has been over 80 for hello past 5 minutes."</span></span> <span data-ttu-id="cc09c-234">Une variété de systèmes Azure possèdent un concept d’alertes : vous pouvez définir une règle quelconque et recevoir une notification lorsque les conditions correspondent à cette règle.</span><span class="sxs-lookup"><span data-stu-id="cc09c-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="cc09c-235">Chaque fois qu’un type d’alerte Azure pris en charge 'active,' ou hello conditions sont rempli toogenerate une notification, un enregistrement de l’activation de hello est envoyé également catégorie toothis Hello journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="cc09c-235">Each time a supported Azure alert type 'activates,' or hello conditions are met toogenerate a notification, a record of hello activation is also pushed toothis category of hello Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="cc09c-236">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="cc09c-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
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

### <a name="property-descriptions"></a><span data-ttu-id="cc09c-237">Description des propriétés</span><span class="sxs-lookup"><span data-stu-id="cc09c-237">Property descriptions</span></span>
| <span data-ttu-id="cc09c-238">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="cc09c-238">Element Name</span></span> | <span data-ttu-id="cc09c-239">Description</span><span class="sxs-lookup"><span data-stu-id="cc09c-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc09c-240">caller</span><span class="sxs-lookup"><span data-stu-id="cc09c-240">caller</span></span> | <span data-ttu-id="cc09c-241">Toujours Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="cc09c-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="cc09c-242">channels</span><span class="sxs-lookup"><span data-stu-id="cc09c-242">channels</span></span> | <span data-ttu-id="cc09c-243">Toujours « Admin, opération »</span><span class="sxs-lookup"><span data-stu-id="cc09c-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="cc09c-244">réclamations</span><span class="sxs-lookup"><span data-stu-id="cc09c-244">claims</span></span> | <span data-ttu-id="cc09c-245">Objet blob de JSON avec hello SPN (nom principal de service), ou une ressource de type, de moteur d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-245">JSON blob with hello SPN (service principal name), or resource type, of hello alert engine.</span></span> |
| <span data-ttu-id="cc09c-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="cc09c-246">correlationId</span></span> | <span data-ttu-id="cc09c-247">Un GUID au format de chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-247">A GUID in hello string format.</span></span> |
| <span data-ttu-id="cc09c-248">description</span><span class="sxs-lookup"><span data-stu-id="cc09c-248">description</span></span> |<span data-ttu-id="cc09c-249">Description de texte statique de l’événement d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-249">Static text description of hello alert event.</span></span> |
| <span data-ttu-id="cc09c-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="cc09c-250">eventDataId</span></span> |<span data-ttu-id="cc09c-251">Identificateur unique de l’événement d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-251">Unique identifier of hello alert event.</span></span> |
| <span data-ttu-id="cc09c-252">level</span><span class="sxs-lookup"><span data-stu-id="cc09c-252">level</span></span> |<span data-ttu-id="cc09c-253">Niveau d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-253">Level of hello event.</span></span> <span data-ttu-id="cc09c-254">Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires »</span><span class="sxs-lookup"><span data-stu-id="cc09c-254">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="cc09c-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="cc09c-255">resourceGroupName</span></span> |<span data-ttu-id="cc09c-256">Nom du groupe de ressources hello pour hello affectée ressource s’il s’agit d’une alerte de métrique.</span><span class="sxs-lookup"><span data-stu-id="cc09c-256">Name of hello resource group for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="cc09c-257">Pour les autres types d’alerte, il s’agit de nom de hello hello du groupe de ressources qui contient l’alerte hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="cc09c-257">For other alert types, this is hello name of hello resource group that contains hello alert itself.</span></span> |
| <span data-ttu-id="cc09c-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="cc09c-258">resourceProviderName</span></span> |<span data-ttu-id="cc09c-259">Nom du fournisseur de ressources hello pour hello affectée ressource s’il s’agit d’une alerte de métrique.</span><span class="sxs-lookup"><span data-stu-id="cc09c-259">Name of hello resource provider for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="cc09c-260">Pour les autres types d’alerte, il s’agit de nom de hello de fournisseur de ressources hello pour alerte hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="cc09c-260">For other alert types, this is hello name of hello resource provider for hello alert itself.</span></span> |
| <span data-ttu-id="cc09c-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="cc09c-261">resourceId</span></span> | <span data-ttu-id="cc09c-262">Nom de l’ID de ressource hello pour hello affectée ressource s’il s’agit d’une alerte de métrique.</span><span class="sxs-lookup"><span data-stu-id="cc09c-262">Name of hello resource ID for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="cc09c-263">Pour les autres types d’alerte, il s’agit de hello les ID de ressource de ressource d’alerte hello elle-même.</span><span class="sxs-lookup"><span data-stu-id="cc09c-263">For other alert types, this is hello resource ID of hello alert resource itself.</span></span> |
| <span data-ttu-id="cc09c-264">operationId</span><span class="sxs-lookup"><span data-stu-id="cc09c-264">operationId</span></span> |<span data-ttu-id="cc09c-265">Un GUID est partagé entre les événements hello qui correspondent tooa une seule opération.</span><span class="sxs-lookup"><span data-stu-id="cc09c-265">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="cc09c-266">operationName</span><span class="sxs-lookup"><span data-stu-id="cc09c-266">operationName</span></span> |<span data-ttu-id="cc09c-267">Nom de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-267">Name of hello operation.</span></span> |
| <span data-ttu-id="cc09c-268">properties</span><span class="sxs-lookup"><span data-stu-id="cc09c-268">properties</span></span> |<span data-ttu-id="cc09c-269">Jeu de `<Key, Value>` paires (autrement dit, un dictionnaire) hello décrivant les événements hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="cc09c-270">status</span><span class="sxs-lookup"><span data-stu-id="cc09c-270">status</span></span> |<span data-ttu-id="cc09c-271">Chaîne décrivant l’état hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-271">String describing hello status of hello operation.</span></span> <span data-ttu-id="cc09c-272">Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="cc09c-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="cc09c-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="cc09c-273">subStatus</span></span> | <span data-ttu-id="cc09c-274">Généralement, nul pour les alertes.</span><span class="sxs-lookup"><span data-stu-id="cc09c-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="cc09c-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="cc09c-275">eventTimestamp</span></span> |<span data-ttu-id="cc09c-276">Horodatage lors de l’événement de hello a été généré par hello du traitement du service Azure hello demande événement hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="cc09c-276">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="cc09c-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="cc09c-277">submissionTimestamp</span></span> |<span data-ttu-id="cc09c-278">Horodatage lors de l’événement de hello sont devenues disponible pour l’interrogation.</span><span class="sxs-lookup"><span data-stu-id="cc09c-278">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="cc09c-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="cc09c-279">subscriptionId</span></span> |<span data-ttu-id="cc09c-280">ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="cc09c-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="cc09c-281">Champ Propriétés par type d’alerte</span><span class="sxs-lookup"><span data-stu-id="cc09c-281">Properties field per alert type</span></span>
<span data-ttu-id="cc09c-282">champ de propriétés Hello contient des valeurs différentes en fonction de la source de hello d’événement d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-282">hello properties field will contain different values depending on hello source of hello alert event.</span></span> <span data-ttu-id="cc09c-283">Deux fournisseurs d’événements d’alertes courants sont les alertes du journal d’activité et les alertes métriques.</span><span class="sxs-lookup"><span data-stu-id="cc09c-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="cc09c-284">Propriétés pour les alertes du journal d’activité</span><span class="sxs-lookup"><span data-stu-id="cc09c-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="cc09c-285">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="cc09c-285">Element Name</span></span> | <span data-ttu-id="cc09c-286">Description</span><span class="sxs-lookup"><span data-stu-id="cc09c-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc09c-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="cc09c-287">properties.subscriptionId</span></span> | <span data-ttu-id="cc09c-288">ID d’abonnement Hello à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé.</span><span class="sxs-lookup"><span data-stu-id="cc09c-288">hello subscription ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="cc09c-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="cc09c-289">properties.eventDataId</span></span> | <span data-ttu-id="cc09c-290">Hello des ID de données d’événement à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé.</span><span class="sxs-lookup"><span data-stu-id="cc09c-290">hello event data ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="cc09c-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="cc09c-291">properties.resourceGroup</span></span> | <span data-ttu-id="cc09c-292">groupe de ressources Hello à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé.</span><span class="sxs-lookup"><span data-stu-id="cc09c-292">hello resource group from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="cc09c-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="cc09c-293">properties.resourceId</span></span> | <span data-ttu-id="cc09c-294">ID de ressource Hello à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé.</span><span class="sxs-lookup"><span data-stu-id="cc09c-294">hello resource ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="cc09c-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="cc09c-295">properties.eventTimestamp</span></span> | <span data-ttu-id="cc09c-296">Bonjour horodatage d’un événement de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé.</span><span class="sxs-lookup"><span data-stu-id="cc09c-296">hello event timestamp of hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="cc09c-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="cc09c-297">properties.operationName</span></span> | <span data-ttu-id="cc09c-298">nom de l’opération Hello à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé.</span><span class="sxs-lookup"><span data-stu-id="cc09c-298">hello operation name from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="cc09c-299">Properties.Status</span><span class="sxs-lookup"><span data-stu-id="cc09c-299">properties.status</span></span> | <span data-ttu-id="cc09c-300">état de Hello à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé.</span><span class="sxs-lookup"><span data-stu-id="cc09c-300">hello status from hello activity log event which caused this activity log alert rule toobe activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="cc09c-301">Propriétés des alertes métriques</span><span class="sxs-lookup"><span data-stu-id="cc09c-301">Properties for metric alerts</span></span>
| <span data-ttu-id="cc09c-302">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="cc09c-302">Element Name</span></span> | <span data-ttu-id="cc09c-303">Description</span><span class="sxs-lookup"><span data-stu-id="cc09c-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc09c-304">Propriétés. RuleUri</span><span class="sxs-lookup"><span data-stu-id="cc09c-304">properties.RuleUri</span></span> | <span data-ttu-id="cc09c-305">ID de ressource de hello métrique règle d’alerte lui-même.</span><span class="sxs-lookup"><span data-stu-id="cc09c-305">Resource ID of hello metric alert rule itself.</span></span> |
| <span data-ttu-id="cc09c-306">Propriétés. Nom_règle</span><span class="sxs-lookup"><span data-stu-id="cc09c-306">properties.RuleName</span></span> | <span data-ttu-id="cc09c-307">nom Hello de règle d’alerte métrique hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-307">hello name of hello metric alert rule.</span></span> |
| <span data-ttu-id="cc09c-308">Propriétés. RuleDescription</span><span class="sxs-lookup"><span data-stu-id="cc09c-308">properties.RuleDescription</span></span> | <span data-ttu-id="cc09c-309">description de Hello de règle d’alerte métrique hello (tel que défini dans la règle d’alerte hello).</span><span class="sxs-lookup"><span data-stu-id="cc09c-309">hello description of hello metric alert rule (as defined in hello alert rule).</span></span> |
| <span data-ttu-id="cc09c-310">Propriétés. Seuil</span><span class="sxs-lookup"><span data-stu-id="cc09c-310">properties.Threshold</span></span> | <span data-ttu-id="cc09c-311">valeur de seuil Hello utilisée dans l’évaluation de hello de règle d’alerte métrique hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-311">hello threshold value used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="cc09c-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="cc09c-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="cc09c-313">taille de la fenêtre Hello utilisée dans l’évaluation de hello de règle d’alerte métrique hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-313">hello window size used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="cc09c-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="cc09c-314">properties.Aggregation</span></span> | <span data-ttu-id="cc09c-315">type d’agrégation Hello défini dans la règle d’alerte métrique hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-315">hello aggregation type defined in hello metric alert rule.</span></span> |
| <span data-ttu-id="cc09c-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="cc09c-316">properties.Operator</span></span> | <span data-ttu-id="cc09c-317">opérateur conditionnel de Hello utilisée dans l’évaluation de hello de règle d’alerte métrique hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-317">hello conditional operator used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="cc09c-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="cc09c-318">properties.MetricName</span></span> | <span data-ttu-id="cc09c-319">nom de la métrique Hello de métrique hello utilisée dans l’évaluation de hello de règle d’alerte métrique hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-319">hello metric name of hello metric used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="cc09c-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="cc09c-320">properties.MetricUnit</span></span> | <span data-ttu-id="cc09c-321">unité de mesure Hello pour métrique hello utilisée dans l’évaluation de hello de règle d’alerte métrique hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-321">hello metric unit for hello metric used in hello evaluation of hello metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="cc09c-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="cc09c-322">Autoscale</span></span>
<span data-ttu-id="cc09c-323">Cette catégorie contient un enregistrement hello de toute opération toohello connexes d’événements du moteur de mise à l’échelle hello selon les paramètres d’échelle automatique que vous avez défini dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="cc09c-323">This category contains hello record of any events related toohello operation of hello autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="cc09c-324">Un exemple de type hello d’événement que vous verriez dans cette catégorie est « Mise à l’échelle mise à l’échelle de l’échec de l’action. »</span><span class="sxs-lookup"><span data-stu-id="cc09c-324">An example of hello type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="cc09c-325">À l’aide de la mise à l’échelle, vous pouvez automatiquement montée en puissance parallèle ou mettre à l’échelle dans hello nombre d’instances d’un type de ressource pris en charge basée sur l’heure du jour et/ou la charge des données (métriques) à l’aide d’un paramètre de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="cc09c-325">Using autoscale, you can automatically scale out or scale in hello number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="cc09c-326">En cas de hello conditions sont remplies tooscale vers le haut ou vers le bas, hello démarrer et a réussi, ou les événements ayant échouées seront enregistrés dans cette catégorie.</span><span class="sxs-lookup"><span data-stu-id="cc09c-326">When hello conditions are met tooscale up or down, hello start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="cc09c-327">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="cc09c-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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

### <a name="property-descriptions"></a><span data-ttu-id="cc09c-328">Description des propriétés</span><span class="sxs-lookup"><span data-stu-id="cc09c-328">Property descriptions</span></span>
| <span data-ttu-id="cc09c-329">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="cc09c-329">Element Name</span></span> | <span data-ttu-id="cc09c-330">Description</span><span class="sxs-lookup"><span data-stu-id="cc09c-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc09c-331">caller</span><span class="sxs-lookup"><span data-stu-id="cc09c-331">caller</span></span> | <span data-ttu-id="cc09c-332">Always Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="cc09c-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="cc09c-333">channels</span><span class="sxs-lookup"><span data-stu-id="cc09c-333">channels</span></span> | <span data-ttu-id="cc09c-334">Toujours « Admin, opération »</span><span class="sxs-lookup"><span data-stu-id="cc09c-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="cc09c-335">réclamations</span><span class="sxs-lookup"><span data-stu-id="cc09c-335">claims</span></span> | <span data-ttu-id="cc09c-336">Objet blob de JSON avec hello type SPN (nom principal de service) ou des ressources, du moteur de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-336">JSON blob with hello SPN (service principal name), or resource type, of hello autoscale engine.</span></span> |
| <span data-ttu-id="cc09c-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="cc09c-337">correlationId</span></span> | <span data-ttu-id="cc09c-338">Un GUID au format de chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-338">A GUID in hello string format.</span></span> |
| <span data-ttu-id="cc09c-339">description</span><span class="sxs-lookup"><span data-stu-id="cc09c-339">description</span></span> |<span data-ttu-id="cc09c-340">Description de texte statique d’événement de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-340">Static text description of hello autoscale event.</span></span> |
| <span data-ttu-id="cc09c-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="cc09c-341">eventDataId</span></span> |<span data-ttu-id="cc09c-342">Identificateur unique de l’événement de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-342">Unique identifier of hello autoscale event.</span></span> |
| <span data-ttu-id="cc09c-343">level</span><span class="sxs-lookup"><span data-stu-id="cc09c-343">level</span></span> |<span data-ttu-id="cc09c-344">Niveau d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-344">Level of hello event.</span></span> <span data-ttu-id="cc09c-345">Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires »</span><span class="sxs-lookup"><span data-stu-id="cc09c-345">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="cc09c-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="cc09c-346">resourceGroupName</span></span> |<span data-ttu-id="cc09c-347">Nom du groupe de ressources hello pour le paramètre de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-347">Name of hello resource group for hello autoscale setting.</span></span> |
| <span data-ttu-id="cc09c-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="cc09c-348">resourceProviderName</span></span> |<span data-ttu-id="cc09c-349">Nom du fournisseur de ressources hello pour le paramètre de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-349">Name of hello resource provider for hello autoscale setting.</span></span> |
| <span data-ttu-id="cc09c-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="cc09c-350">resourceId</span></span> |<span data-ttu-id="cc09c-351">Id de ressource du paramètre de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-351">Resource id of hello autoscale setting.</span></span> |
| <span data-ttu-id="cc09c-352">operationId</span><span class="sxs-lookup"><span data-stu-id="cc09c-352">operationId</span></span> |<span data-ttu-id="cc09c-353">Un GUID est partagé entre les événements hello qui correspondent tooa une seule opération.</span><span class="sxs-lookup"><span data-stu-id="cc09c-353">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="cc09c-354">operationName</span><span class="sxs-lookup"><span data-stu-id="cc09c-354">operationName</span></span> |<span data-ttu-id="cc09c-355">Nom de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-355">Name of hello operation.</span></span> |
| <span data-ttu-id="cc09c-356">properties</span><span class="sxs-lookup"><span data-stu-id="cc09c-356">properties</span></span> |<span data-ttu-id="cc09c-357">Jeu de `<Key, Value>` paires (autrement dit, un dictionnaire) hello décrivant les événements hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="cc09c-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="cc09c-358">properties.Description</span></span> | <span data-ttu-id="cc09c-359">Description détaillée des opérations en cours dans le moteur de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-359">Detailed description of what hello autoscale engine was doing.</span></span> |
| <span data-ttu-id="cc09c-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="cc09c-360">properties.ResourceName</span></span> | <span data-ttu-id="cc09c-361">ID de ressource de hello affectées les ressources (hello des ressources sur le hello à l’échelle a été effectuée.)</span><span class="sxs-lookup"><span data-stu-id="cc09c-361">Resource ID of hello impacted resource (hello resource on which hello scale action was being performed)</span></span> |
| <span data-ttu-id="cc09c-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="cc09c-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="cc09c-363">nombre de Hello d’instances avant l’action de mise à l’échelle hello a pris effet.</span><span class="sxs-lookup"><span data-stu-id="cc09c-363">hello number of instances before hello autoscale action took effect.</span></span> |
| <span data-ttu-id="cc09c-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="cc09c-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="cc09c-365">nombre de Hello d’instances une fois que l’action de mise à l’échelle hello a pris effet.</span><span class="sxs-lookup"><span data-stu-id="cc09c-365">hello number of instances after hello autoscale action took effect.</span></span> |
| <span data-ttu-id="cc09c-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="cc09c-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="cc09c-367">horodatage de Hello de lorsque l’action de mise à l’échelle hello s’est produite.</span><span class="sxs-lookup"><span data-stu-id="cc09c-367">hello timestamp of when hello autoscale action occurred.</span></span> |
| <span data-ttu-id="cc09c-368">status</span><span class="sxs-lookup"><span data-stu-id="cc09c-368">status</span></span> |<span data-ttu-id="cc09c-369">Chaîne décrivant l’état hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="cc09c-369">String describing hello status of hello operation.</span></span> <span data-ttu-id="cc09c-370">Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="cc09c-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="cc09c-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="cc09c-371">subStatus</span></span> | <span data-ttu-id="cc09c-372">Généralement, nul pour la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="cc09c-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="cc09c-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="cc09c-373">eventTimestamp</span></span> |<span data-ttu-id="cc09c-374">Horodatage lors de l’événement de hello a été généré par hello du traitement du service Azure hello demande événement hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="cc09c-374">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="cc09c-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="cc09c-375">submissionTimestamp</span></span> |<span data-ttu-id="cc09c-376">Horodatage lors de l’événement de hello sont devenues disponible pour l’interrogation.</span><span class="sxs-lookup"><span data-stu-id="cc09c-376">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="cc09c-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="cc09c-377">subscriptionId</span></span> |<span data-ttu-id="cc09c-378">ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="cc09c-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cc09c-379">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cc09c-379">Next steps</span></span>
* [<span data-ttu-id="cc09c-380">En savoir plus sur hello journal d’activité (anciennement les journaux d’Audit)</span><span class="sxs-lookup"><span data-stu-id="cc09c-380">Learn more about hello Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="cc09c-381">Flux tooEvent du journal des activités Azure hello concentrateurs</span><span class="sxs-lookup"><span data-stu-id="cc09c-381">Stream hello Azure Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
