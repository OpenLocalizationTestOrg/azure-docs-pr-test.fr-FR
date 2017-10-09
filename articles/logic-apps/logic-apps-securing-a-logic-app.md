---
title: "aaaSecure accéder aux applications de la logique de tooAzure | Documents Microsoft"
description: "Ajoutez la sécurité pour la protection d’accès tootriggers, entrées et sorties, paramètres d’action et services utilisés avec les flux de travail dans Azure Logic Apps."
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
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a><span data-ttu-id="71b65-103">Sécuriser l’accès aux applications de la logique de tooyour</span><span class="sxs-lookup"><span data-stu-id="71b65-103">Secure access tooyour logic apps</span></span>

<span data-ttu-id="71b65-104">Il existe des nombreux toohelp disponible outils vous sécurisez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="71b65-104">There are many tools available toohelp you secure your logic app.</span></span>

* <span data-ttu-id="71b65-105">Sécurisation des accès tootrigger une logique d’application (déclencheur de demande HTTP)</span><span class="sxs-lookup"><span data-stu-id="71b65-105">Securing access tootrigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="71b65-106">Sécurisation des accès toomanage, modifier, ou une application de la logique de lecture</span><span class="sxs-lookup"><span data-stu-id="71b65-106">Securing access toomanage, edit, or read a logic app</span></span>
* <span data-ttu-id="71b65-107">Sécurisation de toocontents d’accès d’entrées et sorties pour une exécution</span><span class="sxs-lookup"><span data-stu-id="71b65-107">Securing access toocontents of inputs and outputs for a run</span></span>
* <span data-ttu-id="71b65-108">Sécurisation des paramètres ou des entrées dans des actions d’un flux de travail</span><span class="sxs-lookup"><span data-stu-id="71b65-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="71b65-109">Sécurisation des accès tooservices qui reçoivent des requêtes à partir d’un flux de travail</span><span class="sxs-lookup"><span data-stu-id="71b65-109">Securing access tooservices that receive requests from a workflow</span></span>

## <a name="secure-access-tootrigger"></a><span data-ttu-id="71b65-110">Sécuriser l’accès tootrigger</span><span class="sxs-lookup"><span data-stu-id="71b65-110">Secure access tootrigger</span></span>

<span data-ttu-id="71b65-111">Lorsque vous travaillez avec une application de la logique qui se déclenche sur une requête HTTP ([demande](../connectors/connectors-native-reqres.md) ou [Webhook](../connectors/connectors-native-webhook.md)), vous pouvez restreindre l’accès afin que seuls les clients autorisés peuvent déclencher l’application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire hello logic app.</span></span> <span data-ttu-id="71b65-112">Toutes les requêtes dans une application logique sont chiffrées et sécurisées via SSL.</span><span class="sxs-lookup"><span data-stu-id="71b65-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="71b65-113">Signature d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="71b65-113">Shared Access Signature</span></span>

