---
title: "Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique. | Microsoft Docs"
description: "Découvrez comment utiliser des actions de mise à l’échelle automatique pour appeler des URL web ou envoyer des notifications par courrier électronique dans Azure Monitor. "
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
ms.openlocfilehash: 16caf14028494800e9259f0296c292b606d0210a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="cef6f-104">Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Moonitor</span><span class="sxs-lookup"><span data-stu-id="cef6f-104">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="cef6f-105">Cet article explique comment paramétrer des déclencheurs pour vous permettre d’appeler des URL web spécifiques ou d’envoyer des courriers électroniques en fonction d’actions de mise à l’échelle automatique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cef6f-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="cef6f-106">Webhooks</span><span class="sxs-lookup"><span data-stu-id="cef6f-106">Webhooks</span></span>
<span data-ttu-id="cef6f-107">Les webhooks vous permettent d’acheminer les notifications d’alerte Azure vers d’autres systèmes afin qu’elles soient post-traitées ou personnalisées.</span><span class="sxs-lookup"><span data-stu-id="cef6f-107">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span></span> <span data-ttu-id="cef6f-108">À titre d’exemple, citons l’acheminement de l’alerte vers des services qui peuvent gérer une demande web entrante pour envoyer des SMS, consigner des bogues, informer une équipe par le biais de services de conversation ou de messagerie, etc. L’URI du webhook doit être un point de terminaison HTTP ou HTTPS valide.</span><span class="sxs-lookup"><span data-stu-id="cef6f-108">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="cef6f-109">Email</span><span class="sxs-lookup"><span data-stu-id="cef6f-109">Email</span></span>
<span data-ttu-id="cef6f-110">Un courrier électronique peut être envoyé à n’importe quelle adresse électronique valide.</span><span class="sxs-lookup"><span data-stu-id="cef6f-110">Email can be sent to any valid email address.</span></span> <span data-ttu-id="cef6f-111">Les administrateurs et les coadministrateurs de l’abonnement dans lequel la règle est exécutée seront également avertis.</span><span class="sxs-lookup"><span data-stu-id="cef6f-111">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="cef6f-112">Services cloud et applications web</span><span class="sxs-lookup"><span data-stu-id="cef6f-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="cef6f-113">Vous pouvez l’activer depuis le portail Azure pour les services cloud et les batteries de serveurs (applications web).</span><span class="sxs-lookup"><span data-stu-id="cef6f-113">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="cef6f-114">Choisissez la métrique **scale by (mise à l’échelle par)** .</span><span class="sxs-lookup"><span data-stu-id="cef6f-114">Choose the **scale by** metric.</span></span>

