---
title: "authentification et sécurité de grille d’événement aaaAzure"
description: "Détaille Azure Event Grid et ses concepts."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="a55e6-103">Sécurité et authentification Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="a55e6-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="a55e6-104">Azure Event Grid dispose de trois types d’authentification :</span><span class="sxs-lookup"><span data-stu-id="a55e6-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="a55e6-105">Abonnements à des événements</span><span class="sxs-lookup"><span data-stu-id="a55e6-105">Event subscriptions</span></span>
* <span data-ttu-id="a55e6-106">Publication d’événement</span><span class="sxs-lookup"><span data-stu-id="a55e6-106">Event publishing</span></span>
* <span data-ttu-id="a55e6-107">Remise d’événement WebHook</span><span class="sxs-lookup"><span data-stu-id="a55e6-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="a55e6-108">Remise d’événement WebHook</span><span class="sxs-lookup"><span data-stu-id="a55e6-108">WebHook Event delivery</span></span>

<span data-ttu-id="a55e6-109">Webhooks sont un des nombreux événements tooreceive de manières en temps réel à partir de la grille d’événement Azure.</span><span class="sxs-lookup"><span data-stu-id="a55e6-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="a55e6-110">Chaque fois qu’il existe un nouveau toobe de prêt événement remis, grille d’événement envoie une requête HTTP avec tooyour WebHook avec les événements hello dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="a55e6-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="a55e6-111">Lorsque vous inscrivez votre propre point de terminaison WebHook avec grille d’événement, il vous envoie une requête POST avec un code de validation simple dans la propriété de commande tooprove point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="a55e6-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="a55e6-112">Votre application doit toorespond en affichant le code de validation hello précédent.</span><span class="sxs-lookup"><span data-stu-id="a55e6-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="a55e6-113">Grille d’événement renverra pas d’événements tooWebHook des points de terminaison qui n’ont pas réussi la validation hello.</span><span class="sxs-lookup"><span data-stu-id="a55e6-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="a55e6-114">Détails de validation :</span><span class="sxs-lookup"><span data-stu-id="a55e6-114">Validation details:</span></span>

* <span data-ttu-id="a55e6-115">Au moment de hello d’événement abonnement création/mise à jour, grille d’événement valide un point de terminaison cible de toohello événements « SubscriptionValidationEvent ».</span><span class="sxs-lookup"><span data-stu-id="a55e6-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="a55e6-116">événement de Hello contient une valeur d’en-tête « Validation de : Type d’événement ».</span><span class="sxs-lookup"><span data-stu-id="a55e6-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="a55e6-117">corps de l’événement Hello a hello même schéma que d’autres événements de la grille d’événement.</span><span class="sxs-lookup"><span data-stu-id="a55e6-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="a55e6-118">données d’événement Hello incluent une propriété « ValidationCode » avec une chaîne générée de façon aléatoire, par exemple « ValidationCode : acb13... ».</span><span class="sxs-lookup"><span data-stu-id="a55e6-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="a55e6-119">Dans la propriété de commande tooprove point de terminaison, par exemple, de code de validation hello arrière d’écho « ValidationResponse : acb13... ».</span><span class="sxs-lookup"><span data-stu-id="a55e6-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="a55e6-120">Enfin, il est important toonote que grille d’événement Azure prend en charge les points de terminaison HTTPS webhook.</span><span class="sxs-lookup"><span data-stu-id="a55e6-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="a55e6-121">Abonnement à un événement</span><span class="sxs-lookup"><span data-stu-id="a55e6-121">Event subscription</span></span>

