---
title: "Sécurité et authentification Azure Event Grid"
description: "Détaille le service Azure Event Grid et ses concepts."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: b6e1c7587c0b47d04862b4850741aaa3b7d191a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="f83fa-103">Sécurité et authentification Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="f83fa-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="f83fa-104">Azure Event Grid dispose de trois types d’authentification :</span><span class="sxs-lookup"><span data-stu-id="f83fa-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="f83fa-105">Abonnements à des événements</span><span class="sxs-lookup"><span data-stu-id="f83fa-105">Event subscriptions</span></span>
* <span data-ttu-id="f83fa-106">Publication d’événement</span><span class="sxs-lookup"><span data-stu-id="f83fa-106">Event publishing</span></span>
* <span data-ttu-id="f83fa-107">Remise d’événement WebHook</span><span class="sxs-lookup"><span data-stu-id="f83fa-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="f83fa-108">Remise d’événement WebHook</span><span class="sxs-lookup"><span data-stu-id="f83fa-108">WebHook Event delivery</span></span>

<span data-ttu-id="f83fa-109">Webhook constitue l’un des nombreux moyens de réception d’événements en temps réel depuis Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="f83fa-109">Webhooks are one of many ways to receive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="f83fa-110">Chaque fois qu’un nouvel événement est prêt à être remis, Event Grid envoie une requête HTTP à votre WebHook en mentionnant l’événement dans le corps.</span><span class="sxs-lookup"><span data-stu-id="f83fa-110">Every time there is a new event ready to be delivered, Event Grid sends an HTTP request with to your WebHook with the event in the body.</span></span>

<span data-ttu-id="f83fa-111">Lorsque vous inscrivez votre point de terminaison WebHook avec Event Grid, le WebHook vous envoie une requête POST avec un code de validation simple pour prouver que vous êtes le propriétaire du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="f83fa-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order to prove endpoint ownership.</span></span> <span data-ttu-id="f83fa-112">Votre application doit répondre en renvoyant le code de validation.</span><span class="sxs-lookup"><span data-stu-id="f83fa-112">Your app needs to respond by echoing back the validation code.</span></span> <span data-ttu-id="f83fa-113">Event Grid ne remet aucun événement aux points de terminaison WebHook qui n’ont pas été validés.</span><span class="sxs-lookup"><span data-stu-id="f83fa-113">Event Grid will not deliver events to WebHook endpoints that have not passed the validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="f83fa-114">Détails de validation :</span><span class="sxs-lookup"><span data-stu-id="f83fa-114">Validation details:</span></span>

* <span data-ttu-id="f83fa-115">Lors de la création/mise à jour de l’abonnement d’événement, Event Grid publie un événement nommé « SubscriptionValidationEvent » dans le point de terminaison cible.</span><span class="sxs-lookup"><span data-stu-id="f83fa-115">At the time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event to the target endpoint.</span></span>
* <span data-ttu-id="f83fa-116">L’événement contient une valeur d’en-tête « Event-Type: Validation ».</span><span class="sxs-lookup"><span data-stu-id="f83fa-116">The event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="f83fa-117">Le corps de l’événement dispose du même schéma que les autres événements Event Grid.</span><span class="sxs-lookup"><span data-stu-id="f83fa-117">The event body has the same schema as other Event Grid events.</span></span>
* <span data-ttu-id="f83fa-118">Les données d’événement incluent une propriété « ValidationCode » avec une chaîne générée de façon aléatoire, par exemple « ValidationCode : acb13... ».</span><span class="sxs-lookup"><span data-stu-id="f83fa-118">The event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="f83fa-119">Afin de prouver que vous êtes propriétaire du point de terminaison, renvoyez le code de validation, par exemple : « ValidationResponse : acb13... ».</span><span class="sxs-lookup"><span data-stu-id="f83fa-119">In order to prove endpoint ownership, echo back the validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="f83fa-120">Enfin, il est important de noter qu’Azure Event Grid ne prend en charge que les points de terminaison HTTPS webhook.</span><span class="sxs-lookup"><span data-stu-id="f83fa-120">Finally, it is important to note that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="f83fa-121">Abonnement à un événement</span><span class="sxs-lookup"><span data-stu-id="f83fa-121">Event subscription</span></span>

