---
title: "Diffuser en continu le journal d’activité Azure sur les Event Hubs | Microsoft Docs"
description: "Apprenez comment diffuser en continu le journal d’activité Azure sur les Event Hubs."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 88c5701279f370914fac68872d67b02a7571748a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="stream-the-azure-activity-log-to-event-hubs"></a><span data-ttu-id="63898-103">Diffuser en continu le journal des activités Azure sur les Event Hubs</span><span class="sxs-lookup"><span data-stu-id="63898-103">Stream the Azure Activity Log to Event Hubs</span></span>
<span data-ttu-id="63898-104">Le [**journal d’activité Azure**](monitoring-overview-activity-logs.md) peut être diffusé en quasi-temps réel sur n’importe quelle application à l’aide de l’option « Export » intégrée au portail, ou en activant l’identifiant de règle Service Bus dans un profil de journal via les applets de commande PowerShell Azure ou l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="63898-104">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time to any application using the built-in “Export” option in the portal, or by enabling the Service Bus Rule Id in a Log Profile via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-the-activity-log-and-event-hubs"></a><span data-ttu-id="63898-105">Ce que vous pouvez faire avec le journal d’activité et Event Hubs</span><span class="sxs-lookup"><span data-stu-id="63898-105">What you can do with the Activity Log and Event Hubs</span></span>
<span data-ttu-id="63898-106">Voici quelques façons d’utiliser la fonctionnalité de diffusion en continu pour le journal d’activité :</span><span class="sxs-lookup"><span data-stu-id="63898-106">Here are just a few ways you might use the streaming capability for the Activity Log:</span></span>