<span data-ttu-id="71b65-114">Chaque point de terminaison de demande pour une application logique inclut un [Signature d’accès partagé (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) dans le cadre de l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of hello URL.</span></span> <span data-ttu-id="71b65-115">Chaque URL contient un paramètre de requête `sp`, `sv` et `sig`.</span><span class="sxs-lookup"><span data-stu-id="71b65-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="71b65-116">Les autorisations sont spécifiées par `sp`, et elles correspondent à des méthodes tooHTTP autorisées, `sv` est hello version utilisée toogenerate, et `sig` est tootrigger d’accès tooauthenticate utilisé.</span><span class="sxs-lookup"><span data-stu-id="71b65-116">Permissions are specified by `sp`, and correspond tooHTTP methods allowed, `sv` is hello version used toogenerate, and `sig` is used tooauthenticate access tootrigger.</span></span> <span data-ttu-id="71b65-117">signature de Hello est généré à l’aide d’algorithme de hello SHA256 avec une clé secrète sur tous les chemins d’accès des URL hello et propriétés.</span><span class="sxs-lookup"><span data-stu-id="71b65-117">hello signature is generated using hello SHA256 algorithm with a secret key on all hello URL paths and properties.</span></span> <span data-ttu-id="71b65-118">clé secrète de Hello n’est jamais exposée et publiée et sont chiffrées et stockées dans le cadre de l’application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-118">hello secret key is never exposed and published, and is kept encrypted and stored as part of hello logic app.</span></span> <span data-ttu-id="71b65-119">Votre application logique autorise uniquement les déclencheurs qui contiennent une signature valide créée avec une clé secrète hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-119">Your logic app only authorizes triggers that contain a valid signature created with hello secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="71b65-120">Régénération de clés d'accès</span><span class="sxs-lookup"><span data-stu-id="71b65-120">Regenerate access keys</span></span>

<span data-ttu-id="71b65-121">Vous pouvez régénérer une clé sécurisée au niveau à tout moment via le portail d’API REST ou Azure hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-121">You can regenerate a new secure key at anytime through hello REST API or Azure portal.</span></span> <span data-ttu-id="71b65-122">Toutes les URL actuelles qui ont été créés précédemment à l’aide de la clé d’anciens hello sont application logique de hello toofire invalidé et ne sont plus autorisés.</span><span class="sxs-lookup"><span data-stu-id="71b65-122">All current URLs that were generated previously using hello old key are invalidated and no longer authorized toofire hello logic app.</span></span>

1. <span data-ttu-id="71b65-123">Bonjour portail Azure, ouvrez hello logique application tooregenerate une clé</span><span class="sxs-lookup"><span data-stu-id="71b65-123">In hello Azure portal, open hello logic app you want tooregenerate a key</span></span>
1. <span data-ttu-id="71b65-124">Cliquez sur hello **clés d’accès** élément de menu sous **paramètres**</span><span class="sxs-lookup"><span data-stu-id="71b65-124">Click hello **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="71b65-125">Choisissez tooregenerate de clé hello et processus de hello terminée</span><span class="sxs-lookup"><span data-stu-id="71b65-125">Choose hello key tooregenerate and complete hello process</span></span>

<span data-ttu-id="71b65-126">Après la régénération de récupérer les URL sont signés avec la nouvelle clé d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-126">URLs you retrieve after regeneration are signed with hello new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="71b65-127">Création d’URL de rappel avec une date d’expiration</span><span class="sxs-lookup"><span data-stu-id="71b65-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="71b65-128">Si vous partagez avec d’autres parties hello URL, vous pouvez générer des URL avec des clés spécifiques et les dates d’expiration en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="71b65-128">If you are sharing hello URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="71b65-129">Vous pouvez accéder en toute transparence substituer les clés, ou vérifiez toofire d’accès à une application est restreint tooa certaine timespan.</span><span class="sxs-lookup"><span data-stu-id="71b65-129">You can then seamlessly roll keys, or ensure access toofire an app is restricted tooa certain timespan.</span></span> <span data-ttu-id="71b65-130">Vous pouvez spécifier une date d’expiration pour une URL via hello [logique applications API REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="71b65-130">You can specify an expiration date for a URL through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="71b65-131">Dans le corps de hello, inclure la propriété de hello `NotAfter` comme une chaîne de date JSON, qui retourne une URL de rappel qui est uniquement valide jusqu'à hello `NotAfter` date et heure.</span><span class="sxs-lookup"><span data-stu-id="71b65-131">In hello body, include hello property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until hello `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="71b65-132">Création d’URL avec une clé de secret principale ou secondaire</span><span class="sxs-lookup"><span data-stu-id="71b65-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="71b65-133">Lorsque vous générez ou répertoriez les URL de rappel pour les déclencheurs de demande de, vous pouvez également spécifier des URL hello toosign toouse clé.</span><span class="sxs-lookup"><span data-stu-id="71b65-133">When you generate or list callback URLs for request-based triggers, you can also specify which key toouse toosign hello URL.</span></span>  <span data-ttu-id="71b65-134">Vous pouvez générer une URL signée par une clé spécifique via hello [logique applications API REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers) comme suit :</span><span class="sxs-lookup"><span data-stu-id="71b65-134">You can generate a URL signed by a specific key through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="71b65-135">Dans le corps de hello, inclure la propriété de hello `KeyType` en tant que `Primary` ou `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="71b65-135">In hello body, include hello property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="71b65-136">Cela retourne une URL signée par hello de clé sécurisée spécifiée.</span><span class="sxs-lookup"><span data-stu-id="71b65-136">This returns a URL signed by hello secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="71b65-137">Limiter les adresses IP entrantes</span><span class="sxs-lookup"><span data-stu-id="71b65-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="71b65-138">En outre toohello Signature d’accès partagé, vous pouvez toorestrict appelant une application logique uniquement à partir de clients spécifiques.</span><span class="sxs-lookup"><span data-stu-id="71b65-138">In addition toohello Shared Access Signature, you may wish toorestrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="71b65-139">Par exemple, si vous gérez votre point de terminaison via la gestion des API Azure, vous pouvez limiter la logique de hello application tooonly accepter la demande de hello lors de la demande de hello provient hello adresse IP d’instance gestion des API.</span><span class="sxs-lookup"><span data-stu-id="71b65-139">For example, if you manage your endpoint through Azure API Management, you can restrict hello logic app tooonly accept hello request when hello request comes from hello API Management instance IP address.</span></span>

<span data-ttu-id="71b65-140">Ce paramètre peut être configuré dans les paramètres de l’application hello logique :</span><span class="sxs-lookup"><span data-stu-id="71b65-140">This setting can be configured within hello logic app settings:</span></span>

1. <span data-ttu-id="71b65-141">Bonjour portail Azure, ouvrez hello logique application tooadd restrictions par adresse IP</span><span class="sxs-lookup"><span data-stu-id="71b65-141">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="71b65-142">Cliquez sur hello **configuration de contrôle d’accès** élément de menu sous **paramètres**</span><span class="sxs-lookup"><span data-stu-id="71b65-142">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="71b65-143">Spécifiez la liste hello de toobe de plages d’adresses IP accepté par le déclencheur de hello</span><span class="sxs-lookup"><span data-stu-id="71b65-143">Specify hello list of IP address ranges toobe accepted by hello trigger</span></span>

<span data-ttu-id="71b65-144">Une plage IP valide prend le format de hello `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="71b65-144">A valid IP range takes hello format `192.168.1.1/255`.</span></span> <span data-ttu-id="71b65-145">Si vous souhaitez hello logique application tooonly incendie comme application logique imbriquées, sélectionnez hello **seulement d’autres applications logique** option.</span><span class="sxs-lookup"><span data-stu-id="71b65-145">If you want hello logic app tooonly fire as a nested logic app, select hello **Only other logic apps** option.</span></span> <span data-ttu-id="71b65-146">Cette option écrit une ressource de toohello tableau vide, ce qui signifie que seuls les appels à partir de hello service proprement dit (applications de logique parent) incendie avec succès.</span><span class="sxs-lookup"><span data-stu-id="71b65-146">This option writes an empty array toohello resource, meaning only calls from hello service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="71b65-147">Vous pouvez toujours exécuter une application logique avec un déclencheur de la demande via l’API REST de hello / gestion `/triggers/{triggerName}/run` , quelle que soit l’IP.</span><span class="sxs-lookup"><span data-stu-id="71b65-147">You can still run a logic app with a request trigger through hello REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="71b65-148">Ce scénario requiert une authentification par rapport à hello API REST Azure, et tous les événements apparaît dans les journaux d’Audit Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-148">This scenario requires authentication against hello Azure REST API, and all events would appear in hello Azure Audit Log.</span></span> <span data-ttu-id="71b65-149">Définissez les stratégies de contrôle d’accès en conséquence.</span><span class="sxs-lookup"><span data-stu-id="71b65-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="71b65-150">Définition de plages d’adresses IP sur la définition de ressource hello</span><span class="sxs-lookup"><span data-stu-id="71b65-150">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="71b65-151">Si vous utilisez un [modèle de déploiement](logic-apps-create-deploy-template.md) tooautomate vos déploiements, les paramètres des plages IP hello peuvent être configurés sur le modèle de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

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

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="71b65-152">Ajout d’Azure Active Directory, d’OAuth ou d’une autre sécurité</span><span class="sxs-lookup"><span data-stu-id="71b65-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="71b65-153">tooadd d’autorisation de plusieurs protocoles sur une application logique, [gestion des API Azure](https://azure.microsoft.com/services/api-management/) offre riche analyse, sécurité, la stratégie et documentation pour n’importe quel point de terminaison avec hello fonctionnalité tooexpose une application logique en tant qu’une API.</span><span class="sxs-lookup"><span data-stu-id="71b65-153">tooadd more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with hello capability tooexpose a logic app as an API.</span></span> <span data-ttu-id="71b65-154">Gestion des API Azure peuvent exposer un point de terminaison public ou privé pour l’application hello logique, pouvant utiliser Azure Active Directory, certificat, OAuth ou autres normes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="71b65-154">Azure API Management can expose a public or private endpoint for hello logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="71b65-155">Lorsqu’une demande est reçue, gestion des API Azure transfère hello demande toohello logique application (exécution de toutes les transformations nécessaires ou les restrictions en cours).</span><span class="sxs-lookup"><span data-stu-id="71b65-155">When a request is received, Azure API Management forwards hello request toohello logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="71b65-156">Vous pouvez utiliser la plage IP entrant de hello paramètres hello logique application tooonly autorisent hello logique application toobe déclenchée à partir de la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="71b65-156">You can use hello incoming IP range settings on hello logic app tooonly allow hello logic app toobe triggered from API Management.</span></span>

## <a name="secure-access-toomanage-or-edit-logic-apps"></a><span data-ttu-id="71b65-157">Sécuriser l’accès aux applications de logique toomanage ou modifier</span><span class="sxs-lookup"><span data-stu-id="71b65-157">Secure access toomanage or edit logic apps</span></span>

<span data-ttu-id="71b65-158">Vous pouvez limiter les opérations d’accès toomanagement sur une logique d’application afin que seuls des utilisateurs ou groupes soient tooperform en mesure des opérations sur les ressources hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-158">You can restrict access toomanagement operations on a logic app so that only specific users or groups are able tooperform operations on hello resource.</span></span> <span data-ttu-id="71b65-159">Les applications de logique utilisent hello Azure [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md) fonctionnalité et peut être personnalisée avec hello mêmes outils.</span><span class="sxs-lookup"><span data-stu-id="71b65-159">Logic apps use hello Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with hello same tools.</span></span>  <span data-ttu-id="71b65-160">Il existe quelques rôles intégrés, que vous pouvez affecter des membres de votre abonnement de tooas bien :</span><span class="sxs-lookup"><span data-stu-id="71b65-160">There are a few built-in roles you can assign members of your subscription tooas well:</span></span>

* <span data-ttu-id="71b65-161">**Collaboration d’application logique** -fournit l’accès tooview, modifier et mettre à jour une application logique.</span><span class="sxs-lookup"><span data-stu-id="71b65-161">**Logic App Contributor** - Provides access tooview, edit, and update a logic app.</span></span>  <span data-ttu-id="71b65-162">Impossible de supprimer la ressource de hello ou effectuer des opérations d’administration.</span><span class="sxs-lookup"><span data-stu-id="71b65-162">Cannot remove hello resource or perform admin operations.</span></span>
* <span data-ttu-id="71b65-163">**Opérateur d’application logique** : peut afficher l’application logique de hello et l’historique d’exécution et activer ou désactiver.</span><span class="sxs-lookup"><span data-stu-id="71b65-163">**Logic App Operator** - Can view hello logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="71b65-164">Impossible de modifier ou de mettre à jour de définition de hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-164">Cannot edit or update hello definition.</span></span>

<span data-ttu-id="71b65-165">Vous pouvez également utiliser [verrou de ressource Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changement ou suppression d’applications de la logique.</span><span class="sxs-lookup"><span data-stu-id="71b65-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changing or deleting logic apps.</span></span> <span data-ttu-id="71b65-166">Cette fonctionnalité est tooprevent précieuses ressources de production à partir de la modification ou suppression.</span><span class="sxs-lookup"><span data-stu-id="71b65-166">This capability is valuable tooprevent production resources from changes or deletions.</span></span>

## <a name="secure-access-toocontents-of-hello-run-history"></a><span data-ttu-id="71b65-167">Toocontents de sécuriser l’accès de l’historique d’exécution de hello</span><span class="sxs-lookup"><span data-stu-id="71b65-167">Secure access toocontents of hello run history</span></span>

<span data-ttu-id="71b65-168">Vous pouvez limiter toocontents d’accès de l’entrée ni sortie à partir de précédentes plages d’adresses IP toospecific s’exécute.</span><span class="sxs-lookup"><span data-stu-id="71b65-168">You can restrict access toocontents of inputs or outputs from previous runs toospecific IP address ranges.</span></span>  

<span data-ttu-id="71b65-169">Toutes les données de l’exécution d’un flux de travail sont chiffrées pendant le transit et au repos.</span><span class="sxs-lookup"><span data-stu-id="71b65-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="71b65-170">Lors de l’appel toorun historique, service de hello authentifie hello demande et fournit des liens toohello demande et les entrées de la réponse et les sorties.</span><span class="sxs-lookup"><span data-stu-id="71b65-170">When a call toorun history is made, hello service authenticates hello request and provides links toohello request and response inputs and outputs.</span></span> <span data-ttu-id="71b65-171">Ce lien peut être protégé par conséquent, seules les demandes tooview le contenu à partir d’une plage d’adresses IP désigné retourner le contenu de hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-171">This link can be protected so only requests tooview content from a designated IP address range return hello contents.</span></span> <span data-ttu-id="71b65-172">Vous pouvez utiliser cette fonctionnalité pour obtenir un contrôle d’accès supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="71b65-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="71b65-173">Vous pouvez également spécifier une adresse IP telle que `0.0.0.0` afin que personne ne puisse accéder aux entrées/sorties.</span><span class="sxs-lookup"><span data-stu-id="71b65-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="71b65-174">Seule une personne disposant d’autorisations d’administrateur a supprimer cette restriction, en fournissant la possibilité de hello pour le contenu tooworkflow d’accès de « juste-à-temps ».</span><span class="sxs-lookup"><span data-stu-id="71b65-174">Only someone with admin permissions could remove this restriction, providing hello possibility for 'just-in-time' access tooworkflow contents.</span></span>

<span data-ttu-id="71b65-175">Ce paramètre peut être configuré dans les paramètres de ressource hello Hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="71b65-175">This setting can be configured within hello resource settings of hello Azure portal:</span></span>

1. <span data-ttu-id="71b65-176">Bonjour portail Azure, ouvrez hello logique application tooadd restrictions par adresse IP</span><span class="sxs-lookup"><span data-stu-id="71b65-176">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="71b65-177">Cliquez sur hello **configuration de contrôle d’accès** élément de menu sous **paramètres**</span><span class="sxs-lookup"><span data-stu-id="71b65-177">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="71b65-178">Spécifiez la liste hello de plages d’adresses IP pour un accès toocontent</span><span class="sxs-lookup"><span data-stu-id="71b65-178">Specify hello list of IP address ranges for access toocontent</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="71b65-179">Définition de plages d’adresses IP sur la définition de ressource hello</span><span class="sxs-lookup"><span data-stu-id="71b65-179">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="71b65-180">Si vous utilisez un [modèle de déploiement](logic-apps-create-deploy-template.md) tooautomate vos déploiements, les paramètres des plages IP hello peuvent être configurés sur le modèle de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

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

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="71b65-181">Sécuriser les paramètres et les entrées dans un flux de travail</span><span class="sxs-lookup"><span data-stu-id="71b65-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="71b65-182">Vous pourriez tooparameterize certains aspects d’une définition de flux de travail pour le déploiement dans des environnements.</span><span class="sxs-lookup"><span data-stu-id="71b65-182">You might want tooparameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="71b65-183">En outre, certains paramètres peuvent être des paramètres sécurisés, vous ne souhaitez pas tooappear lors de la modification d’un flux de travail, telles qu’un ID client et la clé secrète du client pour [l’authentification Azure Active Directory](../connectors/connectors-native-http.md#authentication) d’une action HTTP.</span><span class="sxs-lookup"><span data-stu-id="71b65-183">Also, some parameters might be secure parameters you don't want tooappear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="71b65-184">Utilisation des paramètres et des paramètres sécurisés</span><span class="sxs-lookup"><span data-stu-id="71b65-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="71b65-185">hello tooaccess hello valeur d’un paramètre de ressource lors de l’exécution, [langage de définition de flux de travail](http://aka.ms/logicappsdocs) fournit une `@parameters()` opération.</span><span class="sxs-lookup"><span data-stu-id="71b65-185">tooaccess hello value of a resource parameter at runtime, hello [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="71b65-186">En outre, vous pouvez [spécifier les paramètres de modèle de déploiement de ressources hello](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="71b65-186">Also, you can [specify parameters in hello resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="71b65-187">Mais si vous spécifiez le type de paramètre hello en tant que `securestring`, paramètre hello ne sera pas renvoyée avec rest hello de définition de ressource hello et ne seront pas accessible en consultant les ressources hello après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="71b65-187">But if you specify hello parameter type as `securestring`, hello parameter won't be returned with hello rest of hello resource definition, and won't be accessible by viewing hello resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="71b65-188">Si votre paramètre est utilisé dans les en-têtes de hello ou de corps d’une requête, le paramètre hello peut être visible en accédant à l’historique de hello exécuter et de la demande HTTP sortante.</span><span class="sxs-lookup"><span data-stu-id="71b65-188">If your parameter is used in hello headers or body of a request, hello parameter might be visible by accessing hello run history and outgoing HTTP request.</span></span> <span data-ttu-id="71b65-189">Assurez-vous que tooset vos stratégies d’accès au contenu en conséquence.</span><span class="sxs-lookup"><span data-stu-id="71b65-189">Make sure tooset your content access policies accordingly.</span></span>
> <span data-ttu-id="71b65-190">Les en-têtes d’autorisation ne sont jamais visibles par le biais d’entrées ou de sorties.</span><span class="sxs-lookup"><span data-stu-id="71b65-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="71b65-191">Par conséquent, si le secret de hello il est utilisé, secret de hello n’est pas récupérable.</span><span class="sxs-lookup"><span data-stu-id="71b65-191">So if hello secret is being used there, hello secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="71b65-192">Modèle de déploiement de ressource avec des clés secrètes</span><span class="sxs-lookup"><span data-stu-id="71b65-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="71b65-193">Hello suivant montre un déploiement qui fait référence à un paramètre sécurisé de `secret` lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="71b65-193">hello following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="71b65-194">Dans un fichier de paramètres distincts, vous pouvez spécifier la valeur d’environnement hello pour hello `secret`, ou utilisez [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) secrets tooretrieve au niveau du déploiement.</span><span class="sxs-lookup"><span data-stu-id="71b65-194">In a separate parameters file, you could specify hello environment value for hello `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secrets at deploy time.</span></span>

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
                "body": "This is hello request"
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

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a><span data-ttu-id="71b65-195">Sécuriser l’accès aux demandes de réception tooservices à partir d’un flux de travail</span><span class="sxs-lookup"><span data-stu-id="71b65-195">Secure access tooservices receiving requests from a workflow</span></span>

<span data-ttu-id="71b65-196">Il existe de nombreuses façons toohelp sécurisé que tooaccess a besoin de n’importe quelle application de la logique de point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-196">There are many ways toohelp secure any endpoint hello logic app needs tooaccess.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="71b65-197">Utilisation de l’authentification sur les requêtes sortantes</span><span class="sxs-lookup"><span data-stu-id="71b65-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="71b65-198">Lorsque vous travaillez avec un HTTP, HTTP + Swagger (API Open) ou l’opération de Webhook, vous pouvez ajouter l’authentification toohello envoyé.</span><span class="sxs-lookup"><span data-stu-id="71b65-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication toohello request being sent.</span></span> <span data-ttu-id="71b65-199">Vous pouvez inclure l’authentification de base, l’authentification par certificat ou l’authentification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71b65-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="71b65-200">Plus d’informations sur comment tooconfigure cette authentification peut être détectée [dans cet article](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="71b65-200">Details on how tooconfigure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-toologic-app-ip-addresses"></a><span data-ttu-id="71b65-201">Limitation des adresses IP de l’accès toologic application</span><span class="sxs-lookup"><span data-stu-id="71b65-201">Restricting access toologic app IP addresses</span></span>

<span data-ttu-id="71b65-202">Tous les appels d’applications logiques proviennent d’un ensemble spécifique d’adresses IP par région.</span><span class="sxs-lookup"><span data-stu-id="71b65-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="71b65-203">Vous pouvez ajouter un filtrage supplémentaire tooonly accepter les demandes de celles désigné des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="71b65-203">You can add additional filtering tooonly accept requests from those designated IP addresses.</span></span> <span data-ttu-id="71b65-204">Pour obtenir la liste de ces adresses IP, consultez [Limites et configuration des applications logiques](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="71b65-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="71b65-205">Connectivité locale</span><span class="sxs-lookup"><span data-stu-id="71b65-205">On-premises connectivity</span></span>

<span data-ttu-id="71b65-206">Logique applications fournissent l’intégration avec plusieurs services tooprovide, sécurisée et fiable local communication.</span><span class="sxs-lookup"><span data-stu-id="71b65-206">Logic apps provide integration with several services tooprovide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="71b65-207">Passerelle de données locale</span><span class="sxs-lookup"><span data-stu-id="71b65-207">On-premises data gateway</span></span>

<span data-ttu-id="71b65-208">Plusieurs connecteurs gérés pour les applications de la logique fournissent une connectivité sécurisée des systèmes de site tooon, y compris le système de fichiers, SQL, SharePoint, DB2 et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="71b65-208">Many managed connectors for logic apps provide secure connectivity tooon-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="71b65-209">passerelle de Hello transmet des données à partir de sources locales sur des canaux chiffrés via hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="71b65-209">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="71b65-210">Tout le trafic provient sécurisé trafic sortant à partir de l’agent de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="71b65-210">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="71b65-211">En savoir plus sur [le fonctionnement de la passerelle de données hello](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="71b65-211">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="71b65-212">Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="71b65-212">Azure API Management</span></span>

<span data-ttu-id="71b65-213">[Gestion des API Azure](https://azure.microsoft.com/services/api-management/) a des options de connectivité locale, y compris l’intégration de site à site VPN et ExpressRoute pour les systèmes de site tooon proxy et la communication sécurisées.</span><span class="sxs-lookup"><span data-stu-id="71b65-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication tooon-premises systems.</span></span> <span data-ttu-id="71b65-214">Dans le Concepteur d’application logique de hello, vous pouvez sélectionner rapidement une API exposée à partir de la gestion des API Azure dans un flux de travail, les systèmes de site tooon fournissent un accès rapide.</span><span class="sxs-lookup"><span data-stu-id="71b65-214">In hello Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access tooon-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="71b65-215">Connexions hybrides à partir des services d’application Azure</span><span class="sxs-lookup"><span data-stu-id="71b65-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="71b65-216">Vous pouvez utiliser la fonctionnalité de connexion hybride hello local pour API Azure et Web apps toocommunicate local.</span><span class="sxs-lookup"><span data-stu-id="71b65-216">You can use hello on-premises hybrid connection feature for Azure API and Web apps toocommunicate on-premises.</span></span>  <span data-ttu-id="71b65-217">Plus d’informations sur les connexions hybrides et comment vous pouvez trouver tooconfigure [dans cet article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="71b65-217">Details on hybrid connections and how tooconfigure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="71b65-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71b65-218">Next steps</span></span>
[<span data-ttu-id="71b65-219">Créer un modèle de déploiement</span><span class="sxs-lookup"><span data-stu-id="71b65-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="71b65-220">Gestion des exceptions</span><span class="sxs-lookup"><span data-stu-id="71b65-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="71b65-221">Analyser vos applications logiques</span><span class="sxs-lookup"><span data-stu-id="71b65-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="71b65-222">Diagnostic des échecs et problèmes d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="71b65-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
