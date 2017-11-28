---
title: "Schéma d’abonnement à Azure Event Grid"
description: "Décrit les propriétés d’abonnement à un événement avec Azure Event Grid."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: eff2352066a76010d6d882a7b7e1961870cd2d46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="316e9-103">Schéma d’abonnement à Event Grid</span><span class="sxs-lookup"><span data-stu-id="316e9-103">Event Grid subscription schema</span></span>

<span data-ttu-id="316e9-104">Pour créer un abonnement Event Grid, envoyez une requête à l’opération Créer un abonnement aux événements.</span><span class="sxs-lookup"><span data-stu-id="316e9-104">To create an Event Grid subscription, you send a request to the Create Event subscription operation.</span></span> <span data-ttu-id="316e9-105">Utilisez le format suivant :</span><span class="sxs-lookup"><span data-stu-id="316e9-105">Use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="316e9-106">Par exemple, pour créer un abonnement aux événements pour un compte de stockage nommé `examplestorage` dans un groupe de ressources nommé `examplegroup`, utilisez le format suivant :</span><span class="sxs-lookup"><span data-stu-id="316e9-106">For example, to create an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="316e9-107">L’article décrit les propriétés et le schéma pour le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="316e9-107">The article describes the properties and schema for the body of the request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="316e9-108">Propriétés de l’abonnement aux événements</span><span class="sxs-lookup"><span data-stu-id="316e9-108">Event subscription properties</span></span>

| <span data-ttu-id="316e9-109">Propriété</span><span class="sxs-lookup"><span data-stu-id="316e9-109">Property</span></span> | <span data-ttu-id="316e9-110">Type</span><span class="sxs-lookup"><span data-stu-id="316e9-110">Type</span></span> | <span data-ttu-id="316e9-111">Description</span><span class="sxs-lookup"><span data-stu-id="316e9-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="316e9-112">destination</span><span class="sxs-lookup"><span data-stu-id="316e9-112">destination</span></span> | <span data-ttu-id="316e9-113">objet</span><span class="sxs-lookup"><span data-stu-id="316e9-113">object</span></span> | <span data-ttu-id="316e9-114">Objet qui définit le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="316e9-114">The object that defines the endpoint.</span></span> |
| <span data-ttu-id="316e9-115">filter</span><span class="sxs-lookup"><span data-stu-id="316e9-115">filter</span></span> | <span data-ttu-id="316e9-116">objet</span><span class="sxs-lookup"><span data-stu-id="316e9-116">object</span></span> | <span data-ttu-id="316e9-117">Champ facultatif pour filtrer les types d’événements.</span><span class="sxs-lookup"><span data-stu-id="316e9-117">An optional field for filtering the types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="316e9-118">objet de destination</span><span class="sxs-lookup"><span data-stu-id="316e9-118">destination object</span></span>

| <span data-ttu-id="316e9-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="316e9-119">Property</span></span> | <span data-ttu-id="316e9-120">Type</span><span class="sxs-lookup"><span data-stu-id="316e9-120">Type</span></span> | <span data-ttu-id="316e9-121">Description</span><span class="sxs-lookup"><span data-stu-id="316e9-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="316e9-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="316e9-122">endpointType</span></span> | <span data-ttu-id="316e9-123">string</span><span class="sxs-lookup"><span data-stu-id="316e9-123">string</span></span> | <span data-ttu-id="316e9-124">Type de point de terminaison pour l’abonnement (webhook/HTTP, concentrateur d’événements ou file d’attente).</span><span class="sxs-lookup"><span data-stu-id="316e9-124">The type of endpoint for the subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="316e9-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="316e9-125">endpointUrl</span></span> | <span data-ttu-id="316e9-126">string</span><span class="sxs-lookup"><span data-stu-id="316e9-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="316e9-127">objet de filtre</span><span class="sxs-lookup"><span data-stu-id="316e9-127">filter object</span></span>

| <span data-ttu-id="316e9-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="316e9-128">Property</span></span> | <span data-ttu-id="316e9-129">Type</span><span class="sxs-lookup"><span data-stu-id="316e9-129">Type</span></span> | <span data-ttu-id="316e9-130">Description</span><span class="sxs-lookup"><span data-stu-id="316e9-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="316e9-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="316e9-131">includedEventTypes</span></span> | <span data-ttu-id="316e9-132">array</span><span class="sxs-lookup"><span data-stu-id="316e9-132">array</span></span> | <span data-ttu-id="316e9-133">Affiche une correspondance lorsque le type d’événement du message d’événement correspond exactement à l’un de ces noms de type d’événement.</span><span class="sxs-lookup"><span data-stu-id="316e9-133">Match when the event type in the event message is an exact match to one of these event type names.</span></span> <span data-ttu-id="316e9-134">Génère une erreur lorsque le nom de l’événement ne correspond pas aux noms de type d’événement inscrits pour la source d’événements.</span><span class="sxs-lookup"><span data-stu-id="316e9-134">Raises an error when event name does not match the registered event type names for the event source.</span></span> <span data-ttu-id="316e9-135">Génère une correspondance pour tous les types d’événements.</span><span class="sxs-lookup"><span data-stu-id="316e9-135">Default matches all event types.</span></span> |
| <span data-ttu-id="316e9-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="316e9-136">subjectBeginsWith</span></span> | <span data-ttu-id="316e9-137">string</span><span class="sxs-lookup"><span data-stu-id="316e9-137">string</span></span> | <span data-ttu-id="316e9-138">Filtre de correspondance de préfixe appliqué au champ objet du message de l’événement.</span><span class="sxs-lookup"><span data-stu-id="316e9-138">A prefix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="316e9-139">La chaîne vide ou par défaut représente une correspondance générale.</span><span class="sxs-lookup"><span data-stu-id="316e9-139">The default or empty string matches all.</span></span> | 
| <span data-ttu-id="316e9-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="316e9-140">subjectEndsWith</span></span> | <span data-ttu-id="316e9-141">string</span><span class="sxs-lookup"><span data-stu-id="316e9-141">string</span></span> | <span data-ttu-id="316e9-142">Filtre de correspondance de suffixe appliqué au champ objet du message de l’événement.</span><span class="sxs-lookup"><span data-stu-id="316e9-142">A suffix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="316e9-143">La chaîne vide ou par défaut représente une correspondance générale.</span><span class="sxs-lookup"><span data-stu-id="316e9-143">The default or empty string matches all.</span></span> |
| <span data-ttu-id="316e9-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="316e9-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="316e9-145">string</span><span class="sxs-lookup"><span data-stu-id="316e9-145">string</span></span> | <span data-ttu-id="316e9-146">Contrôle la correspondance sensible à la casse pour les filtres.</span><span class="sxs-lookup"><span data-stu-id="316e9-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="316e9-147">Exemple de schéma d’abonnement</span><span class="sxs-lookup"><span data-stu-id="316e9-147">Example subscription schema</span></span>

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="316e9-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="316e9-148">Next steps</span></span>

* <span data-ttu-id="316e9-149">Pour une présentation d’Event Grid, consultez l’article [What is Event Grid?](overview.md) (Présentation d’Event Grid).</span><span class="sxs-lookup"><span data-stu-id="316e9-149">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>