<span data-ttu-id="a55e6-122">événement de tooan toosubscribe, vous devez disposer hello **Microsoft.EventGrid/EventSubscriptions/Write** ressource nécessite une autorisation sur hello.</span><span class="sxs-lookup"><span data-stu-id="a55e6-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="a55e6-123">Vous avez besoin de cette autorisation, car l’écriture d’un nouvel abonnement à la portée de hello de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="a55e6-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="a55e6-124">Hello requis ressources différent selon que vous vous abonnez tooa système rubrique ou personnalisé.</span><span class="sxs-lookup"><span data-stu-id="a55e6-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="a55e6-125">Les deux types sont décrits dans cette section.</span><span class="sxs-lookup"><span data-stu-id="a55e6-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="a55e6-126">Rubriques du système (éditeurs du service Azure)</span><span class="sxs-lookup"><span data-stu-id="a55e6-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="a55e6-127">Les rubriques du système, vous avez besoin d’autorisation toowrite un nouvel abonnement des événements au niveau de portée de hello d’événement de hello publication hello ressource.</span><span class="sxs-lookup"><span data-stu-id="a55e6-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="a55e6-128">format Hello de ressource de hello est :`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="a55e6-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="a55e6-129">Par exemple, les événements tooan toosubscribe sur un compte de stockage nommé **MONCOMPTE**, vous devez avoir l’autorisation de Microsoft.EventGrid/EventSubscriptions/Write de hello sur :`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="a55e6-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="a55e6-130">Rubriques personnalisées</span><span class="sxs-lookup"><span data-stu-id="a55e6-130">Custom topics</span></span>

<span data-ttu-id="a55e6-131">Les rubriques personnalisés, vous devez autorisation toowrite un nouvel abonnement des événements au niveau de portée de hello de rubrique de grille d’événement hello.</span><span class="sxs-lookup"><span data-stu-id="a55e6-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="a55e6-132">format Hello de ressource de hello est :`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="a55e6-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="a55e6-133">Par exemple, toosubscribe tooa rubrique personnalisée nommée **mytopic**, vous devez avoir l’autorisation de Microsoft.EventGrid/EventSubscriptions/Write de hello sur :`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="a55e6-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="a55e6-134">Publication d’une rubrique</span><span class="sxs-lookup"><span data-stu-id="a55e6-134">Topic publishing</span></span>

<span data-ttu-id="a55e6-135">Les rubriques utilisent une Signature d’accès partagé (SAP) ou une authentification par clé.</span><span class="sxs-lookup"><span data-stu-id="a55e6-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="a55e6-136">Nous vous recommandons la SAP, mais l’authentification par clé propose une programmation simple et est compatible avec de nombreux éditeurs de webhook existants.</span><span class="sxs-lookup"><span data-stu-id="a55e6-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="a55e6-137">Vous incluez la valeur d’authentification hello dans l’en-tête HTTP de hello.</span><span class="sxs-lookup"><span data-stu-id="a55e6-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="a55e6-138">Pour les associations de sécurité, utilisez **jeton de sas, AEG,** pour la valeur d’en-tête hello.</span><span class="sxs-lookup"><span data-stu-id="a55e6-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="a55e6-139">Pour l’authentification par clé, utilisez **clé de sas, AEG,** pour la valeur d’en-tête hello.</span><span class="sxs-lookup"><span data-stu-id="a55e6-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="a55e6-140">Authentification par clé</span><span class="sxs-lookup"><span data-stu-id="a55e6-140">Key authentication</span></span>

<span data-ttu-id="a55e6-141">Authentification de la clé est la forme la plus simple de hello d’authentification.</span><span class="sxs-lookup"><span data-stu-id="a55e6-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="a55e6-142">Utilisez le format hello :`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="a55e6-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="a55e6-143">Par exemple, vous transmettez une clé avec :</span><span class="sxs-lookup"><span data-stu-id="a55e6-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="a55e6-144">Jetons SAS</span><span class="sxs-lookup"><span data-stu-id="a55e6-144">SAS tokens</span></span>

<span data-ttu-id="a55e6-145">Jetons SAP pour la grille d’événement incluent hello ressource, un délai d’expiration et une signature.</span><span class="sxs-lookup"><span data-stu-id="a55e6-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="a55e6-146">Bonjour format du jeton SAS de hello est : `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="a55e6-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="a55e6-147">chemin d’accès hello est Hello ressource pour hello rubrique toowhich vous envoyez des événements.</span><span class="sxs-lookup"><span data-stu-id="a55e6-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="a55e6-148">Par exemple, un chemin d’accès de ressource valide est :`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="a55e6-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="a55e6-149">Pour générer des signatures de hello à partir d’une clé.</span><span class="sxs-lookup"><span data-stu-id="a55e6-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="a55e6-150">Par exemple, une valeur **aeg-sas-token** valide est :</span><span class="sxs-lookup"><span data-stu-id="a55e6-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="a55e6-151">Hello, l’exemple suivant crée un jeton SAP pour une utilisation avec la grille d’événement :</span><span class="sxs-lookup"><span data-stu-id="a55e6-151">hello following example creates a SAS token for use with Event Grid:</span></span>

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

