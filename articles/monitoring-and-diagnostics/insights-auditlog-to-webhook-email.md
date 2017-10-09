---
title: "aaaCall un webhook sur les alertes du journal des activités Azure | Documents Microsoft"
description: "Services tooother itinéraire activité journal des événements pour les actions personnalisées. Par exemple envoyer des SMS, journaliser des bogues ou notifier une équipe via un service de chat/messagerie."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="a11b5-104">Appeler un webhook sur une alerte de journal d’activité Azure</span><span class="sxs-lookup"><span data-stu-id="a11b5-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="a11b5-105">Autoriser le Webhooks vous tooroute Azure pour les actions de post-traitement ou personnalisées, les systèmes de notification tooother d’alerte.</span><span class="sxs-lookup"><span data-stu-id="a11b5-105">Webhooks allow you tooroute an Azure alert notification tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="a11b5-106">Vous pouvez utiliser un webhook sur une alerte tooroute il tooservices qui envoient des SMS, enregistrer les bogues, notifier une équipe via les services de messagerie/conversation qui ou n’importe quel nombre d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="a11b5-106">You can use a webhook on an alert tooroute it tooservices that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="a11b5-107">Cet article décrit comment tooset un toobe webhook appelée quand un déclenche alerte du journal des activités Azure.</span><span class="sxs-lookup"><span data-stu-id="a11b5-107">This article describes how tooset a webhook toobe called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="a11b5-108">Il montre également le charge hello hello HTTP POST tooa webhook ressemble à.</span><span class="sxs-lookup"><span data-stu-id="a11b5-108">It also shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span> <span data-ttu-id="a11b5-109">Pour plus d’informations sur le programme d’installation hello et le schéma d’une alerte de métrique Azure, [cette page s’affiche à la place](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="a11b5-109">For information on hello setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="a11b5-110">Vous pouvez également configurer un e-mail d’alerte toosend journal d’activité lors de l’activation.</span><span class="sxs-lookup"><span data-stu-id="a11b5-110">You can also set up an Activity Log alert toosend email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="a11b5-111">Cette fonctionnalité est actuellement en version préliminaire et sera supprimée à un moment donné dans hello futures.</span><span class="sxs-lookup"><span data-stu-id="a11b5-111">This feature is currently in preview and will be removed at some point in hello future.</span></span>
>
>

