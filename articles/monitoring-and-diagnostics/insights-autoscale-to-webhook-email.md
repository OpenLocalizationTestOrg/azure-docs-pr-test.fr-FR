---
title: "notifications d’alerte par courrier électronique d’aaaUse échelle actions toosend et webhook. | Microsoft Docs"
description: "Consultez Comment toouse échelle actions toocall web URL ou envoyer des notifications par courrier électronique dans le moniteur de Azure. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="04d39-104">Utiliser la mise à l’échelle actions toosend par courrier électronique et webhook des notifications d’alerte dans le moniteur de Azure</span><span class="sxs-lookup"><span data-stu-id="04d39-104">Use autoscale actions toosend email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="04d39-105">Cet article explique comment paramétrer des déclencheurs pour vous permettre d’appeler des URL web spécifiques ou d’envoyer des courriers électroniques en fonction d’actions de mise à l’échelle automatique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="04d39-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="04d39-106">Webhooks</span><span class="sxs-lookup"><span data-stu-id="04d39-106">Webhooks</span></span>
<span data-ttu-id="04d39-107">Webhooks permettent de systèmes de tooother tooroute hello Azure notifications d’alerte pour les notifications de post-traitement ou personnalisées.</span><span class="sxs-lookup"><span data-stu-id="04d39-107">Webhooks allow you tooroute hello Azure alert notifications tooother systems for post-processing or custom notifications.</span></span> <span data-ttu-id="04d39-108">Par exemple, routage tooservices alerte hello qui peut gérer un entrant web demande toosend SMS, journal des bogues, notifier une équipe à l’aide de la conversation ou de services de messagerie, etc. hello webhook URI doit être un point de terminaison HTTP ou HTTPS valide.</span><span class="sxs-lookup"><span data-stu-id="04d39-108">For example, routing hello alert tooservices that can handle an incoming web request toosend SMS, log bugs, notify a team using chat or messaging services, etc. hello webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="04d39-109">Email</span><span class="sxs-lookup"><span data-stu-id="04d39-109">Email</span></span>
<span data-ttu-id="04d39-110">Adresse de messagerie valide tooany peut être envoyé à par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="04d39-110">Email can be sent tooany valid email address.</span></span> <span data-ttu-id="04d39-111">Les administrateurs et coadministrateurs d’abonnement hello sur lequel la règle de hello s’exécute également soient prévenus.</span><span class="sxs-lookup"><span data-stu-id="04d39-111">Administrators and co-administrators of hello subscription where hello rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="04d39-112">Services cloud et applications web</span><span class="sxs-lookup"><span data-stu-id="04d39-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="04d39-113">Vous pouvez choisir de hello portail Azure pour les Services de cloud computing et des batteries de serveurs (applications Web).</span><span class="sxs-lookup"><span data-stu-id="04d39-113">You can opt-in from hello Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="04d39-114">Choisissez hello **l’échelle** métrique.</span><span class="sxs-lookup"><span data-stu-id="04d39-114">Choose hello **scale by** metric.</span></span>

