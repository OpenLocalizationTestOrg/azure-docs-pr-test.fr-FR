---
title: "Sécuriser l’accès à Azure Logic Apps | Microsoft Docs"
description: "Renforcez la sécurité pour protéger l’accès aux déclencheurs, aux entrées et sorties, aux paramètres d’action et aux services utilisés avec des workflows dans Azure Logic Apps."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 0528d660f590e106f61729f10f8f68da3fe58cb7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-access-to-your-logic-apps"></a><span data-ttu-id="6c347-103">Sécurisation de l’accès à vos applications logiques</span><span class="sxs-lookup"><span data-stu-id="6c347-103">Secure access to your logic apps</span></span>

<span data-ttu-id="6c347-104">De nombreux outils sont disponibles pour vous aider à sécuriser votre application logique.</span><span class="sxs-lookup"><span data-stu-id="6c347-104">There are many tools available to help you secure your logic app.</span></span>

* <span data-ttu-id="6c347-105">Sécurisation de l’accès au déclencheur d’une application logique (Déclencheur de requête HTTP)</span><span class="sxs-lookup"><span data-stu-id="6c347-105">Securing access to trigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="6c347-106">Sécurisation de l’accès pour gérer, modifier ou lire une application logique</span><span class="sxs-lookup"><span data-stu-id="6c347-106">Securing access to manage, edit, or read a logic app</span></span>
* <span data-ttu-id="6c347-107">Sécurisation de l’accès au contenu des entrées et sorties d’une exécution</span><span class="sxs-lookup"><span data-stu-id="6c347-107">Securing access to contents of inputs and outputs for a run</span></span>
* <span data-ttu-id="6c347-108">Sécurisation des paramètres ou des entrées dans des actions d’un flux de travail</span><span class="sxs-lookup"><span data-stu-id="6c347-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="6c347-109">Sécurisation de l’accès aux services recevant des requêtes d’un flux de travail</span><span class="sxs-lookup"><span data-stu-id="6c347-109">Securing access to services that receive requests from a workflow</span></span>

## <a name="secure-access-to-trigger"></a><span data-ttu-id="6c347-110">Sécuriser l’accès au déclencheur</span><span class="sxs-lookup"><span data-stu-id="6c347-110">Secure access to trigger</span></span>

<span data-ttu-id="6c347-111">Lorsque vous utilisez une application logique déclenchée par une requête HTTP ([Requête](../connectors/connectors-native-reqres.md) ou [Webhook](../connectors/connectors-native-webhook.md)), vous pouvez limiter l’accès de sorte que seuls les clients autorisés puissent déclencher l’application logique.</span><span class="sxs-lookup"><span data-stu-id="6c347-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app.</span></span> <span data-ttu-id="6c347-112">Toutes les requêtes dans une application logique sont chiffrées et sécurisées via SSL.</span><span class="sxs-lookup"><span data-stu-id="6c347-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="6c347-113">Signature d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="6c347-113">Shared Access Signature</span></span>

<span data-ttu-id="6c347-114">Chaque point de terminaison de requête pour une application logique inclut une partie [Signature d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAP) dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="6c347-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of the URL.</span></span> <span data-ttu-id="6c347-115">Chaque URL contient un paramètre de requête `sp`, `sv` et `sig`.</span><span class="sxs-lookup"><span data-stu-id="6c347-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="6c347-116">Les autorisations sont spécifiées par `sp` et correspondent aux méthodes HTTP autorisées, `sv` est la version utilisée pour générer et `sig` est utilisé pour authentifier l’accès au déclencheur.</span><span class="sxs-lookup"><span data-stu-id="6c347-116">Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger.</span></span> <span data-ttu-id="6c347-117">La signature est générée à l’aide de l’algorithme SHA 256 avec une clé secrète sur tous les chemins d’accès à l’URL et les propriétés.</span><span class="sxs-lookup"><span data-stu-id="6c347-117">The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties.</span></span> <span data-ttu-id="6c347-118">La clé secrète n’est jamais exposée et publiée, et est chiffrée et stockée dans l’application logique.</span><span class="sxs-lookup"><span data-stu-id="6c347-118">The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app.</span></span> <span data-ttu-id="6c347-119">Votre application logique autorise uniquement les déclencheurs contenant une signature valide créée avec la clé secrète.</span><span class="sxs-lookup"><span data-stu-id="6c347-119">Your logic app only authorizes triggers that contain a valid signature created with the secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="6c347-120">Régénération de clés d'accès</span><span class="sxs-lookup"><span data-stu-id="6c347-120">Regenerate access keys</span></span>