<span data-ttu-id="a11b5-112">Vous pouvez configurer une alerte de journal d’activité à l’aide de hello [applets de commande PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [inter-plateformes CLI](insights-cli-samples.md#work-with-alerts), ou [API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="a11b5-112">You can set up an Activity Log alert using hello [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="a11b5-113">Actuellement, vous ne peut pas définir une à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a11b5-113">Currently, you cannot set one up using hello Azure portal.</span></span>

## <a name="authenticating-hello-webhook"></a><span data-ttu-id="a11b5-114">Authentification hello webhook</span><span class="sxs-lookup"><span data-stu-id="a11b5-114">Authenticating hello webhook</span></span>
<span data-ttu-id="a11b5-115">Hello webhook peut s’authentifier à l’aide d’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a11b5-115">hello webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="a11b5-116">**Autorisation basée sur le jeton** -hello webhook URI est enregistré avec un ID de jeton, par exemple,`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="a11b5-116">**Token-based authorization** - hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="a11b5-117">**Autorisation de base** -hello webhook URI est enregistré avec un nom d’utilisateur et un mot de passe, par exemple,`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="a11b5-117">**Basic authorization** - hello webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="a11b5-118">Schéma de la charge utile</span><span class="sxs-lookup"><span data-stu-id="a11b5-118">Payload schema</span></span>
<span data-ttu-id="a11b5-119">Hello opération POST contient hello suivant charge utile JSON et schéma pour toutes les alertes le journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="a11b5-119">hello POST operation contains hello following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="a11b5-120">Ce schéma est semblable toohello une utilisée par les alertes basées sur la mesure.</span><span class="sxs-lookup"><span data-stu-id="a11b5-120">This schema is similar toohello one used by metric-based alerts.</span></span>

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| <span data-ttu-id="a11b5-121">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="a11b5-121">Element Name</span></span> | <span data-ttu-id="a11b5-122">Description</span><span class="sxs-lookup"><span data-stu-id="a11b5-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a11b5-123">status</span><span class="sxs-lookup"><span data-stu-id="a11b5-123">status</span></span> |<span data-ttu-id="a11b5-124">Utilisé pour les alertes de métrique.</span><span class="sxs-lookup"><span data-stu-id="a11b5-124">Used for metric alerts.</span></span> <span data-ttu-id="a11b5-125">Toujours défini trop « activé » pour les alertes de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="a11b5-125">Always set too"activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="a11b5-126">context</span><span class="sxs-lookup"><span data-stu-id="a11b5-126">context</span></span> |<span data-ttu-id="a11b5-127">Contexte d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-127">Context of hello event.</span></span> |
| <span data-ttu-id="a11b5-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="a11b5-128">resourceProviderName</span></span> |<span data-ttu-id="a11b5-129">le fournisseur de ressources Hello Hello incidence sur la ressource.</span><span class="sxs-lookup"><span data-stu-id="a11b5-129">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="a11b5-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="a11b5-130">conditionType</span></span> |<span data-ttu-id="a11b5-131">Toujours défini sur « Event ».</span><span class="sxs-lookup"><span data-stu-id="a11b5-131">Always "Event."</span></span> |
| <span data-ttu-id="a11b5-132">name</span><span class="sxs-lookup"><span data-stu-id="a11b5-132">name</span></span> |<span data-ttu-id="a11b5-133">Nom de règle d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-133">Name of hello alert rule.</span></span> |
| <span data-ttu-id="a11b5-134">id</span><span class="sxs-lookup"><span data-stu-id="a11b5-134">id</span></span> |<span data-ttu-id="a11b5-135">ID de ressource d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-135">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="a11b5-136">description</span><span class="sxs-lookup"><span data-stu-id="a11b5-136">description</span></span> |<span data-ttu-id="a11b5-137">Description de l’alerte en tant qu’ensemble lors de la création d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-137">Alert description as set during creation of hello alert.</span></span> |
| <span data-ttu-id="a11b5-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="a11b5-138">subscriptionId</span></span> |<span data-ttu-id="a11b5-139">ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a11b5-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="a11b5-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="a11b5-140">timestamp</span></span> |<span data-ttu-id="a11b5-141">Heure à quels hello événement a été généré par hello service Azure qui a traité la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-141">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="a11b5-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="a11b5-142">resourceId</span></span> |<span data-ttu-id="a11b5-143">ID de ressource de hello affectées les ressources.</span><span class="sxs-lookup"><span data-stu-id="a11b5-143">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="a11b5-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="a11b5-144">resourceGroupName</span></span> |<span data-ttu-id="a11b5-145">Nom du groupe de ressources hello pour hello affectés des ressources</span><span class="sxs-lookup"><span data-stu-id="a11b5-145">Name of hello resource group for hello impacted resource</span></span> |
| <span data-ttu-id="a11b5-146">properties</span><span class="sxs-lookup"><span data-stu-id="a11b5-146">properties</span></span> |<span data-ttu-id="a11b5-147">Jeu de `<Key, Value>` paires (c'est-à-dire `Dictionary<String, String>`) qui inclut des détails sur l’événement hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="a11b5-148">event</span><span class="sxs-lookup"><span data-stu-id="a11b5-148">event</span></span> |<span data-ttu-id="a11b5-149">Élément contenant les métadonnées sur l’événement hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-149">Element containing metadata about hello event.</span></span> |
| <span data-ttu-id="a11b5-150">autorisation</span><span class="sxs-lookup"><span data-stu-id="a11b5-150">authorization</span></span> |<span data-ttu-id="a11b5-151">propriétés RBAC Hello d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-151">hello RBAC properties of hello event.</span></span> <span data-ttu-id="a11b5-152">Il s’agit généralement hello « action », « rôle » et hello « étendue ».</span><span class="sxs-lookup"><span data-stu-id="a11b5-152">These usually include hello “action”, “role” and hello “scope.”</span></span> |
| <span data-ttu-id="a11b5-153">category</span><span class="sxs-lookup"><span data-stu-id="a11b5-153">category</span></span> |<span data-ttu-id="a11b5-154">Catégorie d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-154">Category of hello event.</span></span> <span data-ttu-id="a11b5-155">Les valeurs prises en charge sont : Administrative, Alert, Security, ServiceHealth, Recommendation.</span><span class="sxs-lookup"><span data-stu-id="a11b5-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="a11b5-156">caller</span><span class="sxs-lookup"><span data-stu-id="a11b5-156">caller</span></span> |<span data-ttu-id="a11b5-157">Adresse de messagerie de l’utilisateur hello qui a effectué l’opération de hello, revendication UPN ou revendication SPN basée sur la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="a11b5-157">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="a11b5-158">Peut être null pour certains appels système.</span><span class="sxs-lookup"><span data-stu-id="a11b5-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="a11b5-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="a11b5-159">correlationId</span></span> |<span data-ttu-id="a11b5-160">Généralement un GUID au format chaîne.</span><span class="sxs-lookup"><span data-stu-id="a11b5-160">Usually a GUID in string format.</span></span> <span data-ttu-id="a11b5-161">Les événements avec l’ID de corrélation appartiennent toohello même action plus importante et partagent généralement un ID de corrélation.</span><span class="sxs-lookup"><span data-stu-id="a11b5-161">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="a11b5-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="a11b5-162">eventDescription</span></span> |<span data-ttu-id="a11b5-163">Description de texte statique de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-163">Static text description of hello event.</span></span> |
| <span data-ttu-id="a11b5-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="a11b5-164">eventDataId</span></span> |<span data-ttu-id="a11b5-165">Identificateur unique de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-165">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="a11b5-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="a11b5-166">eventSource</span></span> |<span data-ttu-id="a11b5-167">Nom de hello service Azure ou infrastructure que l’événement hello généré.</span><span class="sxs-lookup"><span data-stu-id="a11b5-167">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="a11b5-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="a11b5-168">httpRequest</span></span> |<span data-ttu-id="a11b5-169">Inclut généralement hello « clientRequestId », « clientIpAddress » et « method » (méthode HTTP PUT, par exemple).</span><span class="sxs-lookup"><span data-stu-id="a11b5-169">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="a11b5-170">level</span><span class="sxs-lookup"><span data-stu-id="a11b5-170">level</span></span> |<span data-ttu-id="a11b5-171">Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires ».</span><span class="sxs-lookup"><span data-stu-id="a11b5-171">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="a11b5-172">operationId</span><span class="sxs-lookup"><span data-stu-id="a11b5-172">operationId</span></span> |<span data-ttu-id="a11b5-173">Généralement GUID partagé entre les événements hello correspondant toosingle opération.</span><span class="sxs-lookup"><span data-stu-id="a11b5-173">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="a11b5-174">operationName</span><span class="sxs-lookup"><span data-stu-id="a11b5-174">operationName</span></span> |<span data-ttu-id="a11b5-175">Nom de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-175">Name of hello operation.</span></span> |
| <span data-ttu-id="a11b5-176">properties</span><span class="sxs-lookup"><span data-stu-id="a11b5-176">properties</span></span> |<span data-ttu-id="a11b5-177">Propriétés d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-177">Properties of hello event.</span></span> |
| <span data-ttu-id="a11b5-178">status</span><span class="sxs-lookup"><span data-stu-id="a11b5-178">status</span></span> |<span data-ttu-id="a11b5-179">Chaîne.</span><span class="sxs-lookup"><span data-stu-id="a11b5-179">String.</span></span> <span data-ttu-id="a11b5-180">État de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="a11b5-180">Status of hello operation.</span></span> <span data-ttu-id="a11b5-181">Les valeurs courantes sont : « Started », « In Progress », « Succeeded », « Failed », « Active », « Resolved ».</span><span class="sxs-lookup"><span data-stu-id="a11b5-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="a11b5-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="a11b5-182">subStatus</span></span> |<span data-ttu-id="a11b5-183">Inclut généralement le code d’état HTTP hello d’appel REST hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="a11b5-183">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="a11b5-184">Il peut également inclure d’autres chaînes décrivant un sous-état.</span><span class="sxs-lookup"><span data-stu-id="a11b5-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="a11b5-185">Les valeurs courantes sont : OK (Code d’état HTTP : 200), Created (Code d’état HTTP : 201), Accepted (Code d’état HTTP : 202), No Content (Code d’état HTTP : 204), Bad Request (Code d’état HTTP : 400), Not Found (Code d’état HTTP : 404), Conflict (Code d’état HTTP : 409), Internal Server Error (Code d’état HTTP : 500), Service Unavailable (Code d’état HTTP : 503), Gateway Timeout (Code d’état HTTP : 504).</span><span class="sxs-lookup"><span data-stu-id="a11b5-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a11b5-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a11b5-186">Next steps</span></span>
* [<span data-ttu-id="a11b5-187">En savoir plus sur hello journal d’activité</span><span class="sxs-lookup"><span data-stu-id="a11b5-187">Learn more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="a11b5-188">Exécuter des scripts Azure Automation (Runbooks) sur des alertes Azure</span><span class="sxs-lookup"><span data-stu-id="a11b5-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="a11b5-189">[Utilisez l’application logique toosend SMS via Twilio à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a11b5-189">[Use Logic App toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="a11b5-190">Cet exemple est pour les alertes de métriques, mais peut être modifiée toowork avec une alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="a11b5-190">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="a11b5-191">[Utilisez l’application logique toosend un message de marge d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a11b5-191">[Use Logic App toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="a11b5-192">Cet exemple est pour les alertes de métriques, mais peut être modifiée toowork avec une alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="a11b5-192">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="a11b5-193">[Utilisez l’application logique toosend un tooan message file d’attente Azure à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a11b5-193">[Use Logic App toosend a message tooan Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="a11b5-194">Cet exemple est pour les alertes de métriques, mais peut être modifiée toowork avec une alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="a11b5-194">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