![scale by (mise à l’échelle par)](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="04d39-116">Jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="04d39-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="04d39-117">Pour des machines virtuelles plus récentes créées avec Resource Manager (groupes identiques de machines virtuelles), vous pouvez effectuer cette configuration à l’aide de l’API REST, de modèles Resource Manager, de PowerShell et de l’interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="04d39-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="04d39-118">Aucune interface de portail n’est disponible pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="04d39-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="04d39-119">Lorsque vous utilisez l’API REST de hello ou un modèle de gestionnaire de ressources, inclure l’élément de notifications de hello avec hello options suivantes.</span><span class="sxs-lookup"><span data-stu-id="04d39-119">When using hello REST API or Resource Manager template, include hello notifications element with hello following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| <span data-ttu-id="04d39-120">Champ</span><span class="sxs-lookup"><span data-stu-id="04d39-120">Field</span></span> | <span data-ttu-id="04d39-121">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="04d39-121">Mandatory?</span></span> | <span data-ttu-id="04d39-122">Description</span><span class="sxs-lookup"><span data-stu-id="04d39-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04d39-123">operation</span><span class="sxs-lookup"><span data-stu-id="04d39-123">operation</span></span> |<span data-ttu-id="04d39-124">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-124">yes</span></span> |<span data-ttu-id="04d39-125">la valeur doit être « Scale »</span><span class="sxs-lookup"><span data-stu-id="04d39-125">value must be "Scale"</span></span> |
| <span data-ttu-id="04d39-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="04d39-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="04d39-127">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-127">yes</span></span> |<span data-ttu-id="04d39-128">la valeur doit être « true » ou « false »</span><span class="sxs-lookup"><span data-stu-id="04d39-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="04d39-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="04d39-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="04d39-130">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-130">yes</span></span> |<span data-ttu-id="04d39-131">la valeur doit être « true » ou « false »</span><span class="sxs-lookup"><span data-stu-id="04d39-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="04d39-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="04d39-132">customEmails</span></span> |<span data-ttu-id="04d39-133">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-133">yes</span></span> |<span data-ttu-id="04d39-134">la valeur peut être null ou un tableau de chaînes d’e-mails</span><span class="sxs-lookup"><span data-stu-id="04d39-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="04d39-135">Webhooks</span><span class="sxs-lookup"><span data-stu-id="04d39-135">webhooks</span></span> |<span data-ttu-id="04d39-136">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-136">yes</span></span> |<span data-ttu-id="04d39-137">la valeur peut être null ou un Uri valide</span><span class="sxs-lookup"><span data-stu-id="04d39-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="04d39-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="04d39-138">serviceUri</span></span> |<span data-ttu-id="04d39-139">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-139">yes</span></span> |<span data-ttu-id="04d39-140">un URI https valide</span><span class="sxs-lookup"><span data-stu-id="04d39-140">a valid https Uri</span></span> |
| <span data-ttu-id="04d39-141">properties</span><span class="sxs-lookup"><span data-stu-id="04d39-141">properties</span></span> |<span data-ttu-id="04d39-142">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-142">yes</span></span> |<span data-ttu-id="04d39-143">la valeur doit être vide ( {} ) ou peut contenir des paires clé-valeur</span><span class="sxs-lookup"><span data-stu-id="04d39-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="04d39-144">Authentification dans des webhooks</span><span class="sxs-lookup"><span data-stu-id="04d39-144">Authentication in webhooks</span></span>
<span data-ttu-id="04d39-145">Hello webhook peut s’authentifier à l’aide de l’authentification basée sur le jeton, où vous enregistrez hello webhook URI avec un ID de jeton en tant que paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="04d39-145">hello webhook can authenticate using token-based authentication, where you save hello webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="04d39-146">Par exemple, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="04d39-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="04d39-147">Schéma de la charge utile du webhook de notification de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="04d39-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="04d39-148">Lors de la notification de mise à l’échelle hello est générée, hello métadonnées suivante sont incluses dans la charge utile du webhook hello :</span><span class="sxs-lookup"><span data-stu-id="04d39-148">When hello autoscale notification is generated, hello following metadata is included in hello webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="04d39-149">Champ</span><span class="sxs-lookup"><span data-stu-id="04d39-149">Field</span></span> | <span data-ttu-id="04d39-150">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="04d39-150">Mandatory?</span></span> | <span data-ttu-id="04d39-151">Description</span><span class="sxs-lookup"><span data-stu-id="04d39-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04d39-152">status</span><span class="sxs-lookup"><span data-stu-id="04d39-152">status</span></span> |<span data-ttu-id="04d39-153">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-153">yes</span></span> |<span data-ttu-id="04d39-154">état Hello qui indique qu’une action de mise à l’échelle a été générée.</span><span class="sxs-lookup"><span data-stu-id="04d39-154">hello status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="04d39-155">operation</span><span class="sxs-lookup"><span data-stu-id="04d39-155">operation</span></span> |<span data-ttu-id="04d39-156">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-156">yes</span></span> |<span data-ttu-id="04d39-157">Pour une augmentation des instances, l’option est « augmenter la taille des instances » ; pour une diminution des instances, l’option est « Diminuer la taille des instances »</span><span class="sxs-lookup"><span data-stu-id="04d39-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="04d39-158">context</span><span class="sxs-lookup"><span data-stu-id="04d39-158">context</span></span> |<span data-ttu-id="04d39-159">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-159">yes</span></span> |<span data-ttu-id="04d39-160">contexte d’action de mise à l’échelle de Hello</span><span class="sxs-lookup"><span data-stu-id="04d39-160">hello autoscale action context</span></span> |
| <span data-ttu-id="04d39-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="04d39-161">timestamp</span></span> |<span data-ttu-id="04d39-162">yes</span><span class="sxs-lookup"><span data-stu-id="04d39-162">yes</span></span> |<span data-ttu-id="04d39-163">Horodatage lors de l’action de mise à l’échelle hello a été déclenchée.</span><span class="sxs-lookup"><span data-stu-id="04d39-163">Time stamp when hello autoscale action was triggered</span></span> |
| <span data-ttu-id="04d39-164">id</span><span class="sxs-lookup"><span data-stu-id="04d39-164">id</span></span> |<span data-ttu-id="04d39-165">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-165">Yes</span></span> |<span data-ttu-id="04d39-166">ID du Gestionnaire de ressources du paramètre de mise à l’échelle hello</span><span class="sxs-lookup"><span data-stu-id="04d39-166">Resource Manager ID of hello autoscale setting</span></span> |
| <span data-ttu-id="04d39-167">name</span><span class="sxs-lookup"><span data-stu-id="04d39-167">name</span></span> |<span data-ttu-id="04d39-168">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-168">Yes</span></span> |<span data-ttu-id="04d39-169">nom de Hello du paramètre de mise à l’échelle hello</span><span class="sxs-lookup"><span data-stu-id="04d39-169">hello name of hello autoscale setting</span></span> |
| <span data-ttu-id="04d39-170">détails</span><span class="sxs-lookup"><span data-stu-id="04d39-170">details</span></span> |<span data-ttu-id="04d39-171">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-171">Yes</span></span> |<span data-ttu-id="04d39-172">Explication de l’action hello que nécessaire du service de mise à l’échelle hello et hello modifier dans le nombre d’instances hello</span><span class="sxs-lookup"><span data-stu-id="04d39-172">Explanation of hello action that hello autoscale service took and hello change in hello instance count</span></span> |
| <span data-ttu-id="04d39-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="04d39-173">subscriptionId</span></span> |<span data-ttu-id="04d39-174">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-174">Yes</span></span> |<span data-ttu-id="04d39-175">ID d’abonnement de la ressource cible hello qui est mis à l’échelle</span><span class="sxs-lookup"><span data-stu-id="04d39-175">Subscription ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="04d39-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="04d39-176">resourceGroupName</span></span> |<span data-ttu-id="04d39-177">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-177">Yes</span></span> |<span data-ttu-id="04d39-178">Nom de groupe de ressources de la ressource cible hello qui est mis à l’échelle</span><span class="sxs-lookup"><span data-stu-id="04d39-178">Resource Group name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="04d39-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="04d39-179">resourceName</span></span> |<span data-ttu-id="04d39-180">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-180">Yes</span></span> |<span data-ttu-id="04d39-181">Nom de ressource cible hello qui est mis à l’échelle</span><span class="sxs-lookup"><span data-stu-id="04d39-181">Name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="04d39-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="04d39-182">resourceType</span></span> |<span data-ttu-id="04d39-183">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-183">Yes</span></span> |<span data-ttu-id="04d39-184">Hello trois valeurs prises en charge : « microsoft.classiccompute/domainnames/slots/roles » - rôles de Service Cloud, « microsoft.compute/virtualmachinescalesets - « machines virtuelles identiques et « Microsoft.Web/serverfarms » - application Web</span><span class="sxs-lookup"><span data-stu-id="04d39-184">hello three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="04d39-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="04d39-185">resourceId</span></span> |<span data-ttu-id="04d39-186">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-186">Yes</span></span> |<span data-ttu-id="04d39-187">ID du Gestionnaire de ressources de ressource cible hello qui est mis à l’échelle</span><span class="sxs-lookup"><span data-stu-id="04d39-187">Resource Manager ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="04d39-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="04d39-188">portalLink</span></span> |<span data-ttu-id="04d39-189">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-189">Yes</span></span> |<span data-ttu-id="04d39-190">Page Résumé de lien vers le portail Azure toohello de ressource cible de hello</span><span class="sxs-lookup"><span data-stu-id="04d39-190">Azure portal link toohello summary page of hello target resource</span></span> |
| <span data-ttu-id="04d39-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="04d39-191">oldCapacity</span></span> |<span data-ttu-id="04d39-192">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-192">Yes</span></span> |<span data-ttu-id="04d39-193">Hello (ancienne) nombre d’instances actuelles lors de l’échelle automatique a effectué une action de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="04d39-193">hello current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="04d39-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="04d39-194">newCapacity</span></span> |<span data-ttu-id="04d39-195">Oui</span><span class="sxs-lookup"><span data-stu-id="04d39-195">Yes</span></span> |<span data-ttu-id="04d39-196">nouveau nombre d’instances Hello que mise à l’échelle à l’échelle les ressources hello trop</span><span class="sxs-lookup"><span data-stu-id="04d39-196">hello new instance count that Autoscale scaled hello resource too</span></span>|
| <span data-ttu-id="04d39-197">Propriétés</span><span class="sxs-lookup"><span data-stu-id="04d39-197">Properties</span></span> |<span data-ttu-id="04d39-198">Non</span><span class="sxs-lookup"><span data-stu-id="04d39-198">No</span></span> |<span data-ttu-id="04d39-199">facultatif.</span><span class="sxs-lookup"><span data-stu-id="04d39-199">Optional.</span></span> <span data-ttu-id="04d39-200">Jeu de paires < clé, valeur > (par exemple, Dictionary < String, String >).</span><span class="sxs-lookup"><span data-stu-id="04d39-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="04d39-201">champ de propriétés Hello est facultatif.</span><span class="sxs-lookup"><span data-stu-id="04d39-201">hello properties field is optional.</span></span> <span data-ttu-id="04d39-202">Dans une interface utilisateur personnalisée ou d’un workflow d’application en fonction de logique, vous pouvez entrer des clés et valeurs qui peuvent être passés à l’aide de la charge utile de hello.</span><span class="sxs-lookup"><span data-stu-id="04d39-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using hello payload.</span></span> <span data-ttu-id="04d39-203">Une autre manière que les propriétés personnalisées toopass sauvegarder toohello sortants webhook appel est toouse hello webhook URI elle-même (en tant que paramètres de requête)</span><span class="sxs-lookup"><span data-stu-id="04d39-203">An alternate way toopass custom properties back toohello outgoing webhook call is toouse hello webhook URI itself (as query parameters)</span></span> |