<span data-ttu-id="f83fa-122">Pour vous abonner à un événement, vous devez disposer de l’autorisation **Microsoft.EventGrid/EventSubscriptions/Write** sur la ressource nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f83fa-122">To subscribe to an event, you must have the **Microsoft.EventGrid/EventSubscriptions/Write** permission on the required resource.</span></span> <span data-ttu-id="f83fa-123">Il vous faut cette autorisation, car vous rédigez un nouvel abonnement dans la portée de la ressource.</span><span class="sxs-lookup"><span data-stu-id="f83fa-123">You need this permission because you are writing a new subscription at the scope of the resource.</span></span> <span data-ttu-id="f83fa-124">La ressource nécessaire diffère si vous vous abonnez à une rubrique du système ou à une rubrique personnalisée.</span><span class="sxs-lookup"><span data-stu-id="f83fa-124">The required resource differs based on whether you are subscribing to a system topic or custom topic.</span></span> <span data-ttu-id="f83fa-125">Les deux types sont décrits dans cette section.</span><span class="sxs-lookup"><span data-stu-id="f83fa-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="f83fa-126">Rubriques du système (éditeurs du service Azure)</span><span class="sxs-lookup"><span data-stu-id="f83fa-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="f83fa-127">Dans les rubriques du système, il vous faut l’autorisation de rédiger un nouvel abonnement à un événement dans la portée de la ressource qui publie l’événement.</span><span class="sxs-lookup"><span data-stu-id="f83fa-127">For system topics, you need permission to write a new event subscription at the scope of the resource publishing the event.</span></span> <span data-ttu-id="f83fa-128">La ressource est au format suivant : `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="f83fa-128">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="f83fa-129">Par exemple, pour vous abonner à un événement sur un compte de stockage nommé **myacct**, il vous faut l’autorisation Microsoft.EventGrid/EventSubscriptions/Write sur :`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="f83fa-129">For example, to subscribe to an event on a storage account named **myacct**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="f83fa-130">Rubriques personnalisées</span><span class="sxs-lookup"><span data-stu-id="f83fa-130">Custom topics</span></span>

<span data-ttu-id="f83fa-131">Dans les rubriques personnalisées, il vous faut l’autorisation de rédiger un nouvel abonnement à un événement dans la portée de la rubrique Event Grid.</span><span class="sxs-lookup"><span data-stu-id="f83fa-131">For custom topics, you need permission to write a new event subscription at the scope of the Event Grid topic.</span></span> <span data-ttu-id="f83fa-132">La ressource est au format suivant : `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="f83fa-132">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="f83fa-133">Par exemple, pour vous abonner à une rubrique personnalisée nommée **mytopic**, il vous faut l’autorisation Microsoft.EventGrid/EventSubscriptions/Write sur :`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="f83fa-133">For example, to subscribe to a custom topic named **mytopic**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="f83fa-134">Publication d’une rubrique</span><span class="sxs-lookup"><span data-stu-id="f83fa-134">Topic publishing</span></span>

<span data-ttu-id="f83fa-135">Les rubriques utilisent une Signature d’accès partagé (SAP) ou une authentification par clé.</span><span class="sxs-lookup"><span data-stu-id="f83fa-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="f83fa-136">Nous vous recommandons la SAP, mais l’authentification par clé propose une programmation simple et est compatible avec de nombreux éditeurs de webhook existants.</span><span class="sxs-lookup"><span data-stu-id="f83fa-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="f83fa-137">Vous incluez la valeur d’authentification dans l’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="f83fa-137">You include the authentication value in the HTTP header.</span></span> <span data-ttu-id="f83fa-138">Pour une SAP, utilisez **aeg-sas-token** en valeur de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="f83fa-138">For SAS, use **aeg-sas-token** for the header value.</span></span> <span data-ttu-id="f83fa-139">Pour une authentification par clé, utilisez **aeg-sas-key** en valeur de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="f83fa-139">For key authentication, use **aeg-sas-key** for the header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="f83fa-140">Authentification par clé</span><span class="sxs-lookup"><span data-stu-id="f83fa-140">Key authentication</span></span>