<span data-ttu-id="6c347-121">Vous pouvez régénérer une nouvelle clé sécurisée à tout moment via l’API REST ou le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6c347-121">You can regenerate a new secure key at anytime through the REST API or Azure portal.</span></span> <span data-ttu-id="6c347-122">Toutes les URL actuelles, qui ont été générées précédemment à l’aide de l’ancienne clé, sont invalidées et ne sont plus autorisées pour déclencher l’application logique.</span><span class="sxs-lookup"><span data-stu-id="6c347-122">All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.</span></span>

1. <span data-ttu-id="6c347-123">Dans le portail Azure, ouvrez l’application logique dont vous souhaitez régénérer une clé</span><span class="sxs-lookup"><span data-stu-id="6c347-123">In the Azure portal, open the logic app you want to regenerate a key</span></span>
1. <span data-ttu-id="6c347-124">Cliquez sur l’élément de menu **Clés d’accès** sous **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="6c347-124">Click the **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="6c347-125">Choisissez la clé à régénérer et terminez le processus</span><span class="sxs-lookup"><span data-stu-id="6c347-125">Choose the key to regenerate and complete the process</span></span>

<span data-ttu-id="6c347-126">Les URL que vous récupérez après la régénération sont signées avec la nouvelle clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="6c347-126">URLs you retrieve after regeneration are signed with the new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="6c347-127">Création d’URL de rappel avec une date d’expiration</span><span class="sxs-lookup"><span data-stu-id="6c347-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="6c347-128">Si vous partagez l’URL avec d’autres utilisateurs, vous pouvez générer des URL avec des clés et des dates d’expiration spécifiques si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6c347-128">If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="6c347-129">Vous pouvez alors déployer des clés de manière transparente, ou de garantir que l’accès pour déclencher une application est limité à un intervalle de temps donné.</span><span class="sxs-lookup"><span data-stu-id="6c347-129">You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan.</span></span> <span data-ttu-id="6c347-130">Vous pouvez spécifier une date d’expiration pour une URL via l’[API REST de Logic Apps](https://docs.microsoft.com/rest/api/logic/workflowtriggers) :</span><span class="sxs-lookup"><span data-stu-id="6c347-130">You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="6c347-131">Dans le corps, incluez la propriété `NotAfter` en tant que chaîne de date JSON, qui renvoie une URL de rappel qui n’est valide que jusqu’à ce que la date et l’heure `NotAfter`.</span><span class="sxs-lookup"><span data-stu-id="6c347-131">In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="6c347-132">Création d’URL avec une clé de secret principale ou secondaire</span><span class="sxs-lookup"><span data-stu-id="6c347-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="6c347-133">Lorsque vous générez ou répertoriez des URL de rappel pour des déclencheurs basés sur une requête, vous pouvez également spécifier la clé à utiliser pour signer l’URL.</span><span class="sxs-lookup"><span data-stu-id="6c347-133">When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.</span></span>  <span data-ttu-id="6c347-134">Vous pouvez générer une URL signée par une clé spécifique via l’[API REST de Logic Apps](https://docs.microsoft.com/rest/api/logic/workflowtriggers) comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c347-134">You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="6c347-135">Dans le corps, incluez la propriété `KeyType` en tant que `Primary` ou `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="6c347-135">In the body, include the property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="6c347-136">Cela renvoie une URL signée par la clé sécurisée spécifiée.</span><span class="sxs-lookup"><span data-stu-id="6c347-136">This returns a URL signed by the secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="6c347-137">Limiter les adresses IP entrantes</span><span class="sxs-lookup"><span data-stu-id="6c347-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="6c347-138">En plus de la signature d’accès partagé, vous pouvez souhaiter limiter l’appel d’une application logique à partir de clients spécifiques uniquement.</span><span class="sxs-lookup"><span data-stu-id="6c347-138">In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="6c347-139">Par exemple, si vous gérez votre point de terminaison via gestion des API Azure, vous pouvez limiter l’application logique à n’accepter la requête que lorsqu’elle provient de l’adresse IP d’instance de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="6c347-139">For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.</span></span>

<span data-ttu-id="6c347-140">Ce paramètre peut être configuré dans les paramètres d’application logique :</span><span class="sxs-lookup"><span data-stu-id="6c347-140">This setting can be configured within the logic app settings:</span></span>

1. <span data-ttu-id="6c347-141">Dans le portail Azure, ouvrez l’application logique à laquelle vous souhaitez ajouter des restrictions d’adresse IP</span><span class="sxs-lookup"><span data-stu-id="6c347-141">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="6c347-142">Cliquez sur l’élément de menu **Configuration du contrôle d’accès** sous **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="6c347-142">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="6c347-143">Spécifier la liste des plages d’adresses IP acceptées par le déclencheur</span><span class="sxs-lookup"><span data-stu-id="6c347-143">Specify the list of IP address ranges to be accepted by the trigger</span></span>

<span data-ttu-id="6c347-144">Une plage d’adresses IP valide se présente au format `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="6c347-144">A valid IP range takes the format `192.168.1.1/255`.</span></span> <span data-ttu-id="6c347-145">Si vous souhaitez que l’application logique ne soit déclenchée que comme une application logique imbriquée, sélectionnez l’option **Autres applications logiques uniquement**.</span><span class="sxs-lookup"><span data-stu-id="6c347-145">If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option.</span></span> <span data-ttu-id="6c347-146">Cette option écrit un tableau vide est écrit sur la ressource, ce qui signifie que seuls les appels du service lui-même (applications logiques parentes) entraînent un déclenchement.</span><span class="sxs-lookup"><span data-stu-id="6c347-146">This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="6c347-147">Vous pouvez toujours exécuter une application logique avec un déclencheur de requête via l’API REST / Gestion `/triggers/{triggerName}/run`, quelle que soit l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="6c347-147">You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="6c347-148">Ce scénario nécessite une authentification auprès de l’API REST Azure, et tous les événements apparaissent dans le journal d’audit Azure.</span><span class="sxs-lookup"><span data-stu-id="6c347-148">This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log.</span></span> <span data-ttu-id="6c347-149">Définissez les stratégies de contrôle d’accès en conséquence.</span><span class="sxs-lookup"><span data-stu-id="6c347-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="6c347-150">Définition de plages d’adresses IP sur la définition de ressource</span><span class="sxs-lookup"><span data-stu-id="6c347-150">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="6c347-151">Si vous utilisez un [modèle de déploiement](logic-apps-create-deploy-template.md) pour automatiser vos déploiements, les paramètres de plage d’adresses IP peuvent être configurés sur le modèle de ressource.</span><span class="sxs-lookup"><span data-stu-id="6c347-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="6c347-152">Ajout d’Azure Active Directory, d’OAuth ou d’une autre sécurité</span><span class="sxs-lookup"><span data-stu-id="6c347-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="6c347-153">Pour ajouter davantage de protocoles d’autorisation sur une application logique, la [Gestion des API Azure](https://azure.microsoft.com/services/api-management/) offre des fonctions évoluées de surveillance, la sécurité, la stratégie et la documentation pour n’importe quel point de terminaison avec la possibilité d’exposer une application logique en tant qu’API.</span><span class="sxs-lookup"><span data-stu-id="6c347-153">To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API.</span></span> <span data-ttu-id="6c347-154">La Gestion des API Azure peut exposer un point de terminaison public ou privé de l’application logique, permettant ainsi d’utiliser d’Azure Active Directory, d’un certificat, d’OAuth ou d’autres normes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6c347-154">Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="6c347-155">Lorsqu’une requête est reçue, la Gestion des API Azure la transmet à l’application logique (en effectuant à la volée les transformations ou les restrictions nécessaires).</span><span class="sxs-lookup"><span data-stu-id="6c347-155">When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="6c347-156">Vous pouvez utiliser les paramètres de plage d’adresses IP entrantes sur l’application logique pour autoriser le déclenchement de l’application logique à partir de la Gestion des API uniquement.</span><span class="sxs-lookup"><span data-stu-id="6c347-156">You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.</span></span>

## <a name="secure-access-to-manage-or-edit-logic-apps"></a><span data-ttu-id="6c347-157">Sécuriser l’accès pour gérer ou modifier des applications logiques</span><span class="sxs-lookup"><span data-stu-id="6c347-157">Secure access to manage or edit logic apps</span></span>

<span data-ttu-id="6c347-158">Vous pouvez limiter l’accès aux opérations de gestion sur une application logique de sorte que seuls des utilisateurs ou groupes spécifiques soient en mesure d’effectuer des opérations sur la ressource.</span><span class="sxs-lookup"><span data-stu-id="6c347-158">You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource.</span></span> <span data-ttu-id="6c347-159">Les applications logiques utilisent la fonctionnalité [Contrôle d’accès basé sur les rôles (RBAC)](../active-directory/role-based-access-control-configure.md), et peuvent être personnalisées avec les mêmes outils.</span><span class="sxs-lookup"><span data-stu-id="6c347-159">Logic apps use the Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with the same tools.</span></span>  <span data-ttu-id="6c347-160">Vous pouvez également affecter des rôles intégrés aux membres de votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="6c347-160">There are a few built-in roles you can assign members of your subscription to as well:</span></span>

* <span data-ttu-id="6c347-161">**Collaborateur d’application logique** : accorde un accès pour afficher, modifier et mettre à jour une application logique.</span><span class="sxs-lookup"><span data-stu-id="6c347-161">**Logic App Contributor** - Provides access to view, edit, and update a logic app.</span></span>  <span data-ttu-id="6c347-162">Il ne peut pas supprimer la ressource ou effectuer des opérations d’administration.</span><span class="sxs-lookup"><span data-stu-id="6c347-162">Cannot remove the resource or perform admin operations.</span></span>
* <span data-ttu-id="6c347-163">**Opérateur d’application logique** : peut afficher l’application logique et l’historique d’exécution, et activer/désactiver.</span><span class="sxs-lookup"><span data-stu-id="6c347-163">**Logic App Operator** - Can view the logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="6c347-164">Il ne peut pas modifier ou mettre à jour la définition.</span><span class="sxs-lookup"><span data-stu-id="6c347-164">Cannot edit or update the definition.</span></span>

<span data-ttu-id="6c347-165">Vous pouvez également utiliser le [Verrouillage de la ressource Azure](../azure-resource-manager/resource-group-lock-resources.md) pour empêcher la modification ou suppression des applications logiques.</span><span class="sxs-lookup"><span data-stu-id="6c347-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps.</span></span> <span data-ttu-id="6c347-166">Cette fonctionnalité est utile pour éviter que des ressources de production ne soient modifiées ou supprimées.</span><span class="sxs-lookup"><span data-stu-id="6c347-166">This capability is valuable to prevent production resources from changes or deletions.</span></span>

## <a name="secure-access-to-contents-of-the-run-history"></a><span data-ttu-id="6c347-167">Sécuriser l’accès au contenu de l’historique d’exécution</span><span class="sxs-lookup"><span data-stu-id="6c347-167">Secure access to contents of the run history</span></span>

<span data-ttu-id="6c347-168">Vous pouvez limiter l’accès au contenu des entrées ou sorties d’exécutions précédentes à des plages d’adresses IP spécifiques.</span><span class="sxs-lookup"><span data-stu-id="6c347-168">You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.</span></span>  

<span data-ttu-id="6c347-169">Toutes les données de l’exécution d’un flux de travail sont chiffrées pendant le transit et au repos.</span><span class="sxs-lookup"><span data-stu-id="6c347-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="6c347-170">Lorsque l’historique d’exécution est appelé, le service authentifie la requête et fournit des liens vers les entrées et sorties de la requête et de la réponse.</span><span class="sxs-lookup"><span data-stu-id="6c347-170">When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs.</span></span> <span data-ttu-id="6c347-171">Ces liens peuvent être protégés afin que seules les requêtes d’affichage du contenu provenant d’une plage d’adresses IP désignée renvoient le contenu.</span><span class="sxs-lookup"><span data-stu-id="6c347-171">This link can be protected so only requests to view content from a designated IP address range return the contents.</span></span> <span data-ttu-id="6c347-172">Vous pouvez utiliser cette fonctionnalité pour obtenir un contrôle d’accès supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="6c347-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="6c347-173">Vous pouvez également spécifier une adresse IP telle que `0.0.0.0` afin que personne ne puisse accéder aux entrées/sorties.</span><span class="sxs-lookup"><span data-stu-id="6c347-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="6c347-174">Seul un utilisateur disposant d’autorisations d’administrateur peut supprimer cette restriction, permettant ainsi d’obtenir un accès « juste-à-temps » au contenu du flux de travail.</span><span class="sxs-lookup"><span data-stu-id="6c347-174">Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.</span></span>

<span data-ttu-id="6c347-175">Ce paramètre peut être configuré dans les paramètres de ressource du portail Azure :</span><span class="sxs-lookup"><span data-stu-id="6c347-175">This setting can be configured within the resource settings of the Azure portal:</span></span>

1. <span data-ttu-id="6c347-176">Dans le portail Azure, ouvrez l’application logique à laquelle vous souhaitez ajouter des restrictions d’adresse IP</span><span class="sxs-lookup"><span data-stu-id="6c347-176">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="6c347-177">Cliquez sur l’élément de menu **Configuration du contrôle d’accès** sous **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="6c347-177">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="6c347-178">Spécifier la liste des plages d’adresses IP pour accéder au contenu</span><span class="sxs-lookup"><span data-stu-id="6c347-178">Specify the list of IP address ranges for access to content</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="6c347-179">Définition de plages d’adresses IP sur la définition de ressource</span><span class="sxs-lookup"><span data-stu-id="6c347-179">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="6c347-180">Si vous utilisez un [modèle de déploiement](logic-apps-create-deploy-template.md) pour automatiser vos déploiements, les paramètres de plage d’adresses IP peuvent être configurés sur le modèle de ressource.</span><span class="sxs-lookup"><span data-stu-id="6c347-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="6c347-181">Sécuriser les paramètres et les entrées dans un flux de travail</span><span class="sxs-lookup"><span data-stu-id="6c347-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="6c347-182">Vous souhaiterez peut-être paramétrer certains aspects d’une définition de flux de travail pour le déploiement dans divers environnements.</span><span class="sxs-lookup"><span data-stu-id="6c347-182">You might want to parameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="6c347-183">Certains de ces paramètres peuvent également être des paramètres sécurisés que vous ne souhaitez pas voir apparaître lors de la modification d’un flux de travail, comme un ID client et la clé secrète client pour l’[authentification Azure Active Directory](../connectors/connectors-native-http.md#authentication) d’une action HTTP.</span><span class="sxs-lookup"><span data-stu-id="6c347-183">Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="6c347-184">Utilisation des paramètres et des paramètres sécurisés</span><span class="sxs-lookup"><span data-stu-id="6c347-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="6c347-185">Le [langage de définition de flux de travail](http://aka.ms/logicappsdocs) fournit une opération `@parameters()` pour accéder à la valeur d’un paramètre de ressource lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6c347-185">To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="6c347-186">Vous pouvez également [spécifier des paramètres dans le modèle de déploiement de ressource](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="6c347-186">Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="6c347-187">Mais si vous spécifiez le type de paramètre `securestring`, le paramètre n’est pas renvoyé avec la définition de la ressource, et n’est donc pas accessible en consultant la ressource après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="6c347-187">But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="6c347-188">Si votre paramètre est utilisé dans les en-têtes ou le corps d’une requête, il peut être visible en accédant à l’historique d’exécution et à la requête HTTP sortante.</span><span class="sxs-lookup"><span data-stu-id="6c347-188">If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request.</span></span> <span data-ttu-id="6c347-189">Veillez à définir vos stratégies d’accès au contenu en conséquence.</span><span class="sxs-lookup"><span data-stu-id="6c347-189">Make sure to set your content access policies accordingly.</span></span>
> <span data-ttu-id="6c347-190">Les en-têtes d’autorisation ne sont jamais visibles par le biais d’entrées ou de sorties.</span><span class="sxs-lookup"><span data-stu-id="6c347-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="6c347-191">Si la clé secrète est utilisée ici, elle n’est pas récupérable.</span><span class="sxs-lookup"><span data-stu-id="6c347-191">So if the secret is being used there, the secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="6c347-192">Modèle de déploiement de ressource avec des clés secrètes</span><span class="sxs-lookup"><span data-stu-id="6c347-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="6c347-193">Voici un exemple de déploiement qui fait référence à un paramètre sécurisé de `secret` lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6c347-193">The following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="6c347-194">Dans un fichier de paramètres distinct, vous pouvez spécifier la valeur d’environnement pour `secret` ou utiliser le [Coffre de clés Azure Resource Manager](../azure-resource-manager/resource-manager-keyvault-parameter.md) pour récupérer vos clés secrètes au moment du déploiement.</span><span class="sxs-lookup"><span data-stu-id="6c347-194">In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is the request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-to-services-receiving-requests-from-a-workflow"></a><span data-ttu-id="6c347-195">Sécuriser l’accès aux services recevant des requêtes d’un flux de travail</span><span class="sxs-lookup"><span data-stu-id="6c347-195">Secure access to services receiving requests from a workflow</span></span>

<span data-ttu-id="6c347-196">De nombreuses méthodes sont possibles pour sécuriser un point de terminaison auquel l’application logique doit accéder.</span><span class="sxs-lookup"><span data-stu-id="6c347-196">There are many ways to help secure any endpoint the logic app needs to access.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="6c347-197">Utilisation de l’authentification sur les requêtes sortantes</span><span class="sxs-lookup"><span data-stu-id="6c347-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="6c347-198">Lorsque vous utilisez une action HTTP, HTTP + Swagger (API ouverte) ou Webhook, vous pouvez ajouter l’authentification à la requête envoyée.</span><span class="sxs-lookup"><span data-stu-id="6c347-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent.</span></span> <span data-ttu-id="6c347-199">Vous pouvez inclure l’authentification de base, l’authentification par certificat ou l’authentification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6c347-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="6c347-200">Des détails sur la configuration cette authentification se fournis [dans cet article](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="6c347-200">Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-to-logic-app-ip-addresses"></a><span data-ttu-id="6c347-201">Limitation de l’accès aux adresses IP d’application logique</span><span class="sxs-lookup"><span data-stu-id="6c347-201">Restricting access to logic app IP addresses</span></span>

<span data-ttu-id="6c347-202">Tous les appels d’applications logiques proviennent d’un ensemble spécifique d’adresses IP par région.</span><span class="sxs-lookup"><span data-stu-id="6c347-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="6c347-203">Vous pouvez ajouter un filtrage supplémentaire afin d’accepter ces adresses IP désignées uniquement.</span><span class="sxs-lookup"><span data-stu-id="6c347-203">You can add additional filtering to only accept requests from those designated IP addresses.</span></span> <span data-ttu-id="6c347-204">Pour obtenir la liste de ces adresses IP, consultez [Limites et configuration des applications logiques](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="6c347-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="6c347-205">Connectivité locale</span><span class="sxs-lookup"><span data-stu-id="6c347-205">On-premises connectivity</span></span>

<span data-ttu-id="6c347-206">Logic Apps permet l’intégration plusieurs services afin de fournir une communication locale sécurisée et fiable.</span><span class="sxs-lookup"><span data-stu-id="6c347-206">Logic apps provide integration with several services to provide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="6c347-207">Passerelle de données locale</span><span class="sxs-lookup"><span data-stu-id="6c347-207">On-premises data gateway</span></span>

<span data-ttu-id="6c347-208">De nombreux connecteurs gérés d’applications logiques fournissent une connectivité sécurisée aux systèmes locaux, notamment le système de fichiers, SQL, SharePoint, DB2 et bien d’autres encore.</span><span class="sxs-lookup"><span data-stu-id="6c347-208">Many managed connectors for logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="6c347-209">La passerelle transmet des données à partir de sources locales sur des canaux chiffrés via Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6c347-209">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="6c347-210">Tout le trafic est initialisé en tant que trafic sortant de l’agent de passerelle sécurisé.</span><span class="sxs-lookup"><span data-stu-id="6c347-210">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="6c347-211">En savoir plus sur le [fonctionnement de la passerelle de données](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="6c347-211">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="6c347-212">Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="6c347-212">Azure API Management</span></span>

<span data-ttu-id="6c347-213">[Gestion des API Azure](https://azure.microsoft.com/services/api-management/) inclut des options de connectivité locale, notamment l’intégration VPN de site à site et ExpressRoute pour un proxy et une communication sécurisés vers les systèmes locaux.</span><span class="sxs-lookup"><span data-stu-id="6c347-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems.</span></span> <span data-ttu-id="6c347-214">Dans le concepteur d’application logique, vous pouvez sélectionner rapidement une API exposée à partir de la Gestion des API Azure dans un flux de travail, offrant ainsi un accès rapide aux systèmes locaux.</span><span class="sxs-lookup"><span data-stu-id="6c347-214">In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="6c347-215">Connexions hybrides à partir des services d’application Azure</span><span class="sxs-lookup"><span data-stu-id="6c347-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="6c347-216">Vous pouvez utiliser la fonctionnalité de connexion hybride locale pour que l’API Azure et les applications web communiquent en local.</span><span class="sxs-lookup"><span data-stu-id="6c347-216">You can use the on-premises hybrid connection feature for Azure API and Web apps to communicate on-premises.</span></span>  <span data-ttu-id="6c347-217">Des détails sur les connexions hybrides et leur configuration sont fournis [dans cet article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6c347-217">Details on hybrid connections and how to configure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c347-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c347-218">Next steps</span></span>
[<span data-ttu-id="6c347-219">Créer un modèle de déploiement</span><span class="sxs-lookup"><span data-stu-id="6c347-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="6c347-220">Gestion des exceptions</span><span class="sxs-lookup"><span data-stu-id="6c347-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="6c347-221">Analyser vos applications logiques</span><span class="sxs-lookup"><span data-stu-id="6c347-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="6c347-222">Diagnostic des échecs et problèmes d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="6c347-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