* <span data-ttu-id="63898-107">**Diffuser en continu sur des systèmes de journalisation et de télémétrie tiers** : au fil du temps, la diffusion en continu sur Event Hubs deviendra le mécanisme de diffusion de votre journal d’activité vers les SIEM et les solutions d’analyse de journaux tiers.</span><span class="sxs-lookup"><span data-stu-id="63898-107">**Stream to third-party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="63898-108">**Créer une plateforme de journalisation et de télémétrie personnalisée** : si vous disposez déjà d’une plate-forme de télémétrie personnalisée, ou si vous envisagez d’en créer une, la nature hautement évolutive de publication et d’abonnement d’Event Hubs vous permet d’intégrer avec souplesse le journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="63898-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest the activity log.</span></span> [<span data-ttu-id="63898-109">Consultez ici le guide de Dan Rosanova sur l’utilisation d’Event Hubs dans une plate-forme de télémétrie à échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="63898-109">See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-the-activity-log"></a><span data-ttu-id="63898-110">Activer la diffusion en continu du journal d’activité</span><span class="sxs-lookup"><span data-stu-id="63898-110">Enable streaming of the Activity Log</span></span>
<span data-ttu-id="63898-111">Vous pouvez activer la diffusion en continu du journal d’activité soit par programmation, soit via le portail.</span><span class="sxs-lookup"><span data-stu-id="63898-111">You can enable streaming of the Activity Log either programmatically or via the portal.</span></span> <span data-ttu-id="63898-112">Dans les deux cas, vous choisissez un espace de noms Service Bus et une stratégie d’accès partagé pour cet espace de noms, et un Event Hub est créé dans cet espace de noms lorsque le premier nouvel événement de journal d’activité se produit.</span><span class="sxs-lookup"><span data-stu-id="63898-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when the first new Activity Log event occurs.</span></span> <span data-ttu-id="63898-113">Si vous n’avez pas d’espace de noms Service Bus, vous devez d’abord en créer un.</span><span class="sxs-lookup"><span data-stu-id="63898-113">If you do not have a Service Bus Namespace, you first need to create one.</span></span> <span data-ttu-id="63898-114">Si vous avez précédemment diffusé en continu des événements du journal d’activité vers cet espace de noms Service Bus, l’Event Hub créé précédemment sera réutilisé.</span><span class="sxs-lookup"><span data-stu-id="63898-114">If you have previously streamed Activity Log events to this Service Bus Namespace, the Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="63898-115">La stratégie d’accès partagé définit les autorisations dont dispose le mécanisme de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="63898-115">The shared access policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="63898-116">À l’heure actuelle, la diffusion vers les clients Event Hubs requiert des autorisations de **gestion**, d’**envoi** et d’**écoute**.</span><span class="sxs-lookup"><span data-stu-id="63898-116">Today, streaming to an Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="63898-117">Vous pouvez créer ou modifier les stratégies d’accès partagé de l’espace de noms Service Bus dans le portail Azure Classic sous l’onglet « Configurer » pour votre espace de noms Service Bus.</span><span class="sxs-lookup"><span data-stu-id="63898-117">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="63898-118">Pour mettre à jour le profil de journal d’activité afin d’inclure la diffusion en continu, l’utilisateur qui apporte la modification doit avoir l’autorisation ListKey sur la règle d’autorisation Service Bus.</span><span class="sxs-lookup"><span data-stu-id="63898-118">To update the Activity Log log profile to include streaming, the user making the change must have the ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="63898-119">Il n’est pas nécessaire que l’espace de noms de Service Bus ou du hub d’événements se trouve dans le même abonnement que la ressource générant des journaux, à condition que l’utilisateur qui configure le paramètre ait un accès RBAC approprié aux deux abonnements.</span><span class="sxs-lookup"><span data-stu-id="63898-119">The service bus or event hub namespace does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="63898-120">Via le portail Azure</span><span class="sxs-lookup"><span data-stu-id="63898-120">Via Azure portal</span></span>
1. <span data-ttu-id="63898-121">Accédez au panneau **Journal d’activité** à l’aide du menu sur le côté gauche du portail.</span><span class="sxs-lookup"><span data-stu-id="63898-121">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span></span>
   
    ![Accéder au journal d’activité dans le portail](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="63898-123">Cliquez sur le bouton **Exporter** en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="63898-123">Click the **Export** button at the top of the blade.</span></span>
   
    ![Bouton Exporter dans le portail](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="63898-125">Dans le panneau qui s’affiche, vous pouvez sélectionner les régions pour lesquelles vous voulez diffuser des événements, et l’espace de nom Service Bus dans lequel vous voulez créer un Event Hub pour la diffusion en continu de ces événements.</span><span class="sxs-lookup"><span data-stu-id="63898-125">In the blade that appears, you can select the regions for which you would like to stream events and the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span></span>
   
    ![Panneau Exporter le journal d’activité](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="63898-127">Cliquez sur **Enregistrer** pour enregistrer ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="63898-127">Click **Save** to save these settings.</span></span> <span data-ttu-id="63898-128">Les paramètres sont immédiatement appliqués à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="63898-128">The settings are immediately be applied to your subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="63898-129">Via les applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="63898-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="63898-130">Si un profil de journal existe déjà, vous devez d’abord le supprimer.</span><span class="sxs-lookup"><span data-stu-id="63898-130">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="63898-131">Utiliser `Get-AzureRmLogProfile` pour déterminer s’il existe un profil de journal</span><span class="sxs-lookup"><span data-stu-id="63898-131">Use `Get-AzureRmLogProfile` to identify if a log profile exists</span></span>
2. <span data-ttu-id="63898-132">S’il y en a un, utilisez `Remove-AzureRmLogProfile` pour le supprimer.</span><span class="sxs-lookup"><span data-stu-id="63898-132">If so, use `Remove-AzureRmLogProfile` to remove it.</span></span>
3. <span data-ttu-id="63898-133">Utilisez `Set-AzureRmLogProfile` pour créer un profil :</span><span class="sxs-lookup"><span data-stu-id="63898-133">Use `Set-AzureRmLogProfile` to create a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="63898-134">L’identifiant de règle Service Bus est une chaîne au format : {identifiant de ressource Service Bus}/authorizationrules/{nom de clé}, par exemple</span><span class="sxs-lookup"><span data-stu-id="63898-134">The Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="63898-135">Via l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="63898-135">Via Azure CLI</span></span>
<span data-ttu-id="63898-136">Si un profil de journal existe déjà, vous devez d’abord le supprimer.</span><span class="sxs-lookup"><span data-stu-id="63898-136">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="63898-137">Utiliser `azure insights logprofile list` pour déterminer s’il existe un profil de journal</span><span class="sxs-lookup"><span data-stu-id="63898-137">Use `azure insights logprofile list` to identify if a log profile exists</span></span>
2. <span data-ttu-id="63898-138">S’il y en a un, utilisez `azure insights logprofile delete` pour le supprimer.</span><span class="sxs-lookup"><span data-stu-id="63898-138">If so, use `azure insights logprofile delete` to remove it.</span></span>
3. <span data-ttu-id="63898-139">Utilisez `azure insights logprofile add` pour créer un profil :</span><span class="sxs-lookup"><span data-stu-id="63898-139">Use `azure insights logprofile add` to create a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="63898-140">L’identifiant de règle Service Bus est une chaîne au format : `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="63898-140">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="63898-141">Comment utiliser les données de journal d’Event Hubs ?</span><span class="sxs-lookup"><span data-stu-id="63898-141">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="63898-142">[Le schéma pour le journal d’activité est disponible ici](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="63898-142">[The schema for the Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="63898-143">Chaque événement est dans un tableau d’objets blob JSON appelé « enregistrements ».</span><span class="sxs-lookup"><span data-stu-id="63898-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="63898-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="63898-144">Next Steps</span></span>
* [<span data-ttu-id="63898-145">Archiver le journal d’activité dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="63898-145">Archive the Activity Log to a storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="63898-146">Lire la présentation du journal d’activité Azure</span><span class="sxs-lookup"><span data-stu-id="63898-146">Read the overview of the Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="63898-147">Définir une alerte basée sur un événement de journal d’activité</span><span class="sxs-lookup"><span data-stu-id="63898-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