<span data-ttu-id="f83fa-141">L’authentification par clé est la plus simple.</span><span class="sxs-lookup"><span data-stu-id="f83fa-141">Key authentication is the simplest form of authentication.</span></span> <span data-ttu-id="f83fa-142">Utilisez le format : `aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="f83fa-142">Use the format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="f83fa-143">Par exemple, vous transmettez une clé avec :</span><span class="sxs-lookup"><span data-stu-id="f83fa-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="f83fa-144">Jetons SAS</span><span class="sxs-lookup"><span data-stu-id="f83fa-144">SAS tokens</span></span>

<span data-ttu-id="f83fa-145">Les jetons SAP pour Event Grid incluent la ressource, un délai d’expiration et une signature.</span><span class="sxs-lookup"><span data-stu-id="f83fa-145">SAS tokens for Event Grid include the resource, an expiration time, and a signature.</span></span> <span data-ttu-id="f83fa-146">Le jeton SAP est au format suivant : `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="f83fa-146">The format of the SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="f83fa-147">La ressource représente le chemin d’accès à la rubrique à laquelle vous envoyez des événements.</span><span class="sxs-lookup"><span data-stu-id="f83fa-147">The resource is the path for the topic to which you are sending events.</span></span> <span data-ttu-id="f83fa-148">Par exemple, un chemin d’accès de ressource valide est :`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="f83fa-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="f83fa-149">Vous générez la signature à partir d’une clé.</span><span class="sxs-lookup"><span data-stu-id="f83fa-149">You generate the signature from a key.</span></span>

<span data-ttu-id="f83fa-150">Par exemple, une valeur **aeg-sas-token** valide est :</span><span class="sxs-lookup"><span data-stu-id="f83fa-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="f83fa-151">L’exemple suivant crée un jeton SAP utilisable avec Event Grid :</span><span class="sxs-lookup"><span data-stu-id="f83fa-151">The following example creates a SAS token for use with Event Grid:</span></span>

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a><span data-ttu-id="f83fa-152">Contrôle d’accès à la gestion</span><span class="sxs-lookup"><span data-stu-id="f83fa-152">Management Access Control</span></span>

<span data-ttu-id="f83fa-153">Azure Event Grid vous permet de contrôler le niveau d’accès offert aux utilisateurs, leur permettant d’effectuer différentes opérations de gestion telles que répertorier et créer des abonnements aux événements et générer des clés.</span><span class="sxs-lookup"><span data-stu-id="f83fa-153">Azure Event Grid allows you to control the level of access given to different users to do various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="f83fa-154">Pour cela, Event Grid utilise la vérification d’accès par rôle (RBAC).</span><span class="sxs-lookup"><span data-stu-id="f83fa-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="f83fa-155">Types d’opération</span><span class="sxs-lookup"><span data-stu-id="f83fa-155">Operation types</span></span>

<span data-ttu-id="f83fa-156">Azure Event Grid prend en charge les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="f83fa-156">Azure event grid supports the following actions:</span></span>

* <span data-ttu-id="f83fa-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="f83fa-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="f83fa-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="f83fa-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="f83fa-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="f83fa-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="f83fa-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="f83fa-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="f83fa-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="f83fa-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="f83fa-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="f83fa-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="f83fa-163">Les trois dernières opérations retournent des informations potentiellement confidentielles qui sont filtrées lors d’opérations de lecture normales.</span><span class="sxs-lookup"><span data-stu-id="f83fa-163">The last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="f83fa-164">Nous vous recommandons de restreindre l’accès à ces opérations.</span><span class="sxs-lookup"><span data-stu-id="f83fa-164">It is best practice for you to restrict access to these operations.</span></span> <span data-ttu-id="f83fa-165">Il est possible de créer des rôles personnalisés à l’aide [d’Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), de [l’interface CLI Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md) et de [l’API REST](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="f83fa-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and the [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="f83fa-166">Application de la vérification d’accès par rôle (RBAC)</span><span class="sxs-lookup"><span data-stu-id="f83fa-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="f83fa-167">Pour appliquer la vérification d’accès par rôle, pour différents utilisateurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f83fa-167">Use the following steps to enforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="f83fa-168">Créer un fichier de définition de rôle personnalisé (.json)</span><span class="sxs-lookup"><span data-stu-id="f83fa-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="f83fa-169">Voici des exemples de définitions de rôle dans Event Grid permettant aux utilisateurs d’effectuer différentes actions.</span><span class="sxs-lookup"><span data-stu-id="f83fa-169">The following are sample Event Grid role definitions which allow users to perform different sets of actions.</span></span>

<span data-ttu-id="f83fa-170">**EventGridReadOnlyRole.json** : pour autoriser uniquement les opérations en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="f83fa-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

<span data-ttu-id="f83fa-171">**EventGridNoDeleteListKeysRole.json** : pour autoriser des actions de publication limitées, et interdire les actions de suppression.</span><span class="sxs-lookup"><span data-stu-id="f83fa-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
<span data-ttu-id="f83fa-172">**EventGridContributorRole.json**: pour autoriser toutes les actions dans Event Grid.</span><span class="sxs-lookup"><span data-stu-id="f83fa-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-to-azure-cli"></a><span data-ttu-id="f83fa-173">Installer et se connecter à Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f83fa-173">Install and login to Azure CLI</span></span>

* <span data-ttu-id="f83fa-174">Azure CLI version 0.8.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f83fa-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="f83fa-175">Pour installer la dernière version et l’associer à votre abonnement Azure, consultez [Installer et configurer Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f83fa-175">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="f83fa-176">Azure Resource Manager dans l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="f83fa-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="f83fa-177">Pour plus d’informations, consultez [Utilisation de l’interface de ligne de commande Azure avec Azure Resource Manager](../xplat-cli-azure-resource-manager.md) .</span><span class="sxs-lookup"><span data-stu-id="f83fa-177">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="f83fa-178">Créer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="f83fa-178">Create a custom role</span></span>

<span data-ttu-id="f83fa-179">Pour créer un rôle personnalisé, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f83fa-179">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-the-role-to-a-user"></a><span data-ttu-id="f83fa-180">Affecter le rôle à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="f83fa-180">Assign the role to a user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="f83fa-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f83fa-181">Next steps</span></span>

* <span data-ttu-id="f83fa-182">Pour une présentation d’Event Grid, consultez [Event Grid](overview.md)</span><span class="sxs-lookup"><span data-stu-id="f83fa-182">For an introduction to Event Grid, see [About Event Grid](overview.md)</span></span>