## <a name="management-access-control"></a><span data-ttu-id="a55e6-152">Contrôle d’accès à la gestion</span><span class="sxs-lookup"><span data-stu-id="a55e6-152">Management Access Control</span></span>

<span data-ttu-id="a55e6-153">Grille d’événement Azure permet de vous toocontrol hello au niveau d’accès donné toodifferent utilisateurs toodo plusieurs opérations de gestion telles que les abonnements d’événement de liste, créer de nouveaux et générer des clés.</span><span class="sxs-lookup"><span data-stu-id="a55e6-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="a55e6-154">Pour cela, Event Grid utilise la vérification d’accès par rôle (RBAC).</span><span class="sxs-lookup"><span data-stu-id="a55e6-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="a55e6-155">Types d’opération</span><span class="sxs-lookup"><span data-stu-id="a55e6-155">Operation types</span></span>

<span data-ttu-id="a55e6-156">Grille d’événement Azure prend en charge hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="a55e6-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="a55e6-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="a55e6-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="a55e6-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="a55e6-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="a55e6-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="a55e6-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="a55e6-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="a55e6-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="a55e6-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="a55e6-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="a55e6-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="a55e6-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="a55e6-163">Bonjour les trois dernières opérations retournent potentiellement secret des informations qui obtient filtrage dans les opérations de lecture normales.</span><span class="sxs-lookup"><span data-stu-id="a55e6-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="a55e6-164">Il est recommandé pour vous, les opérations de toothese toorestrict accès.</span><span class="sxs-lookup"><span data-stu-id="a55e6-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="a55e6-165">Des rôles personnalisés peuvent être créés à l’aide de [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Interface de ligne de commande (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)et hello [API REST](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="a55e6-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="a55e6-166">Application de la vérification d’accès par rôle (RBAC)</span><span class="sxs-lookup"><span data-stu-id="a55e6-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="a55e6-167">Hello suivant les étapes tooenforce RBAC pour différents utilisateurs, utilisez :</span><span class="sxs-lookup"><span data-stu-id="a55e6-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="a55e6-168">Créer un fichier de définition de rôle personnalisé (.json)</span><span class="sxs-lookup"><span data-stu-id="a55e6-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="a55e6-169">Hello Voici des exemples de définitions de rôle grille d’événement qui permettent aux utilisateurs tooperform différents ensembles d’actions.</span><span class="sxs-lookup"><span data-stu-id="a55e6-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="a55e6-170">**EventGridReadOnlyRole.json** : pour autoriser uniquement les opérations en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="a55e6-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
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

<span data-ttu-id="a55e6-171">**EventGridNoDeleteListKeysRole.json** : pour autoriser des actions de publication limitées, et interdire les actions de suppression.</span><span class="sxs-lookup"><span data-stu-id="a55e6-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
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
 
<span data-ttu-id="a55e6-172">**EventGridContributorRole.json**: pour autoriser toutes les actions dans Event Grid.</span><span class="sxs-lookup"><span data-stu-id="a55e6-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
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

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="a55e6-173">Installation et ouverture de session tooAzure CLI</span><span class="sxs-lookup"><span data-stu-id="a55e6-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="a55e6-174">Azure CLI version 0.8.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a55e6-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="a55e6-175">version la plus récente tooinstall hello et à associer à votre abonnement Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a55e6-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="a55e6-176">Azure Resource Manager dans l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="a55e6-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="a55e6-177">Accédez trop[Using hello CLI d’Azure avec hello Gestionnaire de ressources](../xplat-cli-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a55e6-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="a55e6-178">Créer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="a55e6-178">Create a custom role</span></span>

<span data-ttu-id="a55e6-179">toocreate un rôle personnalisé, utilisez :</span><span class="sxs-lookup"><span data-stu-id="a55e6-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="a55e6-180">Affecter hello rôle tooa utilisateur</span><span class="sxs-lookup"><span data-stu-id="a55e6-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="a55e6-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a55e6-181">Next steps</span></span>

* <span data-ttu-id="a55e6-182">Pour une introduction tooEvent grille, consultez [sur la grille d’événement](overview.md)</span><span class="sxs-lookup"><span data-stu-id="a55e6-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>