![scale by (mise à l’échelle par)](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="cef6f-116">Jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cef6f-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="cef6f-117">Pour des machines virtuelles plus récentes créées avec Resource Manager (groupes identiques de machines virtuelles), vous pouvez effectuer cette configuration à l’aide de l’API REST, de modèles Resource Manager, de PowerShell et de l’interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="cef6f-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="cef6f-118">Aucune interface de portail n’est disponible pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="cef6f-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="cef6f-119">Lorsque vous utilisez l’API REST ou le modèle Resource Manager, incluez l’élément de notifications avec les options suivantes.</span><span class="sxs-lookup"><span data-stu-id="cef6f-119">When using the REST API or Resource Manager template, include the notifications element with the following options.</span></span>

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
| <span data-ttu-id="cef6f-120">Champ</span><span class="sxs-lookup"><span data-stu-id="cef6f-120">Field</span></span> | <span data-ttu-id="cef6f-121">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="cef6f-121">Mandatory?</span></span> | <span data-ttu-id="cef6f-122">Description</span><span class="sxs-lookup"><span data-stu-id="cef6f-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cef6f-123">operation</span><span class="sxs-lookup"><span data-stu-id="cef6f-123">operation</span></span> |<span data-ttu-id="cef6f-124">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-124">yes</span></span> |<span data-ttu-id="cef6f-125">la valeur doit être « Scale »</span><span class="sxs-lookup"><span data-stu-id="cef6f-125">value must be "Scale"</span></span> |
| <span data-ttu-id="cef6f-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="cef6f-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="cef6f-127">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-127">yes</span></span> |<span data-ttu-id="cef6f-128">la valeur doit être « true » ou « false »</span><span class="sxs-lookup"><span data-stu-id="cef6f-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="cef6f-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="cef6f-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="cef6f-130">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-130">yes</span></span> |<span data-ttu-id="cef6f-131">la valeur doit être « true » ou « false »</span><span class="sxs-lookup"><span data-stu-id="cef6f-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="cef6f-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="cef6f-132">customEmails</span></span> |<span data-ttu-id="cef6f-133">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-133">yes</span></span> |<span data-ttu-id="cef6f-134">la valeur peut être null ou un tableau de chaînes d’e-mails</span><span class="sxs-lookup"><span data-stu-id="cef6f-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="cef6f-135">Webhooks</span><span class="sxs-lookup"><span data-stu-id="cef6f-135">webhooks</span></span> |<span data-ttu-id="cef6f-136">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-136">yes</span></span> |<span data-ttu-id="cef6f-137">la valeur peut être null ou un Uri valide</span><span class="sxs-lookup"><span data-stu-id="cef6f-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="cef6f-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="cef6f-138">serviceUri</span></span> |<span data-ttu-id="cef6f-139">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-139">yes</span></span> |<span data-ttu-id="cef6f-140">un URI https valide</span><span class="sxs-lookup"><span data-stu-id="cef6f-140">a valid https Uri</span></span> |
| <span data-ttu-id="cef6f-141">properties</span><span class="sxs-lookup"><span data-stu-id="cef6f-141">properties</span></span> |<span data-ttu-id="cef6f-142">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-142">yes</span></span> |<span data-ttu-id="cef6f-143">la valeur doit être vide ( {} ) ou peut contenir des paires clé-valeur</span><span class="sxs-lookup"><span data-stu-id="cef6f-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="cef6f-144">Authentification dans des webhooks</span><span class="sxs-lookup"><span data-stu-id="cef6f-144">Authentication in webhooks</span></span>
<span data-ttu-id="cef6f-145">Le webhook peut s’authentifier en utilisant l’authentification par jeton, où vous enregistrez l’URI du webhook avec un ID de jeton comme paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="cef6f-145">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="cef6f-146">Par exemple, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="cef6f-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="cef6f-147">Schéma de la charge utile du webhook de notification de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="cef6f-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="cef6f-148">Lorsque la notification de mise à l’échelle automatique est générée, les métadonnées suivantes sont incluses dans la charge utile du webhook :</span><span class="sxs-lookup"><span data-stu-id="cef6f-148">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' to capacity '2'",
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


| <span data-ttu-id="cef6f-149">Champ</span><span class="sxs-lookup"><span data-stu-id="cef6f-149">Field</span></span> | <span data-ttu-id="cef6f-150">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="cef6f-150">Mandatory?</span></span> | <span data-ttu-id="cef6f-151">Description</span><span class="sxs-lookup"><span data-stu-id="cef6f-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cef6f-152">status</span><span class="sxs-lookup"><span data-stu-id="cef6f-152">status</span></span> |<span data-ttu-id="cef6f-153">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-153">yes</span></span> |<span data-ttu-id="cef6f-154">L’état qui indique qu’une action de mise à l’échelle automatique a été générée.</span><span class="sxs-lookup"><span data-stu-id="cef6f-154">The status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="cef6f-155">operation</span><span class="sxs-lookup"><span data-stu-id="cef6f-155">operation</span></span> |<span data-ttu-id="cef6f-156">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-156">yes</span></span> |<span data-ttu-id="cef6f-157">Pour une augmentation des instances, l’option est « augmenter la taille des instances » ; pour une diminution des instances, l’option est « Diminuer la taille des instances »</span><span class="sxs-lookup"><span data-stu-id="cef6f-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="cef6f-158">context</span><span class="sxs-lookup"><span data-stu-id="cef6f-158">context</span></span> |<span data-ttu-id="cef6f-159">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-159">yes</span></span> |<span data-ttu-id="cef6f-160">Le contexte de l’action de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="cef6f-160">The autoscale action context</span></span> |
| <span data-ttu-id="cef6f-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="cef6f-161">timestamp</span></span> |<span data-ttu-id="cef6f-162">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-162">yes</span></span> |<span data-ttu-id="cef6f-163">Horodatage du déclenchement de l’action de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="cef6f-163">Time stamp when the autoscale action was triggered</span></span> |
| <span data-ttu-id="cef6f-164">id</span><span class="sxs-lookup"><span data-stu-id="cef6f-164">id</span></span> |<span data-ttu-id="cef6f-165">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-165">Yes</span></span> |<span data-ttu-id="cef6f-166">ID Resource Manager du paramètre de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="cef6f-166">Resource Manager ID of the autoscale setting</span></span> |
| <span data-ttu-id="cef6f-167">name</span><span class="sxs-lookup"><span data-stu-id="cef6f-167">name</span></span> |<span data-ttu-id="cef6f-168">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-168">Yes</span></span> |<span data-ttu-id="cef6f-169">Le nom du paramètre de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="cef6f-169">The name of the autoscale setting</span></span> |
| <span data-ttu-id="cef6f-170">détails</span><span class="sxs-lookup"><span data-stu-id="cef6f-170">details</span></span> |<span data-ttu-id="cef6f-171">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-171">Yes</span></span> |<span data-ttu-id="cef6f-172">Explication de l’action exécutée par le service de mise à l’échelle automatique et de la modification du nombre d’instances</span><span class="sxs-lookup"><span data-stu-id="cef6f-172">Explanation of the action that the autoscale service took and the change in the instance count</span></span> |
| <span data-ttu-id="cef6f-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="cef6f-173">subscriptionId</span></span> |<span data-ttu-id="cef6f-174">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-174">Yes</span></span> |<span data-ttu-id="cef6f-175">ID d’abonnement de la ressource cible mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="cef6f-175">Subscription ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="cef6f-176">nom_groupe_ressources</span><span class="sxs-lookup"><span data-stu-id="cef6f-176">resourceGroupName</span></span> |<span data-ttu-id="cef6f-177">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-177">Yes</span></span> |<span data-ttu-id="cef6f-178">Nom de groupe de ressources de la ressource cible mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="cef6f-178">Resource Group name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="cef6f-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="cef6f-179">resourceName</span></span> |<span data-ttu-id="cef6f-180">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-180">Yes</span></span> |<span data-ttu-id="cef6f-181">Nom de la ressource cible mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="cef6f-181">Name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="cef6f-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="cef6f-182">resourceType</span></span> |<span data-ttu-id="cef6f-183">Oui</span><span class="sxs-lookup"><span data-stu-id="cef6f-183">Yes</span></span> |<span data-ttu-id="cef6f-184">Trois valeurs sont prises en charge : « microsoft.classiccompute/domainnames/slots/roles » - Rôles de service cloud, « microsoft.compute/virtualmachinescalesets » - Jeux de mise à l’échelle de machine virtuelle et « Microsoft.Web/serverfarms » - Application Web</span><span class="sxs-lookup"><span data-stu-id="cef6f-184">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="cef6f-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="cef6f-185">resourceId</span></span> |<span data-ttu-id="cef6f-186">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-186">Yes</span></span> |<span data-ttu-id="cef6f-187">ID Resource Manager de la ressource cible mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="cef6f-187">Resource Manager ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="cef6f-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="cef6f-188">portalLink</span></span> |<span data-ttu-id="cef6f-189">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-189">Yes</span></span> |<span data-ttu-id="cef6f-190">Lien du portail Azure vers la page de résumé de la ressource cible</span><span class="sxs-lookup"><span data-stu-id="cef6f-190">Azure portal link to the summary page of the target resource</span></span> |
| <span data-ttu-id="cef6f-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="cef6f-191">oldCapacity</span></span> |<span data-ttu-id="cef6f-192">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-192">Yes</span></span> |<span data-ttu-id="cef6f-193">Nombre d’instances (anciennes) actuel lors de l’exécution d’une action de mise à l’échelle par la mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="cef6f-193">The current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="cef6f-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="cef6f-194">newCapacity</span></span> |<span data-ttu-id="cef6f-195">yes</span><span class="sxs-lookup"><span data-stu-id="cef6f-195">Yes</span></span> |<span data-ttu-id="cef6f-196">Le nouveau nombre d’instances auquel la mise à l’échelle automatique a mis la ressource à l’échelle</span><span class="sxs-lookup"><span data-stu-id="cef6f-196">The new instance count that Autoscale scaled the resource to</span></span> |
| <span data-ttu-id="cef6f-197">properties</span><span class="sxs-lookup"><span data-stu-id="cef6f-197">Properties</span></span> |<span data-ttu-id="cef6f-198">Non</span><span class="sxs-lookup"><span data-stu-id="cef6f-198">No</span></span> |<span data-ttu-id="cef6f-199">facultatif.</span><span class="sxs-lookup"><span data-stu-id="cef6f-199">Optional.</span></span> <span data-ttu-id="cef6f-200">Jeu de paires < clé, valeur > (par exemple, Dictionary < String, String >).</span><span class="sxs-lookup"><span data-stu-id="cef6f-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="cef6f-201">Le champ properties est facultatif.</span><span class="sxs-lookup"><span data-stu-id="cef6f-201">The properties field is optional.</span></span> <span data-ttu-id="cef6f-202">Dans un flux de travail basé sur une application logique ou une interface utilisateur personnalisée, vous pouvez entrer des clés et des valeurs transmissibles par le biais de la charge utile.</span><span class="sxs-lookup"><span data-stu-id="cef6f-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span></span> <span data-ttu-id="cef6f-203">Une autre manière de transmettre des propriétés personnalisées au webhook sortant consiste à utiliser l’URI du webhook (sous la forme de paramètres de requête).</span><span class="sxs-lookup"><span data-stu-id="cef6f-203">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span></span> |